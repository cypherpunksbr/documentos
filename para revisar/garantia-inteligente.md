---
title:  "Garantia Inteligente"
date:   1994-01-01
author:
  - Nick Szabo
categories:
  - Artigo
tags:
  - Garantia Inteligente
  - Transações
  - Smart Liens
---
```
Traduzido por: Vinicius Yaunner
Revisado por: Cypherpunks Brasil
```

# Garantia Inteligente

Copyright (c) 1994 by Nick Szabo
permissão para redistribuir sem alteração aqui concedida.
------------------------------------------------------------

Imagine que seu governo falisse, deixando você sem jurisdição que você e seus vizinhos fossem obrigados a cumprir para viver naquele território. O caos prevaleceria ou um arranjo novo e melhor poderia tomar o lugar do governo? Seria ainda possível, em particular, obrigar o pagamento de dívidas e responsabilidades penais?

Agora imagine que seu governo ainda não está falido, mas pode muito bem se tornar falido se não cortar custos. Uma forma de cortar custos é melhorar a eficiência da função do governo que é mais vital para a economia, o cumprimento de contratos. Como podemos reduzir o ônus de tal imposição sobre os futuros contribuintes sem colocar em risco a livre iniciativa produtiva? A garantia inteligente pode ser uma nova maneira poderosa de realizar essas tarefas.

Primeiro, vamos introduzir a noção de uma agência de proteção (AP), que embora faça parte do setor privado voluntário, poderia assumir muitas das funções jurisdicionais do governo. As APs se diferenciariam dos governos por terem territórios sobrepostos, ou mesmo por serem não territoriais, permitindo aos clientes escolher entre uma ampla variedade de APs competitivas as APs que melhor atendem aos seus objetivos. Já gastamos mais com segurança privada do que com a polícia financiada pelo governo para nos proteger contra o crime, então não pense que as APs são rebuscadas ou perigosas. Sua capacidade de fazer cumprir contratos e cobrar dívidas, em vez de apenas proteger contra o crime, seria muito melhorada com a técnica de penhoras inteligentes, permitindo que as APs aliviassem governos endividados e seus contribuintes desses encargos de execução.

Como cobrar dívidas? Nenhum banco sábio emprestará a um agente (um agente pode ser uma pessoa real ou virtual, também conhecido como uma corporação) mais do que está coberto por garantias seguras e alguma função conservadora de sua reputação de pagamento integral e dentro do prazo. Para todos os agentes, tanto o crédito quanto a responsabilidade estão intimamente relacionados e são limitados.

A responsabilidade dos agentes é limitada pelas garantias desse agente e pela capacidade de dissuadi-lo por meio de ameaças de punição por violar contratos (ou seja, cometer crimes conforme definido no contrato com a AP). O potencial para outras ações que um agente pode tomar que causem responsabilidade, como danos a pessoas ou propriedades de terceiros, também precisa ser limitado. Mais sobre isso mais tarde.

Muitos agentes, especialmente os novos entrantes, podem não ter esse capital de reputação e, portanto, precisarão ser capazes de compartilhar sua propriedade com o banco por meio de garantias seguras. A garantia é, em um sentido prático, um método de compartilhar um pedaço de propriedade entre o "dono do registro" e um "titular da garantia", em vez de a propriedade ter estritamente um proprietário. Os ônus são usados em muitas transações de crédito de grande porte, como empréstimos para compra de automóveis, hipotecas, empréstimos agrícolas, etc. Eles são impostos pela jurisdição especificada no contrato; geralmente essa fiscalização é feita pelo governo e subsidiada pelos contribuintes, em vez de paga pelas partes contratantes. (Na verdade, esse geralmente é o caso com contratos e direitos de propriedade em geral, a cláusula de execução é um subsídio governamental implícito). Uma maneira de implementar uma garantia sem governos é por meio da co-assinatura com seu AP (desde que o AP tenha uma boa classificação de crédito e o direito contratual de tomar as medidas cabíveis contra você). Outra maneira é o que chamo de "garantia inteligente". Uma garantia inteligente é um sistema criptográfico eletrônico por meio do qual ambas as partes precisam se identificar com a propriedade para que ela funcione corretamente. Por exemplo, um penhor inteligente sobre um imóvel controlaria os serviços públicos (eletricidade, água, etc.), desligando-os se o titular da garantia ou o proprietário assim escolherem, ou se o sistema for adulterado para tentar desativar o penhor.

