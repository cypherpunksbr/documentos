---
title:  "Implementando bibliotecas criptográficas tão seguras quanto possível e resistentes ao uso indevido: Parte I"
date:   2020-09-14
categories:
   - Artigo
tags:
  - criptografia
  - tutorial
  - segurança
  - computação
author:
  - Isis Agora Lovecruft
description: "Ao longo dos anos, descobri muitas técnicas para aprender a projetar bibliotecas criptográficas tão seguras quanto possível e resistentes ao uso indevido para algumas primitivas bastante complexas, que gostaria de compartilhar na esperança de que possamos continuar a progredir o estado da arte em criptografia para maior segurança com custo reduzido para criptógrafos e engenheiros de segurança. Se o tempo permitir, espero eventualmente transformar isso em uma série de postagens."
---
```
Traduzido por: Vinicius Yaunner 
Revisado por: Cypherpunks Brasil
```
[```ver lista de contribuidores```](/about/#contribuidores)


## Isis Agora Lovecruft


Ao longo dos anos, descobri muitas técnicas para aprender a projetar bibliotecas criptográficas tão seguras quanto possível e resistentes ao uso indevido para algumas primitivas bastante complexas, que gostaria de compartilhar na esperança de que possamos continuar a progredir o estado da arte em criptografia para maior segurança com custo reduzido para criptógrafos e engenheiros de segurança. Se o tempo permitir, espero eventualmente transformar isso em uma série de postagens.

O *typestate* é aquele que eu aprecio muito, mas não tinha um nome antes de ler **[este artigo](http://cliffle.com/blog/rust-typestate/)**. Recomendo fortemente a leitura, e não irei revisá-lo em detalhes aqui. O *tl;dr*(muito longo; não lido) é que você codifica sua máquina de estado em um sistema de tipos, de forma que mudanças de estado inválidas sejam capturadas em tempo de compilação, e não em tempo de execução.

Considere, por exemplo, esta implementação fragmentada de um protocolo de geração de chave distribuída de duas rodadas

~~~
use curve25519_dalek::ristretto::RistrettoPoint;
use curve25519_dalek::scalar::Scalar;

pub struct Commitment(pub(crate) RistrettoPoint);
pub struct SecretKeyShard(pub(crate) Vec<Scalar>);
pub struct PublicKeyShard(pub(crate) Scalar);
pub struct ProofOfKnowledgeOfSecretKeyShard(pub(crate) Scalar, pub(crate) Scalar);

impl ProofOfKnowledgeOfSecretKeyShard {
    /// Prove em zero-knowledge uma chave secreta.
    pub fn prove(
        secret: &SecretKeyShard
    ) -> ProofOfKnowledgeOfSecretKeyShard {
        // ...
    }

    /// Verifique uma prova de conhecimento de uma chave secreta.
    pub fn verify(
        &self,
    ) -> Result<(), ()> {
        // ...
    }
}

pub struct DistributedKeyGeneration {};

impl DistributedKeyGeneration {
    /// Gere um fragmento do eventual segredo compartilhado, e forme alguns compromissos
    /// uma prova de conhecimento zero sobre esses segredos, a fim de evitar ataques de chaves
    /// não autorizadas, e envie os compromissos e a prova para os outros 
    /// participantes para verificação.
    pub fn round_one_init(
    ) -> (SecretKeyShard, ProofOfKnowledgeOfSecretKeyShard, Vec<Commitment>) {
        // ...
    }

    /// Confira os commits e provas que foram enviados pelos demais participantes.
    pub fn round_one_finish(
        proofs: &Vec<ProofOfKnowledgeOfSecretKeyShard>,
    ) -> Result<(), ()> {
        for proof in proofs.iter() {
            proof.verify()?;
        }
        // ...
    }

    /// Cada participante usa seu fragmento secreto para avaliar um
    /// fragmento diferente da eventual chave pública compartilhada,
    /// que eles enviam para cada participante respectivo.
    pub fn round_two_init(
        secret: &SecretKeyShard,
    ) -> Vec<PublicKeyShard> {
        // ...
    }

    /// Verifique os fragmentos públicos recebidos dos outros participantes,
    /// abortando em caso de falha e, em seguida, calcule nossa chave de assinatura
    /// de longa duração e uma prova de sua correção.

    pub fn round_two_finish(
        secret: &SecretKeyShard,
        public_shards: &Vec<PublicKeyShard>,
        commitments: &Vec<Commitment>,
    ) -> Result<(), ()> {
        // ...
    }
}
~~~

Já está se saindo melhor do que muitas APIs criptográficas que vi por aí pois:

* Em vez de passar blobby arrays de bytes, está pelo menos usando o sistema de tipos para fazer coisas básicas, como garantir que as partes dos fragmentos da chave secreta sejam mantidos separados e tratados de forma diferente dos fragmentos da chave pública, mesmo que compartilhem o mesmo objetos matemáticos subjacentes.
* Possui documentação básica, informando quais ações - fora do escopo desta biblioteca criptográfica - devem ser realizadas com os valores de retorno. (Por exemplo, “enviar os compromissos e comprovantes aos outros participantes para verificação”.)
* Ele tenta usar nomenclatura intuitiva para tipos e variáveis, em vez de condensar as coisas em acrônimos quase indecifráveis ou - pior ainda - usando nomes inexplicáveis[1] de função/variável de uma única letra.

[1] Em minha humilde opinião, não há problema em usar nomes de variáveis de uma única letra ao espelhar os nomes usados em um papel e deixar comentários para deixar claro o que o objeto realmente é, no entanto, é muito provável que este não seja um código que deva ser exposto a um engenheiro de segurança.

Então, como poderia ser melhor?

É precisamente aqui que o padrão de *typestate pattern* brilha. O código acima permitiria a um desenvolvedor fazer:

~~~
let (secret, nipk_of_secret, commitments) = DistributedKeyGeneration::round_one();

send_to_participants(nipk_of_secret, commitments);

let public = DistributedKeyGeneration::round_two_init(&secret);
~~~

Dependendo das especificações do protocolo, pular a chamada para DistributedKeyGeneration::round_one_finish() permite um **[rogue-key attack](https://eprint.iacr.org/2018/417)**, onde um participante desonesto cria um fragmento de chave pública elaborado que nega a contribuição para uma assinatura do outro participante(s) alvo 

Em vez disso, vamos ver como esse ataque conhecido pode ser eliminado inteiramente, *tornando-o detectável em tempo de compilação*.

~~~
use curve25519_dalek::ristretto::RistrettoPoint;
use curve25519_dalek::scalar::Scalar;

pub struct Commitment(pub(crate) RistrettoPoint);
pub struct SecretKeyShard(pub(crate) Vec<Scalar>);
pub struct PublicKeyShard(pub(crate) Scalar);
pub struct ProofOfKnowledgeOfSecretKeyShard(pub(crate) Scalar, pub(crate) Scalar);

impl ProofOfKnowledgeOfSecretKeyShard {
    /// Prove em zero-knowledge uma chave secreta.
    pub fn prove(
        secret: &SecretKeyShard
    ) -> ProofOfKnowledgeOfSecretKeyShard {
        // ...
    }

    /// Verifique uma prova de conhecimento de uma chave secreta.
    pub fn verify(
        &self,
    ) -> Result<(), ()> {
        // ...
    }
}

pub type DistributeKeyGenerationState = DistributedKeyGenerationRound1;

pub struct DistributedKeyGenerationRound1 {
    pub(crate) secret_shards: SecretKeyShard,
    pub proof: ProofOfKnowledgeOfSecretKeyShard,
    pub commitments: Vec<Commitment>,
}; 

impl DistributedKeyGenerationRound1 {
    /// Gere um fragmento do eventual segredo compartilhado, e forme alguns
    /// compromissos e uma prova de conhecimento zero sobre esses segredos, a
    /// fim de evitar ataques de chaves não autorizadas, e envie os
    /// compromissos e a prova para os outros participantes para verificação.
    pub fn init(
    ) -> DistributedKeyGenerationRound1 {
        // ...
    }

    /// Confira os commits e provas que foram enviados pelos demais participantes.
    /// Só progrida para a rodada 2 se as verificações forem aprovadas.
    pub fn progress(
        &self,
        proofs: &Vec<ProofOfKnowledgeOfSecretKeyShard>,
    ) -> Result {
        for proof in proofs.iter() {
            proof.verify()?;
        }

        // ...

        Ok(DistributedKeyGenerationRound2a{ secret_shards: self.secret_shards.clone() }
    }
}

pub struct DistributedKeyGenerationRound2a {
    pub(crate) secret_shards: SecretKeyShard,
}

impl DistributedKeyGenerationRound2a {
    /// Cada participante usa seu fragmento secreto para avaliar um fragmento diferente
    /// da eventual chave pública compartilhada, que eles enviam para cada 
    /// participante respectivo.
    pub fn progress(
        &self,
    ) -> DistributedKeyGenerationRound2b {
        // ...
    }
}

pub struct DistributedKeyGenerationRound2b {
    pub(crate) secret_shards: SecretKeyShard,
    pub public_shards: Vec<PublicKeyShard>,
}

impl DistributedKeyGenerationRound2b {
    /// Verifique os fragmentos públicos recebidos dos outros participantes,
    /// abortando em caso de falha e, em seguida, calcule nossa chave de assinatura
    /// de longa duração e uma prova de sua correção.
    pub fn finish(
        &self,
    ) -> GroupPublicKey {
        // ...
    }
}

pub struct GroupPublicKey(pub RistrettoPoint);
~~~

Com essas mudanças, o código de um desenvolvedor de segurança provavelmente se pareceria mais com isto:

~~~
let state = DistributedKeyGeneration::init();

let proofs = collect_proofs_from_other_participants();

let state = state.progress(&proofs)?.progress();

send_public_shards_to_other_participants(state.public_shards);

let group_public_key = state.progress();
~~~

Se alguma das funções de atualização do estado da máquina for chamada sem o contexto correto, o compilador detecta o erro, reforçando a segurança contra ataques criptográficos antes que eles ocorram.

Este é, embora, um exemplo de brinquedo bastante trivial e simples. Há muitas outras coisas que poderíamos fazer com um sistema de tipos decente para melhorar este código, incluindo, mas não se limitando a:

* Fornecendo um traço RoundTwo para aumento genérico sobre os dois estados tipificados na segunda rodada do protocolo.
* Usar o padrão de **[sealed design](https://rust-lang.github.io/api-guidelines/future-proofing.html#sealed-traits-protect-against-downstream-implementations-c-sealed)** para evitar que terceiros criem implementações adicionais de estados RoundTwo válidos.
* Evitar *clone()/copy()* repetido de dados no estado da máquina (por exemplo, os *secret_shards* que são copiados várias vezes no exemplo acima) abusando de outra característica vazia implementada para todos os estados-tipo para armazenar o estado real em um *heap-allocated pointer* (por exemplo, *Box <ActualState>*) copiado em seu lugar.

Se você gostaria de ver um exemplo mais complexo desses padrões de design todos juntos, tenho **[um esboço de implementação](https://github.com/isislovecruft/ed25519-dalek/blob/9e44fb1c6e060bce9e54480ce1c7387d13c17b75/src/state.rs)** do protocolo MSDL de **["Compact Multi-Signatures for Smaller Blockchains"](https://eprint.iacr.org/2018/483)** de Boneh, Drijvers e Neven.


---
Fonte: [Implementing As-Safe-As-Possible, Misuse-Resistant Cryptographic Libraries: Part I - Isis Agora Lovecruft](https://blog.patternsinthevoid.net/implementing-as-safe-as-possible-misuse-resistant-cryptographic-libraries-part-i.html)