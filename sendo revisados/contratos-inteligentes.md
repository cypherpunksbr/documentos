---
title:  "Contratos Inteligentes"
date:   1994-01-01
author:
  - Nick Szabo
categories:
  - Artigo
tags:
  - contratos
  - transações
  - Smart Contract
---

```
Traduzido por: Vinicius Yaunner
Revisado por: Cypherpunks Brasil
```

# Contratos Inteligentes

Copyright (c) 1994 by Nick Szabo
permissão para redistribuir sem alteração aqui concedida.
------------------------------------------------------------

#### [Glossário](glossario-de-contratos-inteligentes.md)
===exibe no card daqui pra baixo===

Um contrato inteligente é um protocolo de transação computadorizado que executa os termos de um contrato. Os objetivos gerais do projeto de contrato inteligente são satisfazer as condições contratuais comuns (como termos de pagamento, ônus, confidencialidade e até mesmo cumprimento), minimizar exceções maliciosas e acidentais e minimizar a necessidade de intermediários confiáveis. Objetivos econômicos relacionados incluem redução de perdas por fraude, custos de arbitragem e fiscalização e outros custos de transação [1].

Algumas tecnologias que existem hoje podem ser consideradas como contratos inteligentes brutos, por exemplo, terminais e cartões POS, EDI e alocação agórica de largura de banda da rede pública.

**[Os protocolos de moeda digital](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/bearer_contracts.htmlhttps:/)** [2,3] são bons exemplos de contratos inteligentes. Eles permitem o pagamento online ao mesmo tempo que respeitam as características desejadas do papel-moeda: imperdoabilidade, confidencialidade e divisibilidade. Quando olhamos de relance para os protocolos de dinheiro digital, considerando-os no contexto mais amplo do projeto de contrato inteligente, vemos que esses protocolos podem ser usados para implementar uma ampla variedade de títulos eletrônicos ao portador, não apenas dinheiro. Também vemos que, para implementar uma transação cliente-fornecedor completa, precisamos mais do que apenas o protocolo de moeda digital; precisamos de um protocolo que garanta que o produto será entregue caso o pagamento seja feito e vice-versa. Os sistemas comerciais atuais usam uma ampla variedade de técnicas para fazer isso, como correio certificado, troca face a face, confiança no histórico de crédito e agências de cobrança para estender crédito, etc. Contratos inteligentes têm o potencial de reduzir significativamente os custos de fraude e execução de muitas transações comerciais. Os protocolos de moeda digital usam vários dos novos e ricos blocos de construção que vêm dos campos da criptografia e da ciência da computação. A maioria desses componentes ainda não foi amplamente explorada para facilitar os arranjos contratuais, mas o potencial é vasto. Esses subprotocolos incluem acordo bizantino, criptografia simétrica e assimétrica, assinaturas digitais, assinaturas cegas, cortar e escolher, compromisso de bits, [cálculos seguros multipartidários](os-protocolos-de-deus.md), [compartilhamento de segredos](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/secret.html), transferência alheia e computação segura multipartidária. Todos esses, exceto o primeiro, são descritos em [2,3].

As consequências de um projeto inteligente de contrato no direito e na economia dos contratos, e na elaboração de contratos estratégicos (e vice-versa), foram pouco exploradas. Da mesma forma, suspeito que as possibilidades de redução significativa dos custos de transação na execução de alguns tipos de contratos e as oportunidades de criação de novos tipos de negócios e instituições sociais com base em contratos inteligentes são vastas, mas pouco exploradas. Os "cypherpunks" [4] exploraram o impacto político de alguns dos novos blocos de construção do protocolo. O campo de Electronic Data Interchange (EDI), no qual elementos de transações comerciais tradicionais (faturas, recibos, etc.) são trocados eletronicamente, às vezes incluindo criptografia e recursos de assinatura digital, pode ser visto como um precursor primitivo de contratos inteligentes. Na verdade, esses formulários de negócios podem fornecer bons pontos de partida e marcadores de canal para designers de contrato inteligentes.

Uma tarefa importante dos contratos inteligentes, que tem sido amplamente negligenciada pelo EDI tradicional, é comunicar a semântica da transação às partes envolvidas. Há ampla oportunidade em contratos inteligentes para "letras miúdas inteligentes": ações executadas pelo software ocultadas de uma das partes na transação. Por exemplo, as máquinas POS de supermercados não informam aos clientes se seus nomes estão ou não sendo vinculados a suas compras em um banco de dados. Os balconistas nem mesmo sabem, e já processaram milhares de transações assim sob seus narizes. Assim, por meio de ação oculta do software, o cliente está dando informações que ele pode considerar valiosas ou confidenciais, mas o contrato foi redigido e a transação foi desenhada, de forma a ocultar as partes importantes dessa transação do cliente.

Para comunicar bem a semântica da transação, precisamos de boas metáforas visuais para os elementos do contrato. Isso ocultaria os detalhes do protocolo sem abrir mão do controle sobre o conhecimento e a execução dos termos do contrato. Um exemplo primitivo, mas bom, é fornecido pelo software SecureMosiac da CommerceNet. A criptografia é mostrada colocando o documento em um envelope e uma assinatura digital colocando um selo no documento ou envelope. Por outro lado, os servidores Mosaic registram conexões, e às vezes até transações, sem avisar os usuários - ações ocultas clássicas.

Outra área que pode ser considerada em termos de contrato inteligente são os ativos sintéticos [5]. Esses novos títulos são formados pela combinação de títulos (como títulos) e derivativos (opções e futuros) em uma ampla variedade de formas. Estruturas a prazo muito complexas para pagamentos (ou seja, quais pagamentos são feitos quando, a taxa de juros, etc.) agora podem ser incorporadas a contratos padronizados e negociados com baixos custos de transação, devido à análise computadorizada dessas estruturas de prazo complexas. Os ativos sintéticos nos permitem arbitrar as diferentes estruturas de prazo desejadas por diferentes clientes e nos permitem construir contratos que imitam outros contratos, menos certos passivos. Como exemplo do último, foram construídos ativos sintéticos que imitam os retornos das ações das empresas alemãs, sem exigir o pagamento do imposto que os estrangeiros devem pagar ao governo alemão por ganhos de capital em ações alemãs. É importante notar que esses sintéticos _não_ conferem direitos de voto como os originais. Pode ser possível adicionar protocolos de contrato inteligentes para transferir direitos de voto para o sintético. Claro, esses protocolos podem ter que ser bastante seguros para resistir a ataques da jurisdição de terceiros, cujo custo de transação (o imposto) está sendo arbitrado pelo ativo sintético.

Finalmente, podemos estender o conceito de contratos inteligentes à propriedade. A propriedade inteligente pode ser criada incorporando contratos inteligentes em objetos físicos. Esses protocolos incorporados dariam automaticamente o controle das chaves para operar a propriedade ao agente que possui legitimamente essa propriedade, com base nos termos do contrato. Por exemplo, um carro pode ficar inoperante a menos que o protocolo de desafio-resposta adequado seja concluído com seu proprietário de direito, evitando o roubo. Se um empréstimo fosse feito para comprar aquele carro e o proprietário deixasse de fazer os pagamentos, o contrato inteligente poderia automaticamente invocar uma garantia, que devolve o controle das chaves do carro ao banco. Essa [garantia inteligente](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/smart.liens.html) pode ser muito mais barata e eficaz do que um repo man. Também é necessário um protocolo para remover comprovadamente a garantia quando o empréstimo for quitado, bem como dificuldades e exceções operacionais. Por exemplo, seria rude revogar a operação do carro enquanto ele está fazendo 75 na rodovia.

A propriedade inteligente pode estar longe, mas o dinheiro digital e os ativos sintéticos estão aqui hoje, e mecanismos de contrato mais inteligentes estão sendo projetados. Até agora, os critérios de design importantes para automatizar a execução de contratos vieram de campos díspares, como economia e criptografia, com pouca comunicação cruzada: pouca consciência da tecnologia, por um lado, e pouca consciência de seus melhores usos comerciais, por outro. A ideia dos contratos inteligentes é reconhecer que esses esforços buscam objetivos comuns, que convergem para o conceito de contratos inteligentes.

Referências:
[1] _The New Palgrave: Allocation, Information, and Markets_
[2] Bruce Schneier, _Applied Cryptography_ (digital cash
objectives are on pg. 123)
[3] _Crypto_ and _Eurocrypt_ conference proceedings, 1982-1994.
[4] "Crypto Rebels", Wired #2, also cypherpunks mailing list
(mail to majordomo@toad.com with body "subscribe cypherpunks")
[5] Perry H. Beaumont, _Fixed Income Synthetic Assets_

[Artigos e ensaios mais recentes sobre contratos inteligentes e a história e o futuro dos controles comerciais e segurança.](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/index.html)


Fonte : [szabo.best.vwh.net/smart.contracts.html](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/smart.contracts.html)