Como é o caso hoje, os problemas de crédito geralmente serão resolvidos por cartas de advertência escritas de maneira habilidosa e ameaçadoras, bem como notas sobre o rating de crédito de alguém, muito antes de a garantia precisar ser invocada. No entanto, a garantia precisa ser executável para tornar essas cartas de cobrança confiáveis no longo prazo.

Se os APs têm a responsabilidade final pelas atividades criminosas de seus clientes, ou precisam garantir a falta de deserção ou pagamentos futuros por parte dos clientes, eles podem, por sua vez, pedir gravames contra seus clientes, seja com termos contratuais que permitam a prisão de clientes sob certas condições (por exemplo, se eles cometerem atos especificados como criminosos pelo contrato de AP) ou (mais provavelmente para clientes móveis que viajam pelo mundo e com pseudônimos virtuais) garantias inteligentes contra ativos líquidos, como contas bancárias e carteiras de investimento. As garantias inteligentes sobre informações, como títulos ao portador digitais, podem ser implementadas por meio de [compartilhamento secreto](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/secret.html) (duas ou mais chaves necessárias para desbloquear a criptografia).

A "garantia final" seria uma espécie de anti-marcapasso cardíaco controlado pelo portador de segurança. Os clientes de AP provavelmente rejeitariam APs com tal exigência ultrajante, e seria ainda mais nojento para um governo propor tal coisa. No entanto, pode-se imaginar os próprios líderes de AP obrigados a ter garantias finais, controladas por um sistema de votação N-out-of-M de seus clientes e / ou APs estrangeiras com contratação cruzada, como uma proteção contra seu poder. As garantias finais talvez vão contra o imperativo moral que muitos veem por trás do governo limitante, a eliminação da violência e a ameaça de violência no tecido de nossa sociedade, mas se implementadas apenas contra a AP e líderes do governo, elas ainda podem fornecer uma grande melhoria em relação o estado atual das coisas.

Outras áreas importantes de responsabilidade incluem responsabilidade do consumidor e danos à propriedade (incluindo poluição). São necessários mecanismos para que, por exemplo, os danos causados pela poluição a pessoas ou propriedades alheias possam ser avaliados, e existam gravames para que o poluidor seja devidamente cobrado e as vítimas pagas. Onde a poluição é quantificável, como acontece com as emissões de SO2, os mercados podem ser configurados para negociar direitos de emissão. As APs teriam gravames em vigor para monitorar as emissões de seus clientes e avaliar as taxas onde os direitos de emissão foram excedidos.

Infelizmente, existem alguns perigos em que o dano máximo pode ultrapassar qualquer ônus. Uma boa regra prática aqui é que se o risco for contra um terceiro e não puder ser penhorado ou segurado, os APs não devem permitir que seja assumido. As APs que permitem que seus clientes assumam tais riscos contra terceiros não-AP arruinariam sua classificação de crédito. Um exemplo desse risco é a construção de uma usina nuclear para a qual nenhuma seguradora está disposta a apresentar cobertura de responsabilidade. Se uma planta é segura, presumivelmente deve-se ser capaz de convencer uma boa seguradora a cobrir seu potencial de danos à propriedade de terceiros.

As garantias inteligentes são um elemento dos contratos inteligentes. Os contratos inteligentes irão substituir, e até mesmo proteger contra, advogados, políticos e aplicação violenta em muitas empresas e interações sociais. Eles também serão usados para projetar novas instituições de livre mercado lucrativas. Veja meu ensaio Contratos inteligentes para uma introdução aos [contratos inteligentes](/contratos-inteligentes.md).
