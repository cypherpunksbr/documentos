---
title:  'Going Bark: A Furry’s Guide to End-to-End Encryption'
date:   2020-11-14
categories:
  - Artigo
tags:
  - Tutorial
  - Segurança
  - Criptografia
author:
  - Soatok
description: 'Essa template é apenas um exemplo para te ajudar a passar textos para esse padrão. Obviamente esse documento não é para ser traduzido, apenas para servir como exemplo'
---

```
Traduzido por: seu_nome_ou_cypherpunks_brasil
Revisado por: seu_nome_ou_cypherpunks_brasil
```
[```ver lista de contribuidores```](/about/#contribuidores)

# Going Bark: A Furry’s Guide to End-to-End Encryption

Governments are back on their anti-encryption bullshit again.

Between the [U.S. Senate’s “EARN IT” Act,](https://blog.cryptographyengineering.com/2020/03/06/earn-it-is-an-attack-on-encryption/) the [E.U.’s slew of anti-encryption proposals,](https://www.eff.org/deeplinks/2020/10/orders-top-eus-timetable-dismantling-end-end-encryption) and [Australia’s new anti-encryption law,](https://fee.org/articles/australia-s-unprecedented-encryption-law-is-a-threat-to-global-privacy/) it’s become clear that the authoritarians in office view online privacy as a threat to their existence.

Normally, when the governments increase their anti-privacy sabre-rattling, technologists start talking more loudly about Tor, Signal, and other privacy technologies (usually only to be drowned out by paranoid people who think Tor and Signal are government backdoors or something stupid; conspiracy theories ruin everything!).

**I’m not going to do that.**

Instead, I’m going to show you how to add end-to-end encryption to any communication software you’re developing. (Hopefully, I’ll avoid making [any bizarre design decisions](https://soatok.blog/2020/10/28/bizarre-design-choices-in-zooms-end-to-end-encryption/) along the way.)

But first, some important disclaimers:

1. **Yes, you should absolutely do this.** I don’t care how banal your thing is; if you expect people to use it to communicate with each other, you should make it so that you can never decrypt their communications.
2. You should absolutely NOT bill the thing you’re developing as an *alternative* to Signal or WhatsApp.
3. The goal of doing this is to increase the amount of end-to-end encryption deployed on the Internet that the service operator cannot decrypt (even if compelled by court order) and make E2EE normalized. The goal is NOT to compete with highly specialized and peer-reviewed privacy technology.
4. I am not a lawyer, I’m some furry who works in cryptography. The contents of this blog post is not legal advice, nor is it endorsed by any company or organization. Ask the [EFF](https://www.eff.org/) for legal questions.

The organization of this blog post is as follows: First, I’ll explain [how to encrypt and decrypt data between users,](#i-symmetric-key-encryption) assuming you have a key. Next, I’ll explain [how to build an authenticated key exchange](#ii-key-agreement) and [a ratcheting protocol to determine the keys used in the first step.](#session-key-management) Afterwards, I’ll [explore techniques for binding authentication keys to identities and managing trust.](#iii-identity-key-management) Finally, I’ll discuss [strategies for making it impractical to ever backdoor your software (and impossible to silently backdoor it),](#iv-backdoor-resistance) just to piss [the creeps and tyrants of the world](https://en.wikipedia.org/wiki/Five_Eyes) off even more.

You don’t have to implement the full stack of solutions to protect users, but the further you can afford to go, the safer your users will be from privacy-invasive policing.

## Preliminaries

### Choosing a Cryptography Library

In the examples contained on this page, I will be using the [Sodium cryptography library.](https://libsodium.gitbook.io/doc/) Specifically, my example code will be written with the [Sodium-Plus](https://github.com/paragonie/sodium-plus) library for JavaScript, since it strikes a good balance between performance and being cross-platform.

```
const { SodiumPlus } = require('sodium-plus');
    
(async function() {
    // Select a backend automatically
    const sodium = await SodiumPlus.auto();
    
    // Do other stuff here
})();
```

Libsodium is [generally the correct choice for developing cryptography features in software,](https://latacora.micro.blog/2018/04/03/cryptographic-right-answers.html) and is available in most programming languages,

If you’re prone to choose a different library, you should consult your cryptographer (and yes, you should have one on your payroll if you’re doing things different) about your design choices.

### Threat Modelling

Remember above when I said, “You don’t have to implement the full stack of solutions to protect users, but the further you can afford to go, the safer your users will be from privacy-invasive policing”?

How far you go in implementing the steps outlined on this blog post should be informed by [a threat model,](https://adamcaudill.com/2016/07/20/threat-modeling-for-applications/) not an ad hoc judgment.

For example, if you’re encrypting user data and storing it in the cloud, you probably want to pass [the Mud Puddle Test:](https://blog.cryptographyengineering.com/2012/04/05/icloud-who-holds-key/)

>1. First, drop your device(s) in a mud puddle.
>2. Next, slip in said puddle and crack yourself on the head. When you regain consciousness you’ll be perfectly fine, but won’t for the life of you be able to recall your device passwords or keys.
>3. Now try to get your cloud data back.
>
>Did you succeed? If so, you’re screwed. Or to be a bit less dramatic, I should say: your cloud provider has access to your ‘encrypted’ data, as does the government if they want it, as does any rogue employee who knows their way around your provider’s internal policy checks.
>
>Matthew Green describes the Mud Puddle Test, which Apple products [definitely don’t pass.](https://sneak.berlin/i18n/2020-11-12-your-computer-isnt-yours.pt-br/)

If you must fail the Mud Puddle Test for your users, make sure you’re clear and transparent about this in the documentation for your product or service.

## I. Symmetric-Key Encryption

The easiest piece of this puzzle is to encrypt data in transit between both ends (thus, satisfying the loosest definition of end-to-end encryption).

At this layer, you already have some kind of symmetric key to use for encrypting data before you send it, and for decrypting it as you receive it.

For example, the following code will encrypt/decrypt strings and return hexadecimal strings with a version prefix.

```
const VERSION = "v1";
 
/**
 * @param {string|Uint8Array} message
 * @param {Uint8Array} key
 * @param {string|null} assocData
 * @returns {string}
 */
async function encryptData(message, key, assocData = null) {
    const nonce = await sodium.randombytes_buf(24);
    const aad = JSON.stringify({
      'version': VERSION,
      'nonce': await sodium.sodium_bin2hex(nonce),
      'extra': assocData
    });
 
    const encrypted = await sodium.crypto_aead_xchacha20poly1305_ietf_encrypt(
        message,
        nonce,
        key,
        aad
    );
    return (
       VERSION +
       await sodium.sodium_bin2hex(nonce) +
       await sodium.sodium_bin2hex(encrypted)
    );
}
 
/**
 * @param {string|Uint8Array} message
 * @param {Uint8Array} key
 * @param {string|null} assocData
 * @returns {string}
 */
async function decryptData(encrypted, key, assocData = null) {
    const ver = encrypted.slice(0, 2);
    if (!await sodium.sodium_memcmp(ver, VERSION)) {
        throw new Error("Incorrect version: " + ver);
    }
    const nonce = await sodium.sodium_hex2bin(encrypted.slice(2, 50));
    const ciphertext = await sodium.sodium_hex2bin(encrypted.slice(50));
    const aad = JSON.stringify({
      'version': ver,
      'nonce': encrypted.slice(2, 50),
      'extra': assocData
    });
     
    const plaintext = await sodium.crypto_aead_xchacha20poly1305_ietf_decrypt(
        ciphertext,
        nonce,
        key,
        aad
    );
    return plaintext.toString('utf-8');
}
```

Under-the-hood, this is using [XChaCha20-Poly1305,](https://soatok.blog/2020/07/12/comparison-of-symmetric-encryption-methods/#aes-gcm-vs-xchacha20poly1305) which is less sensitive to timing leaks than AES-GCM. However, like AES-GCM, this encryption mode doesn’t provide [message- or key-commitment.](https://eprint.iacr.org/2019/016)

If you want key commitment, you should derive two keys from ```$key``` using a KDF based on hash functions: One for actual encryption, and the other [as a key commitment value.](https://eprint.iacr.org/2020/1153)

If you want message commitment, you can use AES-CTR + HMAC-SHA256 or XChaCha20 + BLAKE2b-MAC.

If you want both, ask [Taylor Campbell](https://mumble.net/~campbell/) about his [BLAKE3-based design.](https://github.com/BLAKE3-team/BLAKE3/issues/138)

A modified version of the above code with key-commitment might look like this:

```
const VERSION = "v2";
 
/**
 * Derive an encryption key and a commitment hash.
 * @param {CryptographyKey} key
 * @param {Uint8Array} nonce
 * @returns {{encKey: CryptographyKey, commitment: Uint8Array}}
 */
async function deriveKeys(key, nonce) {
    const encKey = new CryptographyKey(await sodium.crypto_generichash(
        new Uint8Array([0x01].append(nonce)),
        key
    ));
    const commitment = await sodium.crypto_generichash(
        new Uint8Array([0x02].append(nonce)),
        key
    );
    return {encKey, commitment};
}
 
/**
 * @param {string|Uint8Array} message
 * @param {Uint8Array} key
 * @param {string|null} assocData
 * @returns {string}
 */
async function encryptData(message, key, assocData = null) {
    const nonce = await sodium.randombytes_buf(24);
    const aad = JSON.stringify({
      'version': VERSION,
      'nonce': await sodium.sodium_bin2hex(nonce),
      'extra': assocData
    });
    const {encKey, commitment} = await deriveKeys(key, nonce);
 
    const encrypted = await sodium.crypto_aead_xchacha20poly1305_ietf_encrypt(
        message,
        nonce,
        encKey,
        aad
    );
    return (
       VERSION +
       await sodium.sodium_bin2hex(nonce) +
       await sodium.sodium_bin2hex(commitment) +
       await sodium.sodium_bin2hex(encrypted)
    );
}
 
/**
 * @param {string|Uint8Array} message
 * @param {Uint8Array} key
 * @param {string|null} assocData
 * @returns {string}
 */
async function decryptData(encrypted, key, assocData = null) {
    const ver = encrypted.slice(0, 2);
    if (!await sodium.sodium_memcmp(ver, VERSION)) {
        throw new Error("Incorrect version: " + ver);
    }
    const nonce = await sodium.sodium_hex2bin(encrypted.slice(2, 50));
    const ciphertext = await sodium.sodium_hex2bin(encrypted.slice(114));
    const aad = JSON.stringify({
      'version': ver,
      'nonce': encrypted.slice(2, 50),
      'extra': assocData
    });
    const storedCommitment = await sodium.sodium_hex2bin(encrypted.slice(50, 114));
    const {encKey, commitment} = await deriveKeys(key, nonce);
    if (!(await sodium.sodium_memcmp(storedCommitment, commitment))) {
        throw new Error("Incorrect commitment value");
    }
     
    const plaintext = await sodium.crypto_aead_xchacha20poly1305_ietf_decrypt(
        ciphertext,
        nonce,
        encKey,
        aad
    );
    return plaintext.toString('utf-8');
}
```

Another design choice you might make is to encode ciphertext with base64 instead of hexadecimal. That doesn’t significantly alter the design here, but it does mean your decoding logic has to accommodate this.

You SHOULD version your ciphertexts, and include this in the AAD provided to your AEAD encryption mode. I used “v1” and “v2” as a version string above, but you can use your software name for that too.

## II. Key Agreement

If you’re not familiar with [Elliptic Curve Diffie-Hellman](https://soatok.blog/2020/04/21/elliptic-curve-diffie-hellman-for-humans-and-furries/) or [Authenticated Key Exhcanges,](https://soatok.blog/2020/04/21/authenticated-key-exchanges/) the two of the earliest posts on this blog were dedicated to those topics.

Key agreement in libsodium uses Elliptic Curve Diffie-Hellman over Curve25519, or X25519 for short.

There are many schools of thought for extending ECDH into an authenticated key exchange protocol.

We’re going to implement what the Signal Protocol calls [X3DH](https://signal.org/docs/specifications/x3dh/) instead of doing some interactive EdDSA + ECDH hybrid, because X3DH provides cryptographic [deniability](https://soatok.blog/2020/11/04/a-brief-introduction-to-deniability/) (see [this section](https://signal.org/docs/specifications/x3dh/#deniability) of the X3DH specification for more information).

For the moment, I’m going to assume a client-server model. That may or may not be appropriate for your design. You can substitute “the server” for “the other participant” in a peer-to-peer configuration.

Head’s up: This section of the blog post is code-heavy.

**Update (November 23, 2020):** I implemented this design in TypeScript, if you’d like something tangible to work with. I call my library, [Rawr X3DH.](https://github.com/soatok/rawr-x3dh)

## X3DH Pre-Key Bundles

Each participant will need to upload an Ed25519 identity key once (which is a detail covered in another section), which will be used to sign bundles of X25519 public keys to use for X3DH.

Your implementation will involve a fair bit of boilerplate, like so:

```
/**
 * Generate an X25519 keypair.
 *
 * @returns {{secretKey: X25519SecretKey, publicKey: X25519PublicKey}}
 */
async function generateKeyPair() {
    const keypair = await sodium.crypto_box_keypair();
    return {
        secretKey: await sodium.crypto_box_secretkey(keypair),
        publicKey: await sodium.crypto_box_publickey(keypair)
    };
}
 
/**
 * Generates some number of X25519 keypairs.
 *
 * @param {number} preKeyCount
 * @returns {{secretKey: X25519SecretKey, publicKey: X25519PublicKey}[]}
 */
async function generateBundle(preKeyCount = 100) {
    const bundle = [];
    for (let i = 0; i < preKeyCount; i++) {
        bundle.push(await generateKeyPair());
    }
    return bundle;
}
 
/**
 * BLAKE2b( len(PK) | PK_0, PK_1, ... PK_n )
 *
 * @param {X25519PublicKey[]} publicKeys
 * @returns {Uint8Array}
 */
async function prehashPublicKeysForSigning(publicKeys) {
    const hashState = await sodium.crypto_generichash_init();
    // First, update the state with the number of public keys
    const pkLen = new Uint8Array([
        (publicKeys.length >>> 24) & 0xff,
        (publicKeys.length >>> 16) & 0xff,
        (publicKeys.length >>> 8) & 0xff,
        publicKeys.length & 0xff
    ]);
    await sodium.crypto_generichash_update(hashState, pkLen);
    // Next, update the state with each public key
    for (let pk of publicKeys) {
        await sodium.crypto_generichash_update(
            hashState,
            pk.getBuffer()
        );
    }
    // Return the finalized BLAKE2b hash
    return await sodium.crypto_generichash_final(hashState);
}
 
/**
 * Signs a bundle. Returns the signature.
 *
 * @param {Ed25519SecretKey} signingKey
 * @param {X25519PublicKey[]} publicKeys
 * @returns {Uint8Array}
 */
async function signBundle(signingKey, publicKeys) {
    return sodium.crypto_sign_detached(
        await prehashPublicKeysForSigning(publicKeys),
        signingKey
    );
}
 
/**
 * This is just so you can see how verification looks.
 *
 * @param {Ed25519PublicKey} verificationKey
 * @param {X25519PublicKey[]} publicKeys
 * @param {Uint8Array} signature
 */
async function verifyBundle(verificationKey, publicKeys, signature) {
    return sodium.crypto_sign_verify_detached(
        await prehashPublicKeysForSigning(publicKeys),
        verificationKey,
        signature
    );
}
```

This boilerplate exists just so you can do something like this:

```
/**
 * Generate some number of X25519 keypairs.
 * Persist the bundle.
 * Sign the bundle of publickeys with the Ed25519 secret key.
 * Return the signed bundle (which can be transmitted to the server.)
 *
 * @param {Ed25519SecretKey} signingKey
 * @param {number} numKeys
 * @returns {{signature: string, bundle: string[]}}
 */
async function x3dh_pre_key(signingKey, numKeys = 100) {
    const bundle = await generateBundle(numKeys);
    const publicKeys = bundle.map(x => x.publicKey);
    const signature = await signBundle(signingKey, publicKeys);
     
    // This is a stub; how you persist it is app-specific:
    persistBundleNotDefinedHere(signingKey, bundle);
     
    // Hex-encode all the public keys
    const encodedBundle = [];
    for (let pk of publicKeys) {
        encodedBundle.push(await sodium.sodium_bin2hex(pk.getBuffer()));
    }
     
    return {
        'signature': await sodium.sodium_bin2hex(signature),
        'bundle': encodedBundle
    };
}
```

And then you can drop the output of ```x3dh_pre_key(secretKey)``` into a JSON-encoded HTTP request.

In accordance to Signal’s X3DH spec, you want to use ```x3dh_pre_key(secretKey, 1)``` to generate the “signed pre-key” bundle and ```x3dn_pre_key(secretKey, 100)``` when pushing 100 one-time keys to the server.

### X3DH Initiation

This section conforms to the [Sending the Initial Message section of the X3DH specification.](https://signal.org/docs/specifications/x3dh/#sending-the-initial-message)

When you initiate a conversation, the server should provide you with a bundle containing:

* Your peer’s Identity key (an Ed25519 public key)
* Your peer’s current Signed Pre-Key (an X25519 public key)
* (If any remain unburned) One of your key’s One-Time Keys (an X25519 public key) — and then delete it

If we assume the structure of this response looks like this:

```
/**
 * Get SK for initializing an X3DH handshake
 *
 * @param {object} r -- See previous code block
 * @param {Ed25519SecretKey} senderKey
 */
async function x3dh_initiate_send_get_sk(r, senderKey) {
    const identityKey = new Ed25519PublicKey(
       await sodium.sodium_hex2bin(r.IdentityKey)
    );
    const signedPreKey = new X25519PublicKey(
        await sodium.sodium_hex2bin(r.SignedPreKey.PreKey)
    );
    const signature = await sodium.sodium_hex2bin(r.SignedPreKey.Signature);
 
    // Check signature
    const valid = await verifyBundle(identityKey, [signedPreKey], signature);
    if (!valid) {
        throw new Error("Invalid signature");
    }
    const ephemeral = await generateKeyPair();
    const ephSecret = ephemeral.secretKey;
    const ephPublic = ephemeral.publicKey;
 
    // Turn the Ed25519 keys into X25519 keys for X3DH:
    const senderX = await sodium.crypto_sign_ed25519_sk_to_curve25519(senderKey);
    const recipientX = await sodium.crypto_sign_ed25519_pk_to_curve25519(identityKey);
     
    // See the X3DH specification to really understand this part:
    const DH1 = await sodium.crypto_scalarmult(senderX, signedPreKey);
    const DH2 = await sodium.crypto_scalarmult(ephSecret, recipientX);
    const DH3 = await sodium.crypto_scalarmult(ephSecret, signedPreKey);
    let SK;
    if (r.OneTimeKey) {
        let DH4 = await sodium.crypto_scalarmult(
            ephSecret,
            new X25519PublicKey(await sodium.sodium_hex2bin(r.OneTimeKey))
        );
        SK = kdf(new Uint8Array(
             [].concat(DH1.getBuffer())
             .concat(DH2.getBuffer())
             .concat(DH3.getBuffer())
             .concat(DH4.getBuffer())
        ));
        DH4.wipe();
    } else {
        SK = kdf(new Uint8Array(
             [].concat(DH1.getBuffer())
             .concat(DH2.getBuffer())
             .concat(DH3.getBuffer())
        ));        
    }
 
    // Wipe keys
    DH1.wipe();
    DH2.wipe();
    DH3.wipe();
    ephSecret.wipe();
    senderX.wipe();
 
    return {
        IK: identityKey,
        EK: ephPublic,
        SK: SK,
        OTK: r.OneTimeKey // might be NULL
    };
}
 
/**
 * Initialize an X3DH handshake
 *
 * @param {string} recipientIdentity - Some identifier for the user
 * @param {Ed25519SecretKey} secretKey - Sender's secret key
 * @param {Ed25519PublicKey} publicKey - Sender's public key
 * @param {string} message - The initial message to send
 * @returns {object}
 */
async function x3dh_initiate_send(recipientIdentity, secretKey, publicKey, message) {
    const r = await get_server_response(recipientIdentity);
    const {IK, EK, SK, OTK} = await x3dh_initiate_send_get_sk(r, secretKey);
    const assocData = await sodium.sodium_bin2hex(
        new Uint8Array(
            [].concat(publicKey.getBuffer())
            .concat(IK.getBuffer())
        )
    );
     
    /*
     * We're going to set the session key for our recipient to SK.
     * This might invoke a ratchet.
     *
     * Either SK or the output of the ratchet derived from SK
     * will be returned by getEncryptionKey().
     */
    await setSessionKey(recipientIdentity, SK);
     
    const encrypted = await encryptData(
        message,
        await getEncryptionKey(recipientIdentity),
        assocData
    );
    return {
        "Sender": my_identity_string,
        "IdentityKey": await sodium.sodium_bin2hex(publicKey),
        "EphemeralKey": await sodium.sodium_bin2hex(EK),
        "OneTimeKey": OTK,
        "CipherText": encrypted
    };
}
```

We didn’t define ```setSessionKey()``` or ```getEncryptionKey()``` above. It will be covered later.

### X3DH – Receiving an Initial Message

This section implements the [Receiving the Initial Message section of the X3DH Specification.](https://signal.org/docs/specifications/x3dh/#receiving-the-initial-message)

We’re going to assume the structure of the request looks like this:

```
{
    "Sender": "...",
    "IdentityKey": "...",
    "EphemeralKey": "...",
    "OneTimeKey": "...",
    "CipherText": "..."
}
```

The code to handle this should look like this:

```
/**
 * Handle an X3DH initiation message as a receiver
 *
 * @param {object} r -- See previous code block
 * @param {Ed25519SecretKey} identitySecret
 * @param {Ed25519PublicKey} identityPublic
 * @param {Ed25519SecretKey} preKeySecret
 */
async function x3dh_initiate_recv_get_sk(
    r,
    identitySecret,
    identityPublic,
    preKeySecret
) {
    // Decode strings
    const senderIdentityKey = new Ed25519PublicKey(
        await sodium.sodium_hex2bin(r.IdentityKey),
    );
    const ephemeral = new X25519PublicKey(
        await sodium.sodium_hex2bin(r.EphemeralKey),
    );
     
    // Ed25519 -> X25519
    const senderX = await sodium.crypto_sign_ed25519_pk_to_curve25519(senderIdentityKey);
    const recipientX = await sodium.crypto_sign_ed25519_sk_to_curve25519(identitySecret);
     
    // See the X3DH specification to really understand this part:
    const DH1 = await sodium.crypto_scalarmult(preKeySecret, senderX);
    const DH2 = await sodium.crypto_scalarmult(recipientX, ephemeral);
    const DH3 = await sodium.crypto_scalarmult(preKeySecret, ephemeral);
    let SK;
     
    if (r.OneTimeKey) {
        let DH4 = await sodium.crypto_scalarmult(
            await fetchAndWipeOneTimeSecretKey(r.OneTimeKey),
            ephemeral
        );
        SK = kdf(new Uint8Array(
             [].concat(DH1.getBuffer())
             .concat(DH2.getBuffer())
             .concat(DH3.getBuffer())
             .concat(DH4.getBuffer())
        ));
        DH4.wipe();
    } else {
        SK = kdf(new Uint8Array(
             [].concat(DH1.getBuffer())
             .concat(DH2.getBuffer())
             .concat(DH3.getBuffer())
        ));        
    }
 
    // Wipe keys
    DH1.wipe();
    DH2.wipe();
    DH3.wipe();
    recipientX.wipe();
    return {
        Sender: r.Sender,
        SK: SK,
        IK: senderIdentityKey
    };
}
 
/**
 * Initiate an X3DH handshake as a recipient
 *
 * @param {object} req - Request object
 * @returns {string} - The initial message
 */
async function x3dh_initiate_recv(req) {
    const {identitySecret, identityPublic} = await getIdentityKeypair();
    const {preKeySecret, preKeyPublic} = await getPreKeyPair();
    const {Sender, SK, IK} = await x3dh_initiate_recv_get_sk(
        req,
        identitySecret,
        identityPublic,
        preKeySecret,
        preKeyPublic
    );
    const assocData = await sodium.sodium_bin2hex(
        new Uint8Array(
            [].concat(IK.getBuffer())
            .concat(identityPublic.getBuffer())
        )
    );
    try {
        await setSessionKey(senderIdentity, SK);
        return decryptData(
            req.CipherText,
            await getEncryptionKey(senderIdentity),
            assocData
        );
    } catch (e) {
        await destroySessionKey(senderIdentity);
        throw e;
    }
}
```

And with that, you’ve successfully implemented X3DH and symmetric encryption in JavaScript.

We abstracted some of the details away (i.e. ```kdf()```, the transport mechanisms, the session key management mechanisms, and a few others). Some of them will be highly specific to your application, so it doesn’t make a ton of sense to flesh them out.

One thing to keep in mind: According to the X3DH specification, participants should regularly (e.g. weekly) replace their Signed Pre-Key in the server with a fresh one. They should also publish more One-Time Keys when they start to run low.

If you’d like to see a complete reference implementation of X3DH, as I mentioned before, [Rawr-X3DH](https://github.com/soatok/rawr-x3dh) implements it in TypeScript.

### Session Key Management

Using X3DH to for every message is inefficient and unnecessary. Even the Signal Protocol doesn’t do that.

Instead, Signal [specifies a Double Ratchet protocol](https://signal.org/docs/specifications/doubleratchet/) that combines a Symmetric-Key Ratchet on subsequent messages, and a Diffie-Hellman-based ratcheting protocol.

Signal even specifies [integration guidelines for the Double Ratchet with X3DH.](https://signal.org/docs/specifications/doubleratchet/#integration-with-x3dh)

It’s worth reading through the specification to understand their usages of Key-Derivation Functions (KDFs) and KDF Chains.

Although it is recommended to use HKDF as the Signal protocol specifies, you can *strictly speaking* use any secure keyed PRF to accomplish the same goal.

What follows is an example of a symmetric KDF chain that uses BLAKE2b with 512-bit digests of the current session key; the leftmost half of the BLAKE2b digest becomes the new session key, while the rightmost half becomes the encryption key.

```
const SESSION_KEYS = {};
 
/**
 * Note: In reality you'll want to have two separate sessions:
 * One for receiving data, one for sending data.
 *
 * @param {string} identity
 * @param {CryptographyKey} key
 */
async function setSessionKey(identity, key) {
    SESSION_KEYS[identity] = key;
}
 
async function getEncryptionKey(identity) {
    if (!SESSION_KEYS[identity]) {
        throw new Error("No session key for " + identity");
    }
    const blake2bMac = await sodium.crypto_generichash(
        SESSION_KEYS[identity],
        null,
        64
    );
    SESSION_KEYS[identity] = new CryptographyKey(blake2bMac.slice(0, 32));
    return new CryptographyKey(blake2bMac.slice(32, 64));
}
```

In the interest of time, a full DHRatchet implementation is left as an exercise to the reader (since it’s mostly a state machine), but using the appropriate functions provided by sodium-plus ```(crypto_box_keypair()```, ```crypto_scalarmult()```) should be relatively straightforward.

Make sure your KDFs use domain separation, as per the Signal Protocol specifications.

### Group Key Agreement

Signal Protocol specified X3DH and the Double Ratchet for securely encrypting information between two parties.

Group conversations are trickier, because you have to be able to encrypt information that multiple recipients can decrypt, add/remove participants to the conversation, etc.

(The same complexity comes with multi-device support for end-to-end encryption.)

The best design I’ve read to date for tackling group key agreement is the [IETF Messaging Layer Security RFC draft.](https://datatracker.ietf.org/doc/draft-ietf-mls-protocol/?include_text=1)

I am not going to implement the entire MLS RFC in this blog post. If you want to support multiple devices or group conversations, you’ll want a complete MLS implementation to work with.

### Brief Recap

That was a lot of ground to cover, but we’re not done yet.

So far we’ve tackled encryption, initial key agreement, and session key management. However, we did not flesh out how Identity Keys (which are signing keys–Ed25519 specifically–rather than Diffie-Hellman keys) are managed. That detail was just sorta hand-waved until now.

So let’s talk about that.

## III. Identity Key Management

There’s a meme among technology bloggers to write a post titled “Falsehoods Programmers Believe About _____”.

Fortunately for us, Identity is one of the topics that furries are positioned to understand better than most (due to fursonas): Identities have a many-to-many relationship with Humans.

In an end-to-end encryption protocol, each identity will consist of some identifier (phone number, email address, username and server hostname, etc.) and an Ed25519 keypair (for which the public key will be published).

***But how do you know whether or not a given public key is correct for a given identity?***

This is where we segue into one of the hard problems in cryptography, where the solutions available are entirely dependent on your threat model: **Public Key Infrastructure (PKI).**

Some common PKI designs include:

1. Certificate Authorities (CAs) — TLS does this
2. Web-of-Trust (WoT) — The PGP ecosystem does this
3. Trust On First Use (TOFU) — SSH does this
4. [Key Transparency](https://security.googleblog.com/2017/01/security-through-transparency.html) / Certificate Transparency (CT) — TLS also does this for ensuring CA-issued certificates are auditable (although it was originally meant to replace Certificate Authorities)

And you can sort of choose-your-own-adventure on this one, depending on what’s most appropriate for the type of software you’re building and who your customers are.

One design I’m particularly fond of is called [Gossamer,](https://github.com/paragonie/libgossamer/tree/master/docs) which is a PKI design without Certificate Authorities, originally designed for making WordPress’s automatic updates more secure (i.e. so every developer can sign their theme and plugin updates).

Since we only need to maintain an up-to-date repository of Ed25519 identity keys for each participant in our end-to-end encryption protocol, this makes Gossamer a suitable starting point.

Gossamer specifies a limited grammar of **Actions** that can be performed: **AppendKey, RevokeKey, AppendUpdate, RevokeUpdate,** and **AttestUpdate.** These actions are signed and published to an append-only cryptographic ledger.

I would propose a sixth action: **AttestKey,** so you can have WoT-like assurances and [key-signing parties.](https://en.wikipedia.org/wiki/CryptoParty) (If nothing else, you should be able to attest that the identity keys of other cryptographic ledgers in the network are authentic at a point in time.)

## IV. Backdoor Resistance

In the previous section, I proposed the use of Gossamer as a PKI for Identity Keys. This would provide Ed25519 keypairs for use with X3DH and the Double Ratchet, which would in turn provide session keys to use for symmetric authenticated encryption.

If you’ve implemented everything preceding this section, you have a full-stack end-to-end encryption protocol. But let’s make intelligence agencies and surveillance capitalists even more mad by making it impractical to backdoor our software (and impossible to silently backdoor it).

***How do we pull that off?***

You want [Binary Transparency.](https://wiki.mozilla.org/Security/Binary_Transparency)

For us, the implementation is simple: Use Gossamer as it was originally intended (i.e. to secure your software distribution channels).

Gossamer provides up-to-date verification keys and a commitment to a cryptographic ledger of every software update. You can learn more about its inspiration [here.](https://paragonie.com/blog/2016/10/guide-automatic-security-updates-for-php-developers)

It isn’t enough to merely use Gossamer to manage keys and update signatures. You need independent third parties to use the **AttestUpdate** action to assert one or more of the following:

1. That builds are reproducible from the source code.
2. That they have reviewed the source code and found no evidence of backdoors or exploitable vulnerabilities.

(And then you should let your users decide which of these independent third parties they trust to vet software updates.)

### Closing Remarks

The U.S. Government cries and moans a lot about “criminals going dark” and wonders a lot about how to solve the “going dark problem”.

If more software developers implement end-to-end encryption in their communications software, then maybe one day they won’t be able to use dragnet surveillance to spy on citizens and they’ll be forced to do actual detective work to solve actual crimes.

Y’know, like their job description actually entails?

Let’s normalize end-to-end encryption. Let’s normalize backdoor-resistant software distribution.

Let’s collectively tell the intelligence community in every sophisticated nation state the one word they don’t hear often enough:

Especially if you’re a furry. Because [we improve everything!](https://soatok.blog/2020/04/23/never-underestimate-the-furry-fandom/) :3

## Questions You Might Have

### What About Private Contact Discovery?

That’s one of the major reasons why the thing we’re building isn’t meant to compete with Signal (and it MUST NOT be advertised as such):

Signal is a privacy tool, and their servers have no way of identifying who can contact who.

What we’ve built here isn’t a complete privacy solution, it’s only providing end-to-end encryption (and possibly making NSA employees cry at their desk).

### Does This Design Work with Federation?

Yes. Each identifier string can be [username] at [hostname].

### What About Network Metadata?

If you want anonymity, you want to use Tor.

### Why Are You Using Ed25519 Keys for X3DH?

If you only read the [key agreement section](#ii-key-agreement) of this blog post and the fact that I’m passing around Ed25519 public keys seems weird, you might have missed [the identity section](#iii-identity-key-management) of this blog post where I suggested piggybacking on another protocol called Gossamer to handle the distribution of Ed25519 public keys. (Gossamer is also beneficial for [backdoor resistance](#iv-backdoor-resistance) in software update distribution, as described in the subsequent section.)

Furthermore, we’re actually using birationally equivalent X25519 keys derived from the Ed25519 keypair for the X3DH step. This is a deviation from what Signal does (using X25519 keys everywhere, then [inventing an EdDSA variant to support their usage](https://signal.org/docs/specifications/xeddsa/)).

```
const publicKeyX = await sodium.crypto_sign_ed25519_pk_to_curve25519(foxPublicKey);
const secretKeyX = await sodium.crypto_sign_ed25519_sk_to_curve25519(wolfSecretKey);
```

(Using fox/wolf instead of Alice/Bob, because it’s cuter.)

This design pattern has a few advantages:

1. It makes Gossamer integration seamless, which means you can use Ed25519 for identities and still have a deniable X3DH handshake for 1:1 conversations while implementing the rest of the designs proposed.
2. This approach to X3DH can be implemented entirely with libsodium functions, without forcing you to write your own cryptography implementations (i.e. for XEdDSA).

The only disadvantages I’m aware of are:

1. It deviates from Signal’s core design in a subtle way that means you don’t get to claim the exact same advantages Signal does when it comes to peer review.
2. Some cryptographers are distrustful of the use of birationally equivalent X25519 keys from Ed25519 keys (although there isn’t a vulnerability any of them have been able to point me to that doesn’t involve torsion groups–which libsodium’s implementation already avoids).

If these concerns are valid enough to decide against my implementation above, I invite you to talk with cryptographers about your concerns and then propose alternatives.

### Has Any of This Been Implemented Already?

You can find implementations for the designs discussed on this blog post below:

* [Rawr-X3DH](https://github.com/soatok/rawr-x3dh) implements X3DH in TypeScript (added 2020-11-23)

I will update this section of the blog post as implementations surface.


---
Fonte: https://soatok.blog/2020/11/14/going-bark-a-furrys-guide-to-end-to-end-encryption/