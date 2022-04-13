---
title:  'HODL de Bitcoin com Privacidade'
date:   2022-04-12
author:
  - 6102bitcoin
  - Bitdov
categories:
  - Tutorial
tags:
  - Bitcoin
  - Privacidade
description: 'As maneiras de interagir com o bitcoin estão melhorando com o tempo e as melhores maneiras de utilizar o bitcoin estão cada dia mais sofisticadas e fáceis de usar. Este guia tem como intenção ajudar você a se armar com as ferramentas para fazer seu HODL com privacidade.'
---

```
Fork de HODL-privacy da 6102bitcoin, traduzido e alterado por bitdov

Revisado por: Matheus Bach
```

## HODL de Bitcoin com Privacidade

*   [Motivação](#motivação)
*   [Vazamentos de dados potenciais](#vazamentos-de-dados-potenciais)
    *   [Exchanges](#exchanges-de-bitcoin)
    *   [Exploradores de blocos](#exploradores-de-blocos)
    *   [Conversão de quantia exata](#conversão-de-quantia-exata)
    *   [Plugins do navegador](#plugins-do-navegador)
    *   [Software de hardwallet](#software-de-hardwallet)
    *   [Carteira com autenticação 2FA por e-mail](#carteira-com-autenticação-2fa-por-e-mail)
    *   [Download de bloco limitado](#download-de-bloco-limitado)
    *   [HTTP](#http)
    *   [Confirmações por e-mail](#confirmações-por-e-mail)
*   [Vídeos de dicas de Privacidade no Bitcoin dos bitcoinheiros](#vídeos-para-entender-sobre-privacidade-no-bitcoin)


![media](../stuff/primeira_regra_bitcoin_privacidade.png)

## Motivação

Já há algum tempo estou pensando sobre a privacidade no Bitcoin. Durante o mês de fevereiro de 2020 preparei [vários vídeos sobre privacidade](https://www.youtube.com/playlist?list=PLgcVYwONyxmhS94ynhdPIK6quG_OcprXf) para compartilhar o que eu sei até o momento e ajudar os bitcoinheiros a entenderem melhor quais são realmente as implicações de privacidade, quem são nossos adversários, o que devemos fazer para não vincular nossas informações pessoais com endereços de bitcoin e como evitar que terceiros nos monitorem. É um assunto que me intriga bastante e não poderia ser diferente - sou um pseudônimo que usa um [rig de urso para se apresentar nas interwebs](https://www.youtube.com/playlist?list=PLgcVYwONyxmhrlSK1ykcCEb6oOeE3kS1c)

> “A moda agora parece ser dizer que o Bitcoin é completamente transparente e ainda pior que o sistema bancário para a privacidade. Mas me responda o seguinte: **se eu sair na rua, trocar dinheiro por BTC e guardar esses satoshis na minha carteira privada, qual corporação vai saber quanto eu tenho?**”

A resposta é que vai depender muito das ferramentas e serviços que você usar.

*   Utilizando as melhores ferramentas do bitcoin **com cuidado**, é **impossível** que alguém saiba quanto bitcoin você tem.
*   Utilizando as piores ferramentas (e geralmente as mais comuns) **sem cuidado**, é **possível** que um adversário motivado tenha uma boa ideia do seu saldo total com o tempo.

A maioria dos vazamentos de informação potenciais identificados não vinculam suas moedas diretamente com a sua pessoa física. Eles vinculam dados que podem ser vinculados a você (através do endereço IP, por exemplo). Geralmente é a combinação de várias fontes de dados que cria problemas, os famosos data points.

**Não se desespere**: As maneiras de interagir com o bitcoin estão melhorando com o tempo e as melhores maneiras de utilizar o bitcoin estão cada dia mais sofisticadas e fáceis de usar. Este guia tem como intenção ajudar você a se armar com as ferramentas para fazer seu HODL com privacidade.

---

## Vazamentos de dados potenciais

Para cada vazamento de dado potencial identificado, listei:

*   **Ato**: Como você pode se expor e vazar dados acidentalmente
*   **Dados vazados**: Qual informação pode vazar e para quem
*   **Como mitigar**: Como você pode limitar/evitar o vazamento de dados

---

### Exchanges de Bitcoin

#### Ato:

Você cria uma conta em uma exchange e compra bitcoins se identificando totalmente, oferecendo todos os seus dados pessoais para aquela instituição.

#### Dados vazados:

A empresa ou os indivíduos por trás da corretora coletam todas as informações sobre você e vinculam essas informações com seus endereços bitcoin. Algumas corretoras também colaboram com [empresas de espionagem na blockchain](https://www.youtube.com/watch?v=Si2UtIPYydE) para seguir seus passos depois que você faz a compra e sempre que deposita nela. Todo esse compartilhamento de dados por si só, já é um grande risco para a segurança dos usuários dessas corretoras. Além disso, desde 1/Ago/2019 essa situação se agravou com a necessidade da corretora compartilhar dados sobre suas transações para a receita, aumentando ainda mais a superfície de ataque. Seus adversários potenciais são funcionários corruptos da exchange, da empresa de espionagem da blockchain, da receita e qualquer bandido que conseguir acesso ao banco de dados da exchange, da empresa de espionagem ou da receita. Ao coletar e armazenar essas informações sensíveis, todas as partes se transformam em alvo para bandidos em busca de informação. Esse é um problema que foi herdado do sistema bancário tradicional, mas que no caso das criptmoedas pode colocar a segurança do usuário em maior risco, especialmente aqueles mais obedientes que "não tem nada para esconder".

#### Como mitigar:

Lembre-se que sua privacidade está totalmente exposta nessas exchanges e que você deve atuar de acordo para fazer a sua segurança pessoal se adquirir fundos através dessas instituições de vigilância e controle. A melhor maneira de mitigar esse risco é votando com seu dinheiro: não comprando mais nessas exchanges enquanto não respeitarem você.

Assista [Comprando bitcoins com privacidade](https://www.youtube.com/watch?v=ixoN6IP-yq) e veja alternativas em nosso [Guia de Introdução ao Bitcoin](https://bitcoinheiros.com/intro-bitcoin/#passo-9-comprando-privacidade) ou na tabela de exchanges [KYC? Sai fora!](https://bitcoinheiros.com/kyc)

Aprenda mais sobre [Coinjoin](https://www.youtube.com/playlist?list=PLgcVYwONyxmgxF0k5qMR15Ym7Qo2Wkall) se já comprou na exchange com KYC/AML e quer usar com privacidade

---

### Exploradores de blocos

#### Ato:

Você usa um site explorador de blocos para verificar seus endereços, confirmar se recebeu pagamentos.

#### Dados vazados:

A empresa ou o indivíduo por trás do explorador de blocos pode vincular qualquer informação que você inserir no site (como endereços de bitcoin ou id de transações) com seu endereço IP. Se você verifica se um endereço de bitcoin tem saldo nele, é um sinal fraco-médio de que é o seu endereço... Se você verifica se um endereço de bitcoin tem saldo nele e ele recém recebeu bitcoin ou logo depois que você verificou ele recebeu bitcoin, esse é um sinal forte de que se trata de um endereço de bitcoin seu.

#### Como mitigar:

Acesse os Block Explorers usando TOR. (como o [blockstream.info](http://explorerzydxu5ecjrkwceayqybizmpjjznk5izmitf2modhcusuqlid.onion/)) ou rode seu próprio [software de block explorer](https://github.com/janoside/btc-rpc-explorer) que puxa dados do seu full node privado e soberano.

Veja este vídeo no canal dos bitcoinheiros: [Blockchain explorer é ruim para a privacidade](https://www.youtube.com/watch?v=WpeXvjRW62c)

---

### Conversão de quantia exata

#### Ato:

Buscar ‘Quanto vale x.xxxxxxx BTC em R$’ (ou utlizar outras ferramentas de conversão na web).

#### Dados vazados:

Se a quantia de bitcoin que você buscou fizer parte de um único UTXO e for um valor único, então o buscador ou site podem associar aquele endereço de IP com aquele valor cruzado na blockchain. Se o buscador for o Google, por exemplo, e você estiver conectado, eles podem até vincular aquele UTXO com você (eles têm quase todas as suas informações pessoais).

#### Como mitigar:

Busque com o [DuckDuckGo através do TOR](http://3g2upl4pq6kufc4m.onion/) | Busque com menos precisão x.xx BTC | Calcule manualmente

---

### Plugins do navegador

#### Ato:

Você utiliza um plugin com acesso para todos os websites que você visita e faz alguma das coisas listadas acima ou mais.

#### Dados vazados:

O desenvolvedor do plugin obtem uma cópia dos dados vazados acima (através de exploradores de blocos ou conversão de valores exatos). Além de outros comportamentos e sites relacionados com bitcoin que você visita.

#### Como mitigar:

Evite plugins com acesso muito amplo do seu histórico de navegação | Utilize um navegador especial sem plugins (Tor Browser, por exemplo) quando fizer coisas relacionadas com bitcoin | Utilize o modo de navegação incógnito/privado para fazer coisas relacionadas com bitcoin sem cookies ou plugins.

---

### Software de hardwallet

#### Ato:

Você utiliza a carteira/software fornecida pela fabricante da sua hardwallet.

#### Dados vazados:

A maioria das hardwallets vem com um software/site que envia suas chaves públicas para os servidores da fabricante da hardware wallet. Isso significa que o fabricante da hardwallet pode vincular seu endereço IP com suas moedas. Se o fabricante da sua hardwallet requisitar que você tenha uma conta ou compartilhe outras informações pessoais, então ele também pode vincular esses dados com suas moedas.

#### Como mitigar:

Utilize carteiras de bitcoin que não vazam dados sobre suas moedas, como por exemplo a carteira [electrum](https://electrum.org/#home) com [electrum personal server](https://github.com/chris-belcher/electrum-personal-server) ou a [wasabi wallet](https://wasabiwallet.io).

Assista estes [vídeos dos bitcoinheiros sobre a Electrum Wallet](https://www.youtube.com/playlist?list=PLgcVYwONyxmjZuXVmllvk1H5Yyb95u0X2)  
Assista estes [vídeos sobre a Wasabi Wallet](https://www.youtube.com/playlist?list=PLgcVYwONyxmgLuVTL2BgUcS4Muh5Jgiuw)

---

### Carteira com autenticação 2FA por e-mail

#### Ato:

Você usa uma carteira com autenticação 2FA por e-mail que não está conectada exclusivamente com seu próprio node.

#### Dados vazados:

Seu endereço de e-mail pode ser vinculado com suas moedas, porque a carteira vaza informação sobre suas moedas para o servidor do desenvolvedor da carteira junto com seu endereço IP (que pode ser loggado quando você forneceu seu endereço de e-mail).

#### Como mitigar:

Evite autenticação 2FA por e-mail (opte por alternativas como o Google Authenticator sempre que possível) para carteiras de bitcoin e conecte sua carteira com seu próprio node.

---

### Download de bloco limitado

#### Ato:

Você usa uma carteira light que tem regras de download de blocos pouco sofisticadas através da internet pública (clearnet).

#### Dados vazados:

A maioria das carteiras light baixam apenas os blocos relevantes para suas transações, facilitando que adversários monitorando os blocos que você baixa (como seu provedor de internet) possam identificar os endereços em comum dentro daqueles blocos. Seu provedor pode então conectar seu ponto de conexão à internet / endereço IP com suas moedas.

#### Como mitigar:

Utilize uma carteira que se conectar com seu full node (que baixa **todos os blocos**, impedindo esse ataque) | Utilize uma carteira que preserva sua privacidade (como a [wasabi wallet](https://www.youtube.com/playlist?list=PLgcVYwONyxmgLuVTL2BgUcS4Muh5Jgiuw)).

---

### HTTP

#### Ato:

Você faz qualquer uma das coisas acima sem uma conexão criptografada com o servidor com o qual se comunica (como através do protocolo http).

#### Dados vazados:

Seu provedor pode interceptar todos os dados vazados acima. Se estiver usando Tor, o exit relay também pode interceptar todos os dados.

#### Como mitigar:

Conecter-se apenas através de HTTPS (busque pelo cadeado ao lado da URL). Existe um [plugin da EFF que força a usar https](https://www.eff.org/https-everywhere) em todos os sites. Outro bom plugin deles é o [Privacy Badger](https://www.eff.org/privacybadger) que bloqueia trackers que também podem comprometer sua privacidade.

---

### Confirmações por e-mail

#### Ato:

Você compra mais BTC para seu HODL usando uma exchange online para enviar para um endereço de armazenamento cold que você já usou no passado.

#### Dados vazados:

E-mails de confirmação confirmando o saque vazam o endereço para seu provedor de e-mail (como a Google/Microsoft). A corretora também pode vincular sua conta de e-mail (e outras informações que ela tenha) com aquele endereço.

#### Como mitigar:

Desativar notificações se possível | Utilizar um e-mail dedicado que não esteja conectado com a sua identidade.

Assista este vídeo sobre o risco da [Reutilização de endereços](https://www.youtube.com/watch?v=6-xD5fcX7MI) para a privacidade  
Veja como as exchanges podem [vazar seus dados para empresas de análise da Blockchain](https://www.youtube.com/watch?v=Si2UtIPYydE)  
Não se assuste, você ainda pode [comprar bitcoins com privacidade](https://www.youtube.com/watch?v=ixoN6IP-yq4)  

---

## Vídeos para entender sobre Privacidade no Bitcoin

Não deixe de assistir a nossa [playlist de Privacidade no Bitcoin](https://www.youtube.com/playlist?list=PLgcVYwONyxmhS94ynhdPIK6quG_OcprXf) com diversos vídeos para você entender como melhorar a privacidade dos seus bitcoins.

---

Fork do HODL-privacy mantido pelo [6102bitcoin](https://github.com/6102bitcoin)  
Traduzido e alterado para os [bitcoinheiros](https://www.twitter.com/bitcoinheiros) por [bitdov](https://www.twitter.com/bitdov)

ISENÇÃO DE RESPONSABILIDADE:  
Este guia foi preparado para fins meramente informativos/educativos.  
NÃO é uma recomendação financeira nem de investimento.  
Faça sua própria pesquisa e responsabilize-se por suas decisões.  
Não nos responsabilizamos por ações executadas inspiradas neste guia.

---

Fonte: 
[Bitcoinheiros - HODL-privacidade](https://bitcoinheiros.com/hodl-privacidade)
[6102bitcoin - HODL-privacy](https://6102bitcoin.com/faq-hodl-privacy/)