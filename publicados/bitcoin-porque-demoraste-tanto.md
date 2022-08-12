---
title:  'Bitcoin, por que você demorou tanto?'
date:   2011-05-28
author:
  - Nick Szabo
categories:
  - Documentos
tags:
  - Bitcoin
  - Econmomia
  - Tecnologia
description: 'Os motivos que nos fizeam aguardar tanto pelo nascimento do bitcoin'
---

```
Traduzido por: Matheus Bach
```

# Bitcoin, por que você demorou tanto?

_Assim pergunta [Gwern](https://www.gwern.net/Bitcoin-is-Worse-is-Better) em uma exibição espetacular de retrospectiva._

A resposta curta sobre por que demorou tanto tempo é que as ideias do bit gold/Bitcoin não estavam nem remotamente perto de serem óbvias como Gwern sugere. Elas exigiram uma quantidade muito substancial de pensamento não convencional, não apenas sobre a lista de tecnologias de segurança de Gwern (e temo que a lista tenha esquecido uma das maiores, a replicação ponto-a-ponto com resiliencia bizantina), mas sobre como e porquê escolher e reunir esses protocolos. Bitcoin não é uma lista de recursos criptográficos, é um sistema muito complexo de matemática e protocolos interativos em busca do que era um objetivo muito impopular.

Embora a tecnologia de segurança esteja longe de ser trivial, o "porquê" foi de longe o maior obstáculo - quase todos que ouviram a ideia geral acharam que era uma ideia muito ruim. Eu, Wei Dai e Hal Finney fomos as únicas pessoas que conheço que gostaram da ideia (ou no caso de Dai sua ideia relacionada) o suficiente para persegui-la de forma significativa até Nakamoto (assumindo que Nakamoto não é realmente Finney ou Dai). Apenas Finney ([RPOW](../rpow)) e Nakamoto estavam motivados o suficiente para realmente implementar tal esquema.

O "porquê" exige uma compreensão precisa da natureza de dois tópicos difíceis e quase sempre mal compreendidos, sendo eles [a confiança](https://nakamotoinstitute.org/trusted-third-parties/) e a natureza do dinheiro. A sobreposição entre especialistas criptográficos e libertários que podem simpatizar com essa ideia de "[gold bug](wikipedia.org/wiki/The_Gold-Bug)" já é bastante pequena, já que a maioria dos especialistas criptográficos ganha a vida na academia e compartilha seus preconceitos políticos. Mesmo em meio a esse cruzamento incomum, poucas pessoas acharam que era uma boa ideia. Mesmo os gold bugs não se importavam com isso porque já temos ouro real em vez de meros bits e podemos pagar online simplesmente emitindo certificados digitais baseados em ouro real armazenado em cofres reais, como o antigo e popular [e-gold](wikipedia.org/wiki/E-gold). Além da infinidade dessas reações e críticas equivocadas, permanecem muitas questões em aberto e pontos discutíveis sobre esses tipos de tecnologias e moedas, muitas das quais só podem ser resolvidas realmente colocando-as em campo e vendo como elas funcionam na prática, tanto na economia e termos de segurança.

Aqui estão algumas razões mais específicas pelas quais as ideias por trás do Bitcoin estavam muito longe de serem óbvias:

1) apenas algumas pessoas tinham lido sobre as idéias do [bit gold](../bitgold), que embora eu as tenha inventado em 1998 (ao mesmo tempo e na mesma lista de discussão privada onde Dai estava apresentando [b-money](../bmoney) -- é uma longo história) não foram descritos em público até [2005](classic-web.archive.org/web/20060329122942/http://unenumerated.blogspot.com/2005/12/bit-gold.html), embora várias partes dele eu tenha descrito anteriormente, por exemplo, a parte crucial da cadeia de transações assinadas com replicação bizantina, que generalizei no que chamo de [títulos de propriedade seguros](../titulos-seguros-propriedade).

2) Quase ninguém realmente entende de dinheiro. "O dinheiro simplesmente não funciona assim", me disseram com fervor e frequência. "O ouro não poderia funcionar como dinheiro se não estivesse mais brilhante ou útil para eletrônicos ou qualquer outra coisa além de dinheiro", eles me disseram. (Será que os serviços de seguro também têm que começar úteis para outra coisa, talvez como usinas de energia?). Esse argumento comum vem ironicamente de libertários que interpretaram erroneamente o relato de Menger sobre a origem do dinheiro como sendo a única maneira de ele surgir (em vez de um relato de como ele poderia surgir) e, da mesma forma, aplicam erroneamente o teorema da regressão de Mises. Mesmo que eu tenha refutado esses argumentos em meu estudo sobre [as origens do dinheiro](../shelling-out-origens-dinheiro.md), que humildemente sugiro que deveria ser leitura obrigatória para qualquer um debatendo a economia do Bitcoin.

Não há nada como o esquema de incentivo ao mercado de Nakamoto para mudar a opinião sobre essas questões. :-) Graças a RAMs cheias de moedas com "deflação programada", agora não faltam pessoas dispostas a argumentar a seu favor.

3) Nakamoto melhorou uma falha de segurança significativa que meu projeto tinha, que foi exigir que uma prova de trabalho fosse um nó no sistema ponto a ponto resiliente bizantino para diminuir a ameaça de uma parte não confiável controlando a maioria dos nós e, assim, corrompendo vários recursos de segurança importantes. Ainda outra característica óbvia em retrospectiva, bastante não óbvia em previsão.

4) Em vez do meu [mercado automatizado](unenumerated.blogspot.com/2008/04/bit-gold-markets.html) para explicar o fato de que a dificuldade dos quebra-cabeças muitas vezes pode mudar radicalmente com base em melhorias de hardware e avanços criptográficos (ou seja, descobrindo algoritmos que podem resolver provas de trabalho mais rapidamente) e a imprevisibilidade da demanda, Nakamoto projetou um algoritmo aprovado pelos bizantinos ajustando a dificuldade dos quebra-cabeças. Não consigo decidir se esse aspecto do Bitcoin é mais recurso ou mais bug, mas o torna mais simples.

---
Fonte: [Unenumerated Blog](https://unenumerated.blogspot.com/2011/05/bitcoin-what-took-ye-so-long.html)