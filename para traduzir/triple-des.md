---
title:  'Triple DES: How strong is the data encryption standard?'
date:   2020-09-21
categories:
  - Artigo
tags:
  - Adicione tags aqui, um item por linha
author:
  - Jon Callas
description: 'Favor colocar aqui uma descrição'
---

```
Tradução por: Traduza_e_coloque_seu_nome_aqui
Formatação e revisão: Matheus Bach, revise_para_estar_aqui
```
[```ver lista de contribuidores```](/about/#contribuidores)

# Triple DES: How strong is the data encryption standard?

> Expert Jon Callas explains how strong the Triple DES symmetric encryption algorithm actually is and offers guidance on how it compares to other widely used block ciphers.

_The Data Encryption Standard encryption algorithm on which Triple DES is based was first published in 1975. Over the years, as computers grew faster, the block [cipher](https://www.techtarget.com/searchsecurity/definition/cipher) with a simple 56-bit key proved vulnerable to brute force attacks. Then, in 1999, the lifetime of_ [_DES_](https://www.techtarget.com/searchsecurity/definition/Data-Encryption-Standard) _was extended by tripling the key size of the cipher and encrypting data in three passes in the new_ [_Triple DES specification_](http://dx.doi.org/10.6028/NIST.SP.800-67r1)_._

_After more than 40 years of_ _DES, and 20 years of 3DES, the algorithm is showing its age: the_ [_National Institute of Standards and Technology (NIST)_](https://www.techtarget.com/searchsoftwarequality/definition/NIST) _disallowed the use of DES for anything but legacy use in 1999, and two-key 3DES got the hook in 2015. However, the venerable block cipher is still important to understand, both because it is still used to decrypt legacy data, and because, when used with three unique keys, Triple DES is still considered strong enough to protect data._

_Part of what Triple DES does is to protect against_ [_brute force attacks_](https://www.techtarget.com/searchsecurity/definition/brute-force-cracking)_. The original DES_ _symmetric encryption algorithm_ _specified the use of 56-bit keys -- not enough, by 1999, to protect against practical brute force attacks. Triple DES specifies the use of three distinct DES keys, for a total key length of 168 bits. While NIST disallowed the use of two-key 3DES for encryption, it is still approved for legacy use -- though there are still questions over whether using three distinct DES keys for 3DES provides the strength of a single 168-bit key._

_But does 3DES really deliver 168 bits of encryption strength? Not everyone agrees, but cryptographer Jon Callas explains how, and why, the useful life of the DES symmetric key encryption algorithm has been extended through the use of three (and not two or four) encryption rounds with unique keys._

## Triple DES encryption process

What we all call Triple DES operates in three steps: Encrypt-Decrypt-Encrypt (EDE). It works by taking three 56-bit keys (K1, K2 and K3), and encrypting first with K1, decrypting next with K2 and encrypting a last time with K3.

3DES has two-key and three-key versions. In the two-key version, the same [algorithm](https://www.techtarget.com/whatis/definition/algorithm) runs three times, but uses K1 for the first and last steps. In other words, K1 = K3. Note that if K1 = K2 = K3, then Triple DES is really Single DES.

Triple DES was created back when DES was becoming weaker than users accepted. As a result, they sought an easy way to get more strength. In a system that is dependent on DES, making a composite function out of multiple passes of DES is likely to be easier than bolting in a new symmetric cipher. This has the added benefit of sidestepping the political issues that arise from arguing about the relative strength of a new cipher versus DES.

## Keying options and encryption modes

As it turns out, when you compose a cipher into a new one, you can't use a double enciphering. There is a class of attacks called [meet-in-the-middle attacks](https://internetofthingsagenda.techtarget.com/definition/meet-in-the-middle-attack) in which you encrypt from one end, decrypt from the other and start looking for collisions -- keys that produce the same answer in either direction. With sufficient memory, Double DES -- or any other cipher run twice -- would only be twice as strong as the base cipher. In other words, the double cipher would only be as strong as the same cipher run once, but with a key that was one bit longer.

But that's not all: If the cipher forms a group, then encrypting twice with two keys is equivalent to encrypting once with some other key. It's not trivial to know what that other key is, but it does mean that a brute force attack would find that third key as it tried all the possible single keys. So if the cipher is a group, then multiple ciphering is merely a waste of time.

A group is a relationship between a set and an operator. If they behave more or less the way integers do with addition, they form a group. If you keep encrypting a block and it makes a full circuit over the set of possible blocks, that also forms a group.

As you might guess, DES is not a group. If it were, we wouldn't be discussing this at all. However, DES does have known structural features in it that make people say it's not _strongly_ not a group (in other words, it might be a group). For example, there are known loops in DES where, if you keep encrypting with the same key, you run around in a long loop.

With Triple DES, therefore, each of the three rounds can be run in either direction -- encrypt or decrypt -- using the DES algorithm. This results in eight different possible modes for Triple DES.

![Triple DES modes](../stuff/security-triple_des_chart.png)

Those structural features are why you wouldn't want to use EEE or DDD mode if there were a better option, just as you wouldn't want to use EED, DEE, DDE or EDD. Because of the weak-non-groupness of DES, EDE or DED compositions work best. And Encrypt-Decrypt-Encrypt just makes more sense -- if you use Decrypt-Encrypt-Decrypt, you have to explain why your Triple DES encryption starts with decryption.

## Strength of Triple DES

The reason for going through this multiple encryption exercise is to build a composite cipher that is stronger than Single DES. Because of meet-in-the-middle attacks, Double DES is only one bit stronger than Single DES. Two-key Triple DES (which is no longer approved for encryption due to its susceptibility to brute force attacks) thus has 112 bits of strength (56 multiplied by two).

But what about the three-key version of Triple DES? Common sense dictates it should be at least as strong as two-key Triple DES, but how much stronger? The answer is that no one knows.

I've seen arguments suggesting Triple DES always has 112 bits of strength. I've seen arguments suggesting it has the full 168 bits. (Note that this ignores the obvious weak keys, like K1 = K2.) I don't like either argument, and actually think that the ones that suggest you never get more than 112 bits are better arguments -- even though I disagree.

One thing to remember is that, in cryptography, there's a difference between a theoretical attack and a real one. Let's suppose I came up with an attack that needed 2^80 cipher blocks, which would reduce the strength of three-key Triple DES to no stronger than 112 bits. This attack would be worthy of publication, but it would not be practical. A tera-block (eight terabytes) is 2^40 blocks. With this attack, you would need eight tera-terabytes (or, eight trillion trillion bytes) of memory and a CPU that could address that much. Also, you could defend against this attack by rekeying after encrypting just a few million terabytes of data.

So let's come right down to where I live -- [practical cryptography](https://www.techtarget.com/searchsecurity/tip/Three-IoT-encryption-alternatives-for-enterprises-to-consider). If you ask a good cryptographer if 168-bit Triple DES is weaker than other standard 128-bit ciphers, like [Blowfish](https://www.techtarget.com/searchsecurity/definition/Blowfish), CAST or the [Advanced Encryption Standard](https://www.techtarget.com/searchsecurity/definition/Advanced-Encryption-Standard), they'll almost certainly say no -- if you ask the right way. An example of asking the right way would be, "So, are you saying I should use Blowfish instead of Triple DES because it's stronger?"

Even if they think Triple DES is pretty weak, you'll probably get a response like, "Mmmmmm, no, no, that's not what I'm saying," followed by a discussion similar to this one. Likewise, a good cryptographer won't tell you to use Triple DES because it's a stronger alternative to any of the standard 128-bit ciphers.

Therefore, by practical reasoning, Triple DES is about as strong as 128-bit ciphers. It seems safe to guess, therefore, that Triple DES is stronger than 112 bits, but not as strong as the full 168. Somewhere between 113 and 167, 128 bits seems to be a good, conservative compromise for estimating the strength of three-key Triple DES.

That is why we usually compare Triple DES with 128-bit ciphers. If DES were strongly not a group, then it would be 168 bits. Because DES is definitely not a group, but has weakness in that property, we don't exactly know how strong it is, but no one thinks it's all that much weaker than 128 bits. So we just lump it in with the 128-bit ciphers.

---
Fonte: https://www.techtarget.com/searchsecurity/tip/Expert-advice-Encryption-101-Triple-DES-explained