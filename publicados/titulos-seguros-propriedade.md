---
title:  "Títulos Seguros de Propriedade com Autoridade do dono"
date:   1998-01-01
categories: 
  - Artigo
tags:
  - Contratos
  - propriedade
author:
  - Nick Szabo
---

```
Traduzido por: Matheus Bach
Revisado por: Cypherpunks Brasil
```
[```ver lista de contribuidores```](/about/#contribuidores)


<small>Nick Szabo</small>

#### Originalmente publicado em 1998  

===exibe no card daqui pra baixo===

O advento da escrita melhorou muito o rastreamento dos direitos de propriedade e, de fato, deu origem a nossos modernos sistemas de direitos de propriedade e leis. No entanto, registros escritos provaram ser bastante vulneráveis ao abuso. Um padrão comum durante eras de [instabilidade política ou opressão](http://chronicle.com/free/99/06/99061701t.htm) foi o confisco de terras através da falsificação ou destruição de registros públicos. A reconstrução de registros informais, como a residência registrada em listas telefônicas, mesmo quando possível, é custosa e repleta de erros e potencial para fraudes<sup>[[1]](#fn1)</sup>. Muitas propriedade em alguns países em desenvolvimento não são formalmente tituladas<sup>[[2]](#fn2)</sup>. Mesmo durante eras de estabilidade política em países desenvolvidos, ocorrem muitos problemas graves com [títulos.](http://hobbyfarm.com/buysell11.html)<sup>[[3]](#fn3)</sup> Transcrição direta de registros escritos em um repositório online centralizado tornaria muitos desses problemas ainda piores – registros eletrônicos podem ser altamente vulneráveis a perdas e falsificações, e "hacks internos" são a fonte mais comum de tais ataques. Este artigo propõe um banco de dados de títulos seguro e distribuído para evitar tais ataques contra os direitos de propriedade no futuro.

Muitos tipos de recursos da Internet têm uma característica básica: os usuários devem concordar com seu controle através dos limites de confiança. Um grande exemplo é o nome. O artigo ["Nomes: Descentralizado, Seguro, com Significado Humano: Escolha Dois"](https://web.archive.org/web/20120204172516/http://zooko.com/distnames.html "Names: Decentralized, Secure, Human-Meaningful: Choose Two") dispensa não apenas a onipresença e importância desse problema, mas também a possibilidade de solução.<sup>[[4]](#fn4)</sup> Como alternativa, [petnames](http://www.erights.org/elib/capability/pnml.html) (nomes de animais) são propostos. Esses são, na melhor das hipóteses, meros mnemônicos para traduzir nomes humanamente legíveis em nomes criptográficos; petnames não fazem nada para garantir a nomeação através dos limites de confiança. Todos os três atributos – descentralizado, seguro e com significado humano – deve ser fornecido para que as pessoas se comuniquem e sejam comunicadas com segurança pela Internet, e este documento, juntamente com o artigo [Avanços na Segurança Distribuída]({{url_for('slugview', slug='advances-in-distributed-security')}} "Advances in Distributed Security"), mostram como fornecer todos os três.

De maneira mais geral, mostramos como implementar direitos globais transferíveis, aplicados inteiramente por protocolo, a nomes, atribuições, [bit gold]({{url_for('slugview', slug='bit-gold')}}), e propriedade puramente informatizada de uma entidade específica, mas possuídos e invocados pelo público, e como implementar banco de dados de títulos para outros tipos de propriedade. Para um exemplo específico de direitos de limite de confiança cruzada aplicados inteiramente por protocolo, consulte minha proposta de [integridade de nome em sistemas de arquivos com limite de confiança cruzado](http://szabo.best.vwh.net/nameintegrity.html).

Em todos os casos de direitos de propriedade, há um espaço definido, seja um namespace ou espaço físico, e a tarefa é concordar com atributos simples ou direitos para controlar subdivisões desse espaço. Em alguns casos, um nome ou outro símbolo corresponde a uma pessoa ou objeto pertencente ou controlado por essa pessoa. Por exemplo, os usuários da Internet devem concordar sobre qual nome de domínio corresponde a qual operador do site. Em outros casos, estamos simplesmente preocupados com o controle de uma subdivisão do espaço. Com o setor imobiliário, devemos concordar com quem possui vários direitos (ocupar a superfície, minerar os minerais, etc.) em um pedaço de terra. Com o espectro de rádio, devemos concordar sobre quem possui qual faixa de freqüências e em qual espaço físico (ou poder de transmissão, como uma aproximação facilmente observada do espaço físico usado).

É a hipótese do autor de que todos esses acordos de controle, incluindo o controle sobre a semântica dos símbolos, a serem feitos e respeitados através dos limites da confiança são problemas de concordância e manutenção dos direitos de propriedade. Assim, os resultados deste artigo são muito mais gerais do que podem parecer pela primeira vez. Acredito que este documento forneça uma solução para proteger namespaces e problemas semelhantes, bem como o problema de registrar com segurança acordos sobre os direitos tradicionais de propriedade. Destacar a natureza dos direitos de propriedade dos diretórios públicos também destaca as limitações desses mapeamentos – por exemplo, nomes, endereços e outros símbolos cuja semântica é controlada por uma pessoa podem frequentemente ser delegados, assim como a propriedade pode ser dada ou alugada.

Novos avanços na tecnologia de bancos de dados replicados nos permitirão manter e transferir com segurança a propriedade de uma grande variedade de tipos de propriedade, incluindo não apenas terras, bens móveis, nomes e endereços. Essa tecnologia nos dará registros públicos que podem "sobreviver a uma guerra nuclear", nos moldes do objetivo original do design da Internet. Enquanto bandidos ainda podem tomar propriedade física à força, a existência continuada de registros de propriedade corretos ainda será uma dificuldade para os requerentes usurpadores.

Eu uso palavras políticas neste ensaio como metáforas para descrever como nosso software de título de propriedade hipotético, e especialmente seu protocolo para distribuir o banco de dados de títulos através de uma rede pública, poderia funcionar. Um grupo chamado clube de propriedade se reúne na Internet<sup>[[5]](#fn5)</sup> e decide acompanhar o dono de alguma propriedade. A propriedade é representada por títulos: nomes referentes à propriedade e a chave pública correspondente a uma chave privada mantida pelo seu proprietário atual, assinada pelo proprietário anterior, juntamente com uma cadeia de títulos anteriores. Os nomes dos títulos podem descrever "completamente" a propriedade, por exemplo, alocações em um namspace. (Claro, nomes sempre se referem a algo, a semântica, então tal descrição não é realmente completa). Ou os nomes dos títulos podem ser simplesmente rótulos referentes à propriedade. Várias regras e descrições – mapas, ações e assim por diante – podem ser incluídos.

O clube de propriedade pode ser pensado como um "microgoverno", uma entidade que desempenha globalmente e de forma independente uma função limitada normalmente associada ao governo. Em particular, é uma "microdemocracia constitucional" com baixos custos de entrada e saída. Após as regras de transferência de propriedade terem sido decididas, cada voto deve permanecer dentro desta constituição – de modo que normalmente o voto simplesmente implementará uma operação distribuída de acordo com as regras de propriedade. A votação é necessária não devido a uma ideologia política democrática, mas porque é o resultado ideal na análise de bancos de dados distribuídos com invasores mal-intencionados.<sup>[[6]](#fn6)</sup> Se as regras forem violadas pelos eleitores vencedores, os perdedores corretos podem sair do grupo e reformar um novo grupo, herdando os títulos antigos. Os usuários dos títulos (partes confiantes) que desejam manter os títulos corretos podem verificar com segurança para si mesmos qual grupo dissidente seguiu corretamente as regras e alternou para o grupo correto. Se as regras forem violadas pela perda de eleitores, elas podem ser excluídas da participação adicional tanto dos vencedores corretos quanto das partes confiáveis que seguem as regras.

Este método de votação ou reforma funciona bem onde os custos de saída são baixos. Assim, na prática, os usuários não devem "colocar todos os ovos na mesma cesta", mas clubes de títulos diferentes devem ser usados para diferentes tipos de propriedade. Observe que o principal recurso de segurança do clube não é a votação, mas um conjunto de regras objetivas, muitas vezes automatizadas, e uma trilha de auditoria não comprovada que permite que tanto os membros do clube quanto as partes confiantes verifiquem se cada votação seguiu as regras. Então, para ir mais longe com a metáfora política, um clube de propriedade é uma "microdemocracia constitucional", com ênfase no "constitucional". A votação é necessária, mas é bastante regulamentada.

Para implementar um clube de propriedade, montamos um banco de dados replicado para que os membros do clube, de agora em diante "servidores", possam manter com segurança os títulos de propriedade e transferi-los com segurança mediante solicitação dos proprietários atuais. Na verdade, fazer com que os usuários finais respeitem os direitos de propriedade acordados por este sistema dependerá da natureza específica da propriedade e está além do escopo da consulta atual. O objetivo do banco de dados replicado é simplesmente concordar com segurança sobre quem possui o quê. O banco de dados inteiro é público.

O banco de dados de títulos ideal teria as seguintes propriedades:

1.  A atual proprietária Alice deve poder transferir seu título para apenas uma única contraparte confiável (semelhante ao problema de "gasto duplo" em dinheiro digital)

2.  Os servidores não devem conseguir falsificar transferências

3.  Os servidores não devem poder bloquear transferências de ou para partes politicamente incorretas.

Não podemos alcançar os ideais (1) e (3), por isso introduzimos o "voto" da seguinte maneira. Um bom modelo de bancos de dados replicados seguros é o "Sistema de Quorum Bizantino" de [Malkhi & Reiter](http://www.research.att.com/~dalia/)<sup>[[6]](#fn6)</sup>. Em contraste com o trabalho mais recente em software peer-to-peer, nosso design é baseado em provas matemáticas de segurança em vez de acenar com a mão. Para uma breve discussão sobre essas abordagens de limiar de servidores, veja meu ensaio ["Design de Coalizão para Protocolos Seguros"](http://szabo.best.vwh.net/coalition.html). O banco de dados é replicado em um universo de servidores U, |U|=n. O "sistema de quorum" é uma coleção de subconjuntos (quorum) desses servidores, cada um dos quais se cruza. Cada quórum pode operar em nome do sistema; a interseção garante que as operações feitas em quorums distintos preservam a consistência. Um sistema de quorum tolerante a falhas de servidor bizantinas (maliciosas incondicionalmente) é uma coleção de subconjuntos de servidores, cada um dos quais se cruza em um conjunto contendo muitos servidores corretos para garantir a consistência dos dados replicados. Os autores constroem um protocolo de tal forma que qualquer interseção contenha pelo menos 2f+1 servidores, fornecendo assim resiliência contra até f servidores maliciosos, n > 4f.

Usando esses resultados, parece que podemos abordar nosso banco de dados de títulos ideal da seguinte maneira:

1.  Alice assina o título e a chave pública de Bob e envia esta mensagem para os servidores 2f+1, comprometendo-a a transferir o título para Bob. Bob verifica pelo menos 2f+1 servidores antes de confiar na transferência de Alice.

2.  Nenhuma conspiração de servidores pode forjar a assinatura de Alice (nós conseguimos pelo menos essa conquista idealmente!)

3.  Uma conspiração de >=(1/4)n servidores podem bloquear uma transferência. O único recurso de Alice é usar alguns outros canais para transmitir sua intenção, demonstrando que o registro não seguiu seus desejos e esperando que os canais alternativos sejam mais confiáveis. Bob só tem um recurso similar se ele assinou um documento com Alice demonstrando suas intenções de transferir o título de Alice para Bob. O recurso mais básico é um subconjunto correto de servidores que sai do clube de propriedades e estabelece um novo, e então anuncia sua correção (e prova a incorreção de seu grupo rival) como descrito acima.

O compartilhamento de controle sobre a propriedade, por exemplo, como garantia para um empréstimo, pode ser realizado compartilhando-se a chave privada correspondente à chave pública do proprietário atual. A posse dessa chave privada é necessária para assinar o título; assinaturas de múltiplas entradas também poderiam ser manipuladas. Por isso, pode ser uma boa ideia usar um par de chaves para cada combinação de título e proprietário atual, em vez de pares de chaves representando as identidades dos proprietários. Quando certas condições contratuais são atendidas, como o último pagamento de um empréstimo, isso pode desencadear a geração de um novo par de chaves mantido unicamente pelo proprietário e a transferência do título do par de chaves compartilhado para o novo par de chaves.

## Divisibilidade e Homesteading

As alocações iniciais podem ocorrer mapeando os direitos de propriedade existentes a partir de sua encarnação institucional atual, ou usando os métodos tradicionais de estacamento e negociação de reconhecimento mútuo de reivindicações. Alguns métodos menos dependentes de um regime legal existente para os direitos serão discutidos nesta seção.

Para alguns tipos de alocação, como regiões espaciais ou um namespace hierárquico, desejamos poder subdividir e re-mesclar propriedades. A atual proprietária Alice deve ser capaz de transferir várias partes fracionárias de seu título para várias contrapartes individuais e confiáveis. Uma possibilidade é ter mensagens "divididas" ou "mescladas", onde o proprietário atual de uma propriedade pode aposentar as especificações antigas da propriedade e vinculá-las a novas especificações de propriedade, sendo a mensagem inteira assinada pelo proprietário. Em seguida, as novas especificações de propriedade são introduzidas e consideradas ativas e as antigas consideradas desativadas. Seria responsabilidade dos remetentes subseqüentes garantir que as novas especificações não se cruzem e estejam em bom estado.

Uma forma de abordar o problema do homesteading, ou alocação inicial, chamo de "respeito emergente": Alice reivindica todo o universo não alocado. Bob também o afirma, a mesma especificação de propriedade sob uma assinatura digital diferente. Eles podem então escolher subdividir, vender, dar, etc. propriedade. Cada raiz conflitante cresce como uma árvore em uma alocação de todas as propriedades.

Como resolver árvores com raízes conflitantes? Eventualmente, os bandidos, mecanismos ou acordos informais que impõem direitos de propriedade convergem em uma árvore específica como a alocação padrão e apropriada. As raízes que distribuem mais propriedades a mais pessoas, ou que realmente implementam mecanismos para proteger sua propriedade, ganharão mais respeito pela árvore que começaram.

Em um namespace, os conflitos podem ser resolvidos dando nomes às raízes conflitantes e controlando esses mapeamentos de subtree de nomes como propriedade.

Os usurpadores podem roubar propriedade configurando sua própria raiz e aplicando-a, mas não podem excluir as alocações alternativas. A história está sempre presente como evidência de reivindicações.

Aqueles sem conhecimento em primeira mão de reivindicações conflitantes podem resolvê-los consultando as autoridades e ponderando as opiniões dessas autoridades de acordo com as métricas de confiança, semelhantes às métricas de confiança usadas às vezes para certificados de chave pública.

Com carimbos de data e hora seguros, a homesteading poderia ser feita com base no respeito de um primeiro a chegar, e não no emergente.

## Possessão adversa

Para alguns tipos de propriedade, poderíamos querer acrescentar o direito de posse adversa, ou agachamento formalizado. Aqui está uma maneira geral de implementar um tipo de posse adversa:

1.  As transferências devem ser marcadas com segurança.
2.  As transferências expiram. Para manter a propriedade, o proprietário deve emitir uma nova transferência para si antes da expiração.
3.  Após a expiração, a propriedade pode ser de quem chegar primeiro ou de quem estiver acima considerando uma base de respeito.

Este método não tenta definir ou utilizar um estado de "desuso". Em vez disso, equaciona a atividade da propriedade com a presença on-line ativa de um proprietário que conhece o título e deseja continuar com a propriedade. O custo de manutenção do título pode ser alto, exigindo uma taxa de registro periódica dos proprietários. No entanto, isso introduz o problema de quem obtém o benefício, pelas regras do clube de propriedade, dos lucros dessa taxa e o problema de que a taxa reduz o lucro de possuir a propriedade, mesmo que seja negativa. Uma possibilidade, em que os custos de proteção da propriedade são altos, é cobrar uma "taxa georgiana" com base em alguma estimativa imprecisa, mas objetiva do valor potencial da propriedade, e alocar as taxas para a tarefa de proteger a propriedade. Para chegar a esta estimativa, ou para explicar o uso da propriedade em si, envolveria mecanismos ou observação de características específicas para o tipo de propriedade, como vamos tratar a seguir.

## Correspondência do Terreno

Grande parte dos problemas não abordados acima são de divergência entre as condições reais e direitos de diretório. Por exemplo, posseiros podem legitimamente, aos olhos da maioria dos aplicadores de direitos de propriedade, ocupar e melhorar a terra não utilizada que um registro de título indica ser de propriedade de outros. De Soto<sup>[[2]](#fn2)</sup> descreve posseiros e direitos de propriedade emergentes na fronteira americana e no mundo em desenvolvimento de hoje. Quando nomes são propriedade, um nome pode violar uma marca registrada preexistente, causando a confusão de que tanto o novo namespace quanto o antigo namespace de marca registrada foram projetados para resolver.

Quando a divergência se torna muito grande, é necessária uma solução para lidar com a irrealidade do registro de títulos. Uma dessas soluções é que os posseiros estabeleçam seu próprio registro rival e, em seguida, comprovem a correspondência superior de seu registro com a realidade real em relação ao controle e uso dos recursos. Outra solução para posseiros é usar o mecanismo de posse adversa descrito acima – mas isso só funciona se o custo de manter o título for suficientemente alto.

Outra solução é examinar os incentivos do proprietário do título, para ver se eles correspondem a um controle verdadeiro sobre um recurso. Na maioria dos casos, pode haver incentivo para mentir e não podemos usar esse método. Em alguns casos, há incentivo para dizer a verdade e podemos, com ressalvas, confiar nela. Qualquer pressuposto de incentivo nas regras de propriedade deve ser explicado, para que as partes confiantes possam examinar se as condições que criam o incentivo ainda são válidas.

Outra solução é que as regras do clube de propriedade e o registro incorporem originalmente informações ricas sobre o estado real da propriedade e modifiquem a propriedade e a transferência reais dessa propriedade com base nesse estado, deixando poucas ambiguidades para que possam ser totalmente auditadas por sócios do clube e terceiros. É mais vantajoso quando esta auditoria pode permanecer automatizada, conforme previsto acima. No entanto, a introdução como critério de regra de estados transitórios não registrados (ou não registrados de forma segura) comuns em propriedades físicas faz com que a auditoria, e portanto os títulos, se tornem menos seguros e mais caros.

## Agradecimentos

Meus agradecimentos a Gregory Burch, J.D., Eileen O'Connor, J.D., Melora Svoboda, e muitos outros por seus comentários úteis.

## Referências

1.  Kelly McCollum, ["Using Phone Books, Scholars Build a Data Base for Resettling Kosovars"](http://chronicle.com/free/99/06/99061701t.html) [↩](#ref1)

2.  Hernando de Soto, _The Mystery of Capital_ [↩](#ref2) [↩](#ref2-2)

3.  [Reasons to buy title insurance](http://hobbyfarm.com/buysell11.html) [↩](#ref3)

4.  Bryce "Zooko" Wilcox, [Names: Decentralized, Secure, Human-Meaningful: Choose Two](https://web.archive.org/web/20120204172516/http://zooko.com/distnames.html) [↩](#ref4)

5.  Property on the Internet may take all kinds of new forms. For analysis one recently emerged form, the ownership of open source software projects, see [Eric Raymond, "Homesteading the Noosphere".](http://firstmonday.dk/issues/issue3_10/raymond/index.html) [↩](#ref5)

6.  Malkhi & Reiter, ["Byzantine Quorum Systems"](http://www.research.att.com/~dalia/), STOC97 [↩](#ref6-1) [↩](#ref6-2)

* * *

Por favor, envie seus comentários para nszabo (at) law (dot) gwu (dot) edu

Copyright © 1998,1999,2002,2005 by Nick Szabo  
Permissão para redistribuir sem alteração por este concedida


---
Fonte: [Secure Property Titles with Owner Authority -  Nick Szabo ](https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/securetitle.html)