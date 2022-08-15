---
title:  'Uma Linguagem Formal para Analisar Contratos'
date:   2002-08-06
author:
  - Nick Szabo
categories:
  - Documentos
tags:
  - Contratos
  - Smart Contracts
  - Tecnologia
description: 'Apresentação de mini linguagem para profissionais e pesquisadores
interessados em redigir e analisar contratos'
---

```
Traduzido por: Leonardo Broering Jahn
Formatado por: Daniel Miorim e Matheus Bach
```

# Uma Linguagem Formal para Analisar Contratos

*Nick Szabo*

## Rascunho preliminar de 2002

O autor apresenta uma mini linguagem para profissionais e pesquisadores
interessados em redigir e analisar contratos. Destina-se para a leitura
por computadores também. O principal objetivo dessa linguagem é
especificar, da forma mais inequívoca, completa e sucinta possível,
contratos comuns ou termos contratuais. Isso inclui contratos
financeiros, garantias (penhoras) e outros tipos de segurança,
transferência de propriedade, desempenho de serviços on-line e fluxo de
trabalho da cadeia de suprimentos.

Os seguintes problemas podem ser resolvidos pela linguagem quando
interpretados por computador:

1.  Contabilidade e auditoria. Contratos sofisticados, incluindo
    derivativos e combinações, podem ser especificados em nossa
    linguagem formal. Em seguida, regras contábeis automatizadas ou
    manuais podem ser aplicadas para converter transações concluídas sob
    o contrato em trilhas de auditorias e entradas no livro-razão.

2.  Analisar contratos formalmente especificados em busca de falhas na
    lógica, agendamento, oportunidades para as partes violarem o
    contrato, e conflitos com outros contratos com os quais já está
    comprometido[^1].

3.  Traduzir os contratos formais para uma linguagem de programação
    existente, como a E[^2] e/ou protocolos criptográficos[^3], para
    parcial auto execução e execução protegida como contratos
    inteligentes

4.  Alguns tipos de contratos, especialmente contratos financeiros e de
    commodities e seus derivativos, podem ser convertidos em uma árvore
    de decisão que pode ser analisada para determinar o risco, o valor
    presente líquido etc..

O processo de projetar essa linguagem também é uma ótima maneira de
explorar a natureza básica dos contratos (quais são os "elementos" dos
quais uma grande variedade de contratos úteis pode ser redigida?) e como
é composto (quais regras para compor esses átomos descartam contratos
impossíveis?). A linguagem também é uma ferramenta criativa para pensar
e "esboçar" novos tipos de contratos. Eu dou boas-vindas à sua
participação.

As palavras em nossa linguagem seguem a terminologia legal o máximo
possível -- portanto, por exemplo, desempenho significa execução para
satisfazer os termos do contrato (como no campo jurídico), em vez de
quantidades medidas como velocidade, uso de memória, largura de banda
etc. (como os programadores usam o termo). Não é necessário um diploma
em direito para usar a linguagem, mas recomenda-se alguma familiaridade
com o direito contratual e a elaboração de contratos. Um advogado que
tenha se saído razoavelmente bem nas seções analíticas e lógicas do LSAT
dos EUA ou seu equivalente no exterior, eu suspeito, terá melhor sorte
em elaborar contratos nessa linguagem do que um programador cuja única
experiência reside na linguagem processual tradicional. É por isso que
chamo isso de linguagem de rascunho [de projeto] não de linguagem de
programação.

Nossa linguagem pode especificar o resultado de uma negociação (que pode
ser um leilão, uma troca ou duas partes redigindo o contrato, ou uma
redação de uma parte e a outra concordando, etc.) Também pode definir o
input para um mecanismo que conduz e monitora as transações que executam
o contrato:

> Negociação -> Contrato -> Performance

A execução do contrato, ou seja, sua reificação como um contrato
inteligente, pode, portanto, ser vista como (hipoteticamente, neste
momento) execução de um programa escrito em nossa linguagem. Além disso,
nossa linguagem incorpora uma ampla variedade de termos contratuais, não
apenas termos monetários abstratos e seus derivados. Essas duas
características tornam nossa linguagem muito diferente das linguagens de
contrato financeiro para fins especiais, como[^4]. Embora utilizemos
vários exemplos de contratos financeiros para apresentar nossa linguagem
e demonstrar sua flexibilidade, seu escopo tanto na funcionalidade
quanto nos tipos de contratos e protocolos de transação que ela pode
representar é muito mais amplo.

## Semântica

Cada palavra e frase em nossa linguagem tem um significado padrão claro.
Como resultado, podem ser elaborados contratos que estarão muito menos
sujeitos a disputas sobre interpretação. Por outro lado, a linguagem não
é muito boa para expressar muitos conceitos subjetivos e ambíguos que
muitas vezes são necessários em contratos. Nem é bom, em seu estado
atual, referir-se a jurisdições ou doutrinas da lei. A linguagem é, no
entanto, muito diferente de uma linguagem de programação tradicional. Os
termos contratuais são definidos em termos de eventos que acionam seu
desempenho. Tais eventos incluem datas e horários, escolhas feitas pelas
partes, violações observáveis do contrato e assim por diante.

Nossa linguagem não é uma linguagem de marcação. Não se trata de
manipular texto para fins de elaboração de contratos. Não se trata de
estruturar texto, especificar formulários de preenchimento, definir
formatos de dados estáticos ou tarefas semelhantes de linguagens como
HTML ou XML. Para essas tarefas, deve-se usar uma linguagem de marcação
ou uma linguagem de programação de manipulação de texto (por exemplo,
Perl), não essa linguagem. Nossa linguagem faz algo muito diferente. Ela
modela a dinâmica da execução do contrato -- quando e sob quais
condições as obrigações devem ser executadas.

As palavras e frases do idioma não consistem em instruções seguidas na
página de uma etapa para a outra. Em vez disso, um contrato é lido
(tanto por humanos quanto por computador), seguindo definições aninhadas
de termos contratuais à medida que se expandem e observando eventos nas
declarações **when** [quando] e vendo o que eles acionam. Se o redator
precisar construir explicitamente um cronograma passo a passo do
calendário, isso poderá ser feito usando eventos controlados pelo
calendário ou palavras como **for** [para] e **then** [então].

A linguagem incentiva a composição de contratos. Contratos, direitos e
obrigações podem ser aninhados. Chamamos essas estruturas aninhadas de
clauses [cláusulas]. Os contratos e cláusulas envolvem duas partes, o
Holder [Titular], de cujo ponto de vista lemos o contrato, e uma
Counterparty [Contraparte]. Os acordos de várias partes podem ser
elaborados compondo vários contratos de duas partes.

## Exemplo -- Contratos Futuros

Nosso primeiro exemplo é um contrato financeiro bem conhecido, o futuro.
Um futuro é uma obrigação por parte do Titular do contrato futuro de
comprar uma certa quantidade de uma determinada mercadoria em um
determinado mês, e a obrigação por parte do futuro redator do contrato,
a Contraparte, de entregar esses bens. Para fins de introdução deste
contrato, damos-lhe a forma abstrata na qual os analistas financeiros
geralmente lidam com ele, deixando de fora detalhes importantes que
descrevem os terceiros que atuam como intermediários confiáveis para
definir "pacotes justos" de mercadorias, e também deixamos de fora
muitos detalhes sobre a entrega real.

```ruby
future(rightA="1 round lot pork bellies",

rightB="$1,500.00",

p = "for delivery in July 2002") =

when withinPeriod(p)

to Holder rightA with to Counterparty rightB

then terminate
```

Como essa linguagem ainda não está sendo interpretada por computador, a
sintaxe foi projetada mais para legibilidade humana do que para
computador. Serei um pouco rápido e flexível com a sintaxe, e você
também pode. Geralmente uso tabs em vez de colchetes {} para estruturar
as cláusulas de uma maneira que parece natural e legível para mim -- e
espero que para você -- mas que pode confundir um computador. Sinta-se
livre para desenvolver seu próprio estilo.

As três principais linhas do contrato, na forma name(parameters)
[nome(parâmetros)] = nos dizem que estamos definindo uma named clause
[cláusula nomeada]. A cláusula nomeada pode definir um contrato
inteiro ou apenas uma cláusula em um contrato maior. Podemos passar os
nomes de outras cláusulas nomeadas, listas de eventos e outros tipos de
informações que a cláusula nomeada precisa -- esses são os parâmetros.

when withinPeriod(p) significa "quando o primeiro evento do calendário
ou relógio gerado durante o período p". O redator pode, em outro lugar,
definir com que frequência esse evento "tick tack do relógio" ocorre. O
primeiro tique taque de relógio após o início do período, neste caso, o
primeiro dia de entrega programado no mês de julho, aciona a cláusula
entre colchetes {}. Agendas mais sofisticadas são possíveis, como
aquelas que minimizam os custos de entrega da Contraparte, entregando a
diferentes Titulares em dias diferentes em julho. Felizmente, podemos
ocultar esses detalhes de agendamento dentro do evento de calendário e
agendar mecanismos do iterador, deixando o redator livre de se preocupar
exatamente quando os mercados estão abertos, em que dias são finais de
semana ou feriados ou dias bissextos, etc. O cronograma de entrega da
contraparte pode ser negociado ou esse detalhe pode ser deixado para a
contraparte. No contrato acima, as restrições na entrega são que elas
ocorram em julho e somente em conjunto com o pagamento do Titular.

A cláusula mais interna diz para trocar rightA por rightB. Esta cláusula
é dividida em um direito do titular e um direito da contraparte. A
cláusula certa Holder rightA significa "O titular tem o direito de
executar a rightA", nesse caso, a entrega das barrigas de porco. A
cláusula Counterparty rightB significa "A contraparte tem direito de
desempenhar o rightB", que aqui é o pagamento de 1.500 dólares. with
indica uma troca simultânea -- as duas transações devem ocorrer juntas,
talvez intermediadas por um agente de garantia para fazer cumprir as
condições de entrega e pagamento.

Uma sentença then nos permite avançar passo a passo. Se tivéssemos duas
cláusulas escritas assim:

```ruby
to Holder right1

also to Holder right2
```

Elas poderiam ser executados em qualquer ordem -- right2 pode ser
executado primeiro, ou right1 pode ser, ou (provavelmente) o desempenho
em ambos pode prosseguir no mesmo tempo. Várias instruções when
aninhadas juntas no mesmo nível também têm also implícita, pois podem
ser acionadas em qualquer ordem.

Visualize um duende dançarino que segue o aninhamento de cláusulas à
medida que são executadas e de eventos à medida que são capturados. (Os
programadores chamam esse elfo dançarino pelo nome chato de "ponteiro de
instruções"). Pode haver mais de um elfo dançarino se houver um also ou
mais de um quando a sentença for acionada enquanto outra estiver ativa,
mas geralmente precisamos pensar apenas em um de cada vez.

Se desejarmos adicionar a restrição de que right2 não pode ser executado
até que right1 tenha sido, usamos then:

```ruby
to Holder right1

then to Holder right2
```

Os programadores tradicionais ficarão extremamente tentados a preencher
seus contratos com as declarações then, imitando o estilo da programação
procedural. Não fique! Aqueles com experiência em redação de contratos
sabem que, em alguns casos, essa restrição é claramente apropriada e, em
alguns casos, claramente não é, e é importante ser explícito ao
adicionar restrições. Portanto, a seguinte sentença é ilegal e será
rejeitada pelo computador e por qualquer redator que trabalhe sem um
computador:

```ruby
# Do not do this!

to Holder right1

to Holder right2
```

Finalmente, já vimos esse tipo de cláusula:

```ruby
to Holder right1

with to Holder right2
```

Isso significa que right1 e right2 devem ser executados simultaneamente
-- e ambos devem ser executados ou nenhum deles. No jargão dos
cientistas da computação, deve ser uma transação "atômica".

O then terminate no final da cláusula nomeada garante que todos os
direitos e obrigações sob o contrato sejam rescindidos após a execução.
Não é acionado até que o corpo de uma linha do contrato futuro seja
concluído. Bem como quaisquer cláusulas subordinadas pendentes com seus
direitos e obrigações. Essa cláusula está implícita no final de cada
cláusula nomeada, mas, desta vez, a tornamos explícita. Essa cláusula é
frequentemente usada explicitamente quando o redator deseja garantir o
término adequado de cláusulas não nomeadas aninhadas em uma cláusula
nomeada.

Vamos agora prosseguir com o contrato futuro passo a passo, à medida que
as cláusulas são ativadas e executadas. Uma fonte normal indica que a
cláusula está inativa. Uma fonte em negrito indica um estado ativo -- as
cláusulas estão sendo executadas.

Quando as partes se comprometem com o contrato, suas primeiras cláusulas
(as cláusulas no nível mais alto de indentação) são acordadas. Em nosso
contrato futuro, temos apenas uma dessas cláusulas e, portanto, o when
(mas não as cláusulas aninhadas abaixo) entram em um estado ativo,
aguardando o evento withinPeriod ():

```ruby
when withinPeriod(p)

to Holder rightA with to Counterparty rightB

then terminate
```

Quando o calendário avançou até o final da negociação no último dia de
negociação de agosto, o evento withinPeriod (p) ocorre e o when ativa as
cláusulas aninhadas no próximo nível interno. O when em si se torna
inativo -- não está mais aguardando um evento:

```ruby
when withinPeriod(p)

to Holder rightA with to Counterparty rightB

then terminate
```

O then faz com que o terminate espere pelo when e suas subcláusulas
sejam executadas. Depois que a troca de direitos é realizada, as
cláusulas executadas são convertidas em inatividade e o encerramento é
acionado:

```ruby
when withinPeriod(p)

to Holder rightA with to Counterparty rightB

then terminate
```

É fácil generalizar em nossa linguagem. O contrato futuro genérico se
parece com o seguinte:

```ruby
future(rightA, rightB, p) =

when withinPeriod(p)

to Holder rightA with to Counterparty rightB

then terminate
```

Em vez de barrigas de porco, podemos trocar qualquer outro rightA por
rightB, que pode ser uma grande variedade de coisas além do dinheiro. Os
redatores podem especificar clichês gerais e preencher detalhes para
contratos específicos posteriormente.

## Exemplo -- Contrato de Opção

Agora, apresentamos outro tipo de contrato financeiro. Nesta opção
Americana, o Titular tem o direito de comprar por $20 (o preço de
exercício da opção) por ação um lote inteiro (100 ações) da XYZ Corp no
ou antes do último dia de negociação de agosto. Esses tipos de contratos
são chamados de "derivativos" porque a opção de compra é derivada do
direito subjacente (aqui, ações).

```ruby
callOptionAmerican (rightA="1 round lot XYZ Corp.",

rightB="$2,000/lot",

time="end of trading on last trading day of August") =

when beforeTime(time)

when choiceOf(Holder)

to Holder rightA with to Counterparty rightB

when afterTime(time)

terminate
```

Pense naquele elfo dançante novamente. (Ao ler ou escrever em nossa
linguagem, é importante seguir esses elfos dançarinos. Se os elfos se
tornarem irritantes, pense em algum outro personagem ou processo
dinâmico para uma metáfora que seja adequada). À medida que avança, ele
acorda cláusulas, tornando-as ativas, fazendo com que sejam executadas.
Às vezes, pode haver mais de um elfo dançando no código ao mesmo tempo,
por exemplo, se mais de uma instrução when é acionada enquanto outra
está ativa, mas geralmente precisamos pensar apenas em uma de cada vez.

O contrato começa com duendes dançarinos nas duas cláusulas de nível
superior:

```ruby
when beforeTime(time)

when choiceOf(Holder)

to Holder rightA with to Counterparty rightB

when afterTime(time)

terminate
```

Essas instruções when estão aguardando seus respectivos eventos. Como os
eventos são mutuamente exclusivos (é primeiro beforeTime(time), depois
afterTime(time), mas nunca os dois), precisamos nos preocupar apenas com
o primeiro a ser executado. Observe que, a menos que seja separado por
um then, a ordem das cláusulas no mesmo nível não é importante. O código
a seguir é idêntico ao código em nosso exemplo:

```ruby
when afterTime(time)

terminate

when beforeTime(time)

when choiceOf(Holder)

to Holder rightA with to Counterparty rightB
```

O beforeTime(time) é imediatamente ativado, de modo que começamos com
a(s) cláusula(s) aninhada(s) no nível imediatamente abaixo ativadas
também -- nesse caso, when choiceOf(Holder).

```ruby
when beforeTime(time)

when choiceOf(Holder)

to Holder rightA with to Counterparty rightB

when afterTime(time)

terminate
```

Uma série de whenes no mesmo nível nessa cláusula começam a esperar que
algum deles seja acionado. Quando um when recebe um evento lançado
abaixo ou nele, a cláusula aninhada abaixo se torna ativa. Em seguida,
as cláusulas abaixo ficam ativas e são executadas até os whenes do nível
abaixo. Os whenes nesse nível passam de inativos para ativos, agora
aguardando a ocorrência de seus eventos.

O when beforeTime(time) se torna ativo quando a própria opção é ativada
pela primeira vez e permanece ativo até o time. Ao ser ativo, ele ativa
o when choiceOf(Holder). Esse when especifica o evento que dá ao
contrato sua natureza como uma opção -- a escolha de seu titular para
exercê-lo ou não. Se o Titular optar por fazê-lo, o Titular obtém as
ações (rightA) da Contraparte (o autor da opção de compra) em troca do
dinheiro (rightB). Os duendes dançantes passam da cláusula when para a
cláusula swap:

```ruby
when beforeTime(time)

when choiceOf(Holder)

to Holder rightA with to Counterparty rightB

when afterTime(time)

terminate
```

Quando o código fica complicado, talvez não seja possível saber
facilmente se o then terminate implícito no final na última linha será
executado. Portanto, é uma boa ideia dar um terminate no contrato
explicitamente quando a opção expirar.

Veremos exemplos em que mais de um tipo de evento e até sequências de
eventos (como uma agenda de calendário de datas de pagamento) acionam a
execução dos termos contratuais.

Lembre-se de que a linguagem não procede passo a passo por padrão -- em
vez disso, o leitor (humano ou computador) deve seguir as definições de
contrato aninhadas à medida que se expandem e observar os eventos nas
instruções when para ver o que elas acionam. Planejamentos explícitos de
calendário passo a passo podem ser criados usando for, then, e eventos
do calendário.

Aqui está um exemplo que usa essas etapas explícitas. Um bond faz uma
sequência de pagamentos fixos, chamados cupons, regularmente, e depois
efetua um pagamento final, o principal. Não mostramos aqui os detalhes
da programação em si, mas, em geral, uma programação pode ser definida
como qualquer tipo de sequência temporal -- poderíamos pagar cupons no
último dia de cada mês, em todos os feriados japoneses, de acordo com a
computação da Páscoa (não ria -- agendadores de feiras medievais tiveram
que enfrentar esse problema), ou como quisermos. Quando implementados,
os eventos de calendário e o iterador de agendamento contém uma
implementação muito completa que resolve muitos dos problemas
desagradáveis de calendário que geralmente aparecem nos sistemas de
processamento de transações.

for itera pelos eventos no planejamento, um por um, com o when aninhado
ao manipulá-los. Quando aparece após uma cláusula for, um then avança o
iterador mais uma etapa.

```ruby
bond(coupon, principal, schedule) =

for schedule

when withinPeriod(schedule.next)

to Holder coupon

then

when withinPeriod(schedule.next)

to Holder principal
```

Em seguida, esboçamos um contrato para vender um carro a crédito. Sendo
um esboço e não um projeto completo, este é um exemplo simplificado ou
"brinquedo" -- deixamos de lado as taxas, quaisquer referências a um
contrato de seguro relacionado, garantias, renúncias, etc. Também por
simplicidade, temos o banco (aqui o Titular) é igual ao revendedor de
automóveis. Finalmente, não mostramos aqui nenhuma garantia sobre o
carro para garantir o empréstimo. Faremos uma facada em um mecanismo de
penhor no exemplo abaixo.

```ruby
loanPayments(payment, schedule) =

for schedule

when withinPeriod(schedule.next)

payment

carPurchase(car, downPayment, monthlyPayment, schedule) =

to Counterparty getTitle(car) with to Holder downPayment

then to Holder loanPayment(monthlyPayment, schedule)
```

Se quisermos permitir o pagamento antecipado, nossa programação conterá
horários únicos, em vez de períodos com um horário de início e um
término. E nossos pagamentos de empréstimos teriam a seguinte aparência:

```ruby
loanPayments(payment, schedule) =

for schedule

when beforeTime(schedule.next)

payment
```

Poderíamos calcular o pagamento acima com outras informações que
provavelmente veremos no contrato, mas isso envolve apenas uma
programação normal. Podemos usar uma função para executar o cálculo em
primeiro lugar:

```ruby
loanPayments(principal, interest, schedule) =

constant payment.amount = computeInterest(principal, schedule, interest)

# normal computational function goes here

then for schedule

when beforeTime(schedule.next)

payment
```

"=" define, para todo time (portanto, constant [constante]), o número
payment.amount ao valor retornado pela função computeInterest. Também
poderíamos fazer coisas mais complicadas -- deduzir juros por
pré-pagamento ou, ao contrário, adicionar multas por pré-pagamento ou
uma grande variedade de outras condições.

Também podemos estruturar o contrato de compra do carro para que o novo
proprietário não receba o título até depois que o downPayment
[pagamento inicial] for recebido:

```ruby
carPurchase(car, downPayment, monthlyPayment, schedule) =

to Holder downPayment

then to Counterparty getTitle(car)

then to Holder loanPayments(monthlyPayment, schedule)
```

## Cláusulas de Dano

Vamos usar nossa linguagem para analisar alguns avanços importantes na
história das instituições econômicas. Gênova era uma cidade independente
e bastante libertária (para a época) fortemente envolvida no comércio do
mar Mediterrâneo. Durante seu auge nos séculos XII a XV, ele desenvolveu
muitas inovações comerciais, incluindo duas que examinaremos aqui, o
empréstimo de "troca seca" e o seguro de risco conjunto.

Aqui está uma cláusula de um contrato feito em Gênova em 23 de junho de
1271 d.C. Um homem está assinando uma obrigação feita por seu filho:

Portanto e pelos quais prometemos, nós dois (responsáveis) pelo valor
total, dar e pagar a você ou a seu mensageiro credenciado 53 hyperpers
[moeda de ouro bizantina] de ouro, bons e de peso correto, na Romênia
(Bizâncio), pelas calendas de Setembro. Se, no entanto, não lhe dermos
esses (hyperpers) dentro do prazo, (prometemos) para cada um dos
hyperpers 11 xelins [uma unidade monetária] genoveses em Gênova,
sempre que desejar. Caso contrário, prometemos, nós dois (responsáveis)
pelo valor total, dar a você, fazendo a estipulação, a penalidade do
dobro do referido valor, as (condições) acima mencionadas permanecendo
como liquidadas. E prometemos a você como garantia pelas supracitadas
(promessas) todos os nossos bens, existentes e futuros ...[^5]

Agora, este é um contrato muito inteligente, chamado pelos estudiosos de
"troca seca". A Igreja Católica proibiu a cobrança de juros, de modo que
um contrato de empréstimo que saísse diretamente e cobrasse juros seria
inexequível e exporia os redatores a outras sanções da Igreja. Mas tanto
as trocas de longa distância (negociando em um mercado distante em uma
data posterior -- geralmente através de uma viagem marítima, portanto
uma troca "úmida") quanto as de câmbio eram bastante legais, exequíveis
e comuns. O contrato acima combinou esses dois, juntamente com as
cláusulas de danos, de uma maneira inteligente. Nenhuma das partes acima
tinha intenção de viajar para Bizâncio, ou mesmo para fora de Gênova,
para cumprir este contrato. Sua lógica pode ser analisada da seguinte
forma (o titular é o credor). Adicionamos as declarações "in
(localização geográfica)", security e foreclose para destacar aspectos
importantes deste contrato. O último vende bens suficientes em leilão
para satisfazer a penalidade (se não houvesse o suficiente para
satisfazer os credores, havia um procedimento de falência para alocar de
maneira justa a segurança restante entre os credores, mas isso não é
mostrado):

```ruby
counterpartySecurity = pledge(allGoods(Counterparty))

also cosignerSecurity = pledge(allGoods(co-signer))

then

payment1() =

when beforeTime("Kalends of September 1275")

to Holder in Byzantium "53 hyperpers"

terminate

payment2() =

when breachedPerformance(payment1)

to Holder in Genoa "53*11 = 583 shillings"

terminate

payment3() =

when breachedPerformance(payment2)

to Holder in Genoa "2*583 shillings"

terminate

payment3() =

when breachedPerformance(payment3)

when choiceOf(Holder)

to Holder in Genoa foreclose(counterpartySecurity, penalty)

terminate

when choiceOf(Holder)

to Holder in Genoa foreclose(cosignerSecurity, penalty)

terminate

continue
```

Nenhuma das partes esperava que o pagamento1 fosse realizado. As
quantidades de hiperpers e xelins provavelmente refletiram com precisão
a taxa de câmbio entre as duas moedas na época -- não faz sentido ser
óbvio demais. Mas teria sido muito caro viajar para Bizâncio apenas para
fazer essa troca. Assim, de fato, ambas as partes esperavam que o
pagamento2, uma cláusula de dano falso, fosse normalmente executada.
Caso contrário, temos duas cláusulas de danos reais -- a "penalidade do
dobro" e o letal "todos os nossos bens, existentes e futuros". Outra
interpretação desta última cláusula é que ela se referiria apenas a um
valor de mercadorias até o valor da multa dupla, mas as mercadorias
poderiam ser escolhidas dentre todas as mercadorias do devedor e do
co-signatário. Certamente, um tribunal moderno consideraria a
interpretação que eu coloquei em nossa linguagem como inescrutável e,
portanto, inexequível.

Acima da parte que citamos, o contrato não especifica quanto era o
montante original do empréstimo -- os devedores simplesmente reconhecem
que receberam do credor "um número de denários genoveses" e depois
prometem outras moedas em troca, como citado acima. Portanto, um
investigador da Igreja não poderia provar, apenas lendo o contrato, que
qualquer juro foi cobrado. Quanto ao juiz genovês que arbitra uma
disputa, ele provavelmente seria a favor de empréstimos com juros e
ficaria feliz em piscar, acenar com a cabeça e interpretar o contrato
literalmente.

Os traders modernos de derivativos fazem isso o tempo todo, criando
ativos sintéticos ou combinações que imitam a funcionalidade financeira
de algum outro contrato, evitando suas limitações legais. Nossa
linguagem é ideal para redigir e analisar esses contratos.

## Seguro

Os primeiros contratos de seguro de agrupamento de riscos foram
estruturados de forma semelhante e executados sob os mesmos princípios
legais dos empréstimos. De fato, vamos começar com um empréstimo simples
para a compra de mercadorias sem juros, onde o Titular (o credor) pode
solicitar o empréstimo a qualquer momento entre os dias t1 e t2:

```ruby
loan(goods, principal, penalty, t1, t2) =

counterpartySecurity = pledge(allGoods(Counterparty))

with to Counterparty getTitle(goods)

loanPayment(principal, t1, t2)

with when breachedPerformance(loanPayment)

to Holder foreclose(counterpartySecurity, penalty)

loanPayment(principal, t1, t2) =

when withinPeriod(t1,t2)

when choiceOf(Holder)

to Holder principal
```

Vamos adicionar à nossa linguagem um evento safeArrival(goods) -- o
evento em que um navio que transporta goods [mercadorias] chega com
segurança no porto e os goods [mercadorias] são descarregados e
contabilizados. Agora, adicionando a este contrato de empréstimo apenas
uma linha extra, colocando um when safeArrival() e modificando levemente
algumas outras, podemos transformá-lo em um contrato de seguro marítimo.
O segurado é o Titular, a seguradora é a Contraparte. Para esta versão
simples, os danos são pagos em um valor fixo (principal) se safeArrival
não ocorrer:

```ruby
insureGoods(goodsPremium, principal, penalty, t1, t2, goodsInsured) =

counterpartySecurity = pledge(allGoods(Counterparty))

with to Counterparty getTitle(goodsPremium)

insurancePayment(goodsInsured, principal, t1, t2)

with when breachedPerformance(insurancePayment)

to Holder foreclose(counterpartySecurity, penalty)

insurancePayment(goodsInsured, principal, t1, t2) =

when safeArrival(goodsInsured) terminate

when withinPeriod(t1,t2)

when choiceOf(Holder)

to Holder principal
```

Aqui está um exemplo de um contrato de seguro antecipado desse tipo --
novamente em Gênova, o berço das modernas instituições comerciais. Pela
primeira vez, vemos uma pool [grupo] de seguradoras -- não uma, mas
muitas contrapartes, cada uma comprometendo sua propriedade inteira como
garantia. Muitas vezes, eram senhores feudais com grandes propriedades,
então o valor que poderia ser usado para apoiar esses contratos de
seguro era vasto. É assim que a Lloyds Names ainda funciona hoje. Como
vários Nomes apoiam um único contrato (por exemplo, cobrindo uma única
remessa de mercadorias, como aqui), cada Nome coloca apenas uma pequena
fração de seus bens em risco nessa viagem. Uma bolsa de seguros como a
Lloyds permite que os agentes de proprietários de mercadorias,
remetentes e Nomes atendam e produzam em massa esses tipos de contratos.

... Geri, [filho] do falecido Sor Lapo de Florença, Simone Guascone,
[[mais 9 nomes listados]], cada um deles
[[responsável]] pelo montante escrito abaixo, reconheceu
e, na verdade, me declarou, notário abaixo assinado, como funcionário
público [ocupando] um cargo público, estipulando e recebendo em nome e
em lugar de Federico Vivaldi, cidadão de Gênova, que eles compraram,
tiveram e receberam dele uma certa quantidade de bens do dito Frederico
... E por esses bens e considerando o preço que cada um deles prometeu
dar e pagar ao dito Frederico ou a seu mensageiro credenciado:
[[do]] dito Geri, 150 florins de ouro, do dito Simone, 50
florins, [[100 florins cada um dos outros Nomes]] nos
próximos cinco meses a partir de agora. Caso contrário, eles prometeram
dar e pagar ao referido Frederico a penalidade do dobro e de todo o
valor ao qual e na medida em que [[este acordo]] seja
violado ou não for observado como acima, juntamente com a restituição de
todas as perdas, lucros não realizados e despesas que possam ser
incorridas por causa dele em juízo ou fora dele -- o mencionado acima
permanecendo como liquidado e sob hipótese e penhor de seus bens e [[os
bens]] de qualquer um deles, existentes e futuros.

[[O acima exposto é obrigatório]], com exceção e reserva
especial de que, se a quantidade de bens, propriedades, e mercadorias
que foi carregada ou for carregada por Frederico Imperiale ou por outro
em seu nome, por conta do referido Frederico Vivaldi em Aigues -Mortes
-- a ser transportado para Ayassoluk e Rhodes ou para uma dessas duas
localidades em um determinado navio ... e que partiu de Aigues-Mortes ou
está prestes a partir para navegar para as regiões acima mencionadas --
é trazido e descarregado no localidades de Ayasoluk e Rhodes ou em
qualquer uma delas, em segurança, e nesse caso o presente instrumento é
cancelado, nulo e sem valor e proporcionalmente. E seja entendido que
esse risco começa quando o referido navio sai e zarpa de Aigues-Mortes,
e permanece e dura, enquanto o capitão vai, fica [[no
porto]], navega, carrega e descarrega, da referida
localidade de Aigues-Mortres até as localidades de Ayassoluk e Rhodes,
da maneira que desejar, até que a quantidade de bens, propriedades e
mercadorias seja trazida e descarregada em Ayassoluk e Rhodes ou em
qualquer uma dessas duas localidades em segurança, e proporcionalmente.
Que o presente instrumento também seja cancelado se o referido Frederico
se abster de solicitar pagamentos dos montantes mencionados em dinheiro
pelo espaço de um ano após o tempo ou o prazo decorrido para solicitar
ou obter seu pagamento ... Feito como acima, 15 de setembro, por volta
das nove [[horas]]. [[1393]
[d.C.]] [^6]

Ignorando a linguagem pro rata, a definição específica dos riscos que
impedem a geração ou não do evento safeArrival() e ignorando os vários
nomes (ou seja, tratando-os como uma Contraparte), o contrato pode ser
modelado pelo contrato de seguro que elaboramos acima com seus
parâmetros preenchidos da seguinte forma, e com Frederico Vivaldi como
segurado (o Titular):

```ruby
insureGoods(goodsPremium="a certain amount of goods",

principal="100 fl + 50 fl + 7*100 fl",

penalty=2*principal,

t1="5 months from now",

t2="1 year after [legal] time limit has expired"

goodsInsured="that amount of goods, property,

and merchandise which was loaded")
```

Esse contrato ainda era, legalmente falando, um empréstimo. Isso teve
pelo menos duas conseqüências interessantes sobre o que chamamos agora
de prêmio de seguro. Em primeiro lugar, o prêmio foi tratado como compra
de bens pela seguradora a crédito. Em segundo lugar, mesmo nessa data
tardia, os contratos eram modestos quanto ao valor real desses bens.
Deixar o valor desses bens não especificado dificultou a comprovação da
usura neste "empréstimo".

## Regras: Eventos Logicamente Combinados e Sobrepostos

Eventos em uma cláusula when podem ser combinados em condições lógicas
que devem ser avaliadas como true [verdadeiras] para acionar a
subcláusula. Isso pode ser usado para modelar cláusulas condicionais em
contratos e, mais amplamente, regras processuais e substantivas da lei.
Ao construir regras, chamamos os elementos primitivos de eventos. Por
exemplo, aqui é, seguindo aproximadamente a Reformulação (Segunda) de
Contratos, uma regra legal para o embargo promissório:

```ruby
when

"there is a promise"

P "has relied on that promise"

D "should reasonably expect P would rely on that promise" and

"injustice can only be remedied by enforcing the promise"

then

"the promise will be enforced"

else

"the promise will not be enforced"
```

Nós incluímos um "then" gratuito aqui para facilitar a leitura. Os
programadores de computador devem observar que estamos seguindo uma
abreviação usada aqui por advogados -- escrevemos a frase lógica (A e B
e C e D) como (A B C e D). Ao misturar e e ou, escreva a lógica completa
e use parênteses, quando apropriado.

Os elementos da regra, como "there is a promise" [existe uma
promessa], existem em um estado sobreposto. Por padrão, a lógica
desconhece os fatos e cada elemento está genuinamente em questão. Como
resultado, "there is a promise" e os outros elementos da regra acima são
verdadeiros e falsos, ao mesmo tempo. (Aqueles familiarizados com
mecânica quântica ou raciocínio jurídico sabem do que estou falando
aqui). No estado inicial, onde cada elemento está genuinamente em
questão, regras não triviais sempre serão avaliadas como verdadeiras e
falsas. Assim, ambas as cláusulas "promise will be enforced" [promessa
será aplicada] e "promise will not be enforced" [promessa não será
aplicada] serão acionadas. Quando as cláusulas são incompatíveis, como
essas parecem ser por seus rótulos, cabe ao implementador da cláusula
lidar com isso adequadamente. Nesse caso, tal cláusula deve ser tratada
apenas como aconselhamento até que todos os elementos materiais tenham
sido decididos -- ou seja, eles não estão mais genuinamente em questão,
quando a regra pode ser usada para tomar uma decisão, ou seja, acionar
uma única cláusula que toma uma ação consistente. Uma versão futura
deste documento descreverá como resolver elementos genuinamente em
questão em elementos não genuinamente em questão e, assim, decidir sobre
um único resultado ou curso de ação. Também descreverá como lidar com
cláusulas consultivas; por exemplo, para analisar quais elementos são
mais favoráveis ​​a um resultado ou outro. Finalmente, outro recurso
futuro incluirá elementos que abrangem uma faixa de valores numéricos,
em vez de apenas verdadeiro ou falso, e um "teste de equilíbrio"
formalizado que determina os resultados com base em estimativas
numéricas subjacentes.

## Propriedade -- Estados e Lucros Futuros

Nossa linguagem de regras é ideal para especificar propriedades e lucros
futuros em ações imobiliárias. Também se pode aplicar esses padrões a
outros tipos de propriedade, quando apropriado. Aqui estão alguns
exemplos:

Arrendamento por Prazo: (n.b. -- Concedente = o próprio). Este é um
contrato antigo de direito comum que realmente transfere o título por um
determinado período de tempo.

```ruby
leaseWithTerm(Property, Lessee, Start, Term) =

when afterTime(Start) to Lessee Property

then when afterTime(Start+Term) to Grantor Property
```

Life Estate with Reverter: (n.b. -- Concedente = self)

```ruby
lifeEstateReverter(Property, Grantee) =

to Grantee Property

then when afterDeath(Grantee)

to Grantor Property
```

Reversão Designável para Arrendamento. Para fazer com que os lucros
futuros sejam atribuíveis, defina-os separadamente. (Como sempre,
estamos vendo as coisas do lado do devedor):

```ruby
lifeEstateReverter(Property, Grantee) =

to Grantee Property

then when afterDeath(Grantee)

to Grantor Property
```

Agora podemos redefinir a locação de vida com reversão em termos dos
lucros futuros definidos separadamente:

```ruby
lifeEstateReverter(Property, Grantee, Reverter) =

to Grantee Property

then Reverter(Grantor, Grantee, Property)
```

Locação de Vida com Remanejo. A única diferença aqui é que a propriedade
é remanejada para terceiros em vez de reverter para o concedente.

```ruby
lifeEstateRemainder(Property, Grantee, Remainderman) =

to Grantee Property

then when afterDeath(Grantee) to Remainderman Property
```

Taxa Simples Determinável. A Condição pode ser qualquer evento
verificável ou mudança de estado da propriedade ou seu título. Uma
condição imobiliária comum, por exemplo, é "usada para fins comerciais"
-- isto é, uma restrição de que a propriedade não pode ser usada para
fins comerciais, caso contrário, o beneficiário é penalizado por perder
o título do concedente.

```ruby
feeSimpleDeterminable(Property, Grantee, Condition) =

to Grantee Property

then when Condtion(Property) to Grantor Property
```

Taxa Simples Sujeita a Limitação Executiva. O mesmo que Taxa Simples
Determinável, exceto que a propriedade é remanejada para terceiros em
vez de reverter para o concedente.

```ruby
feeSimpleSubjectToExecutoryLimitation(Property, Grantee, Condition, Remainderman) =

to Grantee Property

then when Condtion(Property) to Remainderman Property
```

Taxa Simples Sujeito a Condição Subseqüente. Aqui, o título não é
automaticamente transferido após a ocorrência da condição. Em vez disso,
o Concedente deve fazer algum ato afirmativo e verificável (neste
exemplo, "entrar" na propriedade), para recuperar o título.

```ruby
feeSimpleSubjectToConditionSubsequent(Property, Grantee, Condition, Enters) =

to Grantee Property

then when Condtion(Property)

when Enters(Grantor, Property) to Grantor Property
```

## Mais Alguns Exemplos Avançados

Nesta seção, examinaremos maneiras de construir acordos
multipartidários, distinguir eventos ambientais de lançados, e examinar
uma série de outros recursos mais avançados ou maneiras de usar nossa
linguagem.

Concluiremos o ciclo de vida da opção americana que elaboramos acima
"escrevendo" a opção -- criando-a a partir de uma security subjacente
rightA e vendendo-a por rightX. Aqui, o Titular (a mesma parte que o
Titular acima, neste caso a pessoa que comprará a opção por escrito)
primeiro verifica que a Contraparte realmente detém a security
subjacente (rightA) junto à Corretora. O Titular confia no Corretor para
garantir que a Contraparte continue mantendo o valor mobiliário até que
a opção seja exercida ou expirada. O contrato entre o Corretor e o
Titular é escrowRight ().)

Como a Contraparte, o criador da opção, não está pagando nada
antecipadamente por uma opção à rightB, esse direito não precisa ser
garantido.

```ruby
escrowRight(right, escrow, newHolder, currentHolder,

newHolderReleaseEvents, currentHolderReleaseEvents) =

to escrow right

then

when (holderReleaseEvents)

to rightHolder right then terminate

when (counterpartyReleaseEvents)

to currentHolder right then terminate

writeCallOptionAmerican(rightA, rightB, rightX, time) =

escrowRight(rightA, Holder, Counterparty,

(optionExercised), (optionExpired))

then

to Counterparty callOptionAmercian(rightA, rightB, time)

with to Holder rightX
```

Agora, reformulamos a opção em si para tirar proveito do escrow
[garantia]. rightA é transferido para o Titular pelo throw [lance]
após o exercício ou de volta à Contraparte se a opção expirar.

```ruby
callOptionAmerican(escrowRight, rightB, time) =

when beforeTime(time)

when choiceOf(Holder)

{ throw optionExercised at escrowRight }

with to Counterparty rightB

then terminate

when afterTime(time)

throw optionExpired at escrowRight

then terminate
```

Podemos pensar nos eventos como sendo de dois tipos. Os primeiros,
eventos ambientais, ocorrem espontaneamente no ambiente ou são gerados
por uma entidade externa à nossa especificação, como um usuário ou um
cronograma. O segundo, eventos lançados, são eventos que lançamos
explicitamente como acima.

Neste manual, expressei cláusulas contratuais em termos de direitos.
Freqüentemente, a linguagem do contrato é expressa em termos de
obrigações, o que pode ser feito como uma imagem espelhada --to Holder
right é o mesmo que from Counterparty obligation e vice-versa. Use from
para distinguir uma obrigação.

## Máquinas de Conexão

Mostrando ainda mais a flexibilidade de nossa linguagem, podemos
adicionar sensores e efetores, acrescentando "inteligência" a nossos
contratos e aumentando a aplicação legal com restrições tecnológicas.

Primeiro, esboçamos uma especificação para o comportamento de contrato
de uma máquina de venda automática:

```ruby
sellCandy(candyPrice = $0.90) =

variable moneyAmount = $0.00

then

# coins also fall into a temporary till tempTill

when (nickel)

add(moneyAmount, $0.05)

when (dime)

add(moneyAmount, $0.10)

when (quarter)

add(moneyAmount, $0.25)

when (moneyReturn)

dropCoins(tempTill, returnTill)

with moneyAmount = $0.00

when threshold(moneyAmount, candyPrice)

when (nickel | dime | quarter)

redirectNewCoinsTo(returnTill)

also display("ready to dispense -- please select candy")

then when (candySelection)

dropCandy(candyRacks, candySelection)

with dropCoins(tempTill, permTill)

with moneyAmount = $0.00

continue
```

Introduzimos aqui um novo recurso de linguagem, uma variável de estado.
Nossa variável de estado moneyAmount gera um evento ao ultrapassar o
limite de preço de doces de $0,90. Observe que nickel [moeda de 5
centavos], dime [moeda de 10 centavos], etc. são objetos físicos
reais que os sensores (gerando eventos "nickel", "dime" etc.) detectam e
tratam separadamente -- não são apenas quantias abstratas de dinheiro.

Variáveis de estado podem ser problemáticas e devem ser evitadas, a
menos que seja absolutamente necessário, como aqui. Esta é relativamente
inofensiva porque o slot de moedas tende a forçar as moedas a entrar uma
de cada vez, de modo que não há duas cláusulas tentando alterar a
variável de estado ao mesmo tempo. Mesmo se fossem, a operação de adição
é o que os matemáticos chamam de "comutativo", o que significa que não
importa em que ordem é feita. Mas se a operação na variável de estado
fosse mais complicada ou envolvesse certos outros tipos de operações,
não saberíamos se seria comutativo. A ordem em que os eventos ocorreram
e alteraram a variável de estado pode importar muito, e poderíamos ter
grandes problemas. Portanto, evite variáveis de estado sempre que
possível.

Para simplificar, deixamos de fazer troco- nossa máquina precisa ter um
desses sinais que você vê às vezes, "somente troco exato". Se o cliente
coloca uma moeda que empurra o valor de, por exemplo, $0,80 a $1,05 --
lamento, a máquina o come. Se o cliente colocar US $ 0,90 (ou mais) e
adicionar mais moedas, no entanto, a máquina retornará automaticamente
as moedas extras. A máquina também retornará tudo o que foi colocado no
caixa, se o cliente mudar de idéia e decidir não comprar o doce.
Exercício para o leitor: verifique por si mesmo que as descrições de
comportamento acima estão corretas conforme o código é escrito.

RedirectNewCoinsTo(returnTill) faz com que outras moedas caiam na rampa
de retorno em vez de no sensor que aciona os eventos acima. O leitor
deve aqui imaginar como é o mecanismo, pois parte do comportamento é
"codificada" em seu mecaninismo, e não explicitamente nesta afirmação.

Pense nos contratos e direitos aninhados como uma árvore invertida --
uma hierarquia de cláusulas aninhadas. Os eventos se propagam de cima
das "folhas" da árvore em direção à "raiz" no topo. Eles são pegos pelo
primeiro evento when que encontram para aquele evento. Nesse caso, uma
vez inserida a cláusula when threshold(), a cláusula when (nickel |
dime | quarter) substitui as cláusulas when (nickel) e assim por diante
acima delas.

Como uma perpetuidade, nossa máquina de venda automática não tem horário
ou condição agendada para a execução -- portanto, temos uma instrução
continue para substituir o implícito then terminate na última linha.

Infelizmente, nem eu nem os fabricantes de máquinas de doces do mundo
real temos nenhum código para resolver o caso em que os doces ficam
presos na máquina.

Acima está uma transcrição do comportamento da máquina. Agora,
tornaremos ainda mais como um contrato. Aqui, incorporamos o cliente e
suas escolhas, que geraram implicitamente os eventos das moedas no
código acima -- aqui as moedas são direitos do Titular. Pensar mais na
parte, e não na máquina, nos permite reconhecer que, a cada passo, o
cliente deseja feedback sobre quanto dinheiro investiu, assim, to
Counterparty display(moneyAmount). Essa exibição é feita pelo Titular (a
máquina de venda automática como um agente do fornecedor) como um
direito da Contraparte (o cliente). Para permitir uma melhor escolha do
cliente, adicionamos uma nova construção à nossa linguagem:
choiceOf(agent, right), que permite ao cliente várias opções, com base
no direito que ele deseja transferir para a contraparte do agente (aqui
a máquina de venda, o Detentor).

```ruby
sellCandy(candyPrice = $0.90) =

variable moneyAmount = $0.00

then

# coins also fall into a temporary till tempTill

when choiceOf(Counterparty, nickel)

to TempTill nickel

then to Counterparty add(moneyAmount, $0.05)

then to Counterparty display(moneyAmount)

when choiceOf(Counterparty, dime)

to TempTill dime

then to Counterparty add(moneyAmount, $0.10)

then to Counterparty display(moneyAmount)

when choiceOf(Counterparty, quarter)

to TempTill quarter

then to Counterparty add(moneyAmount, $0.25)

then to Counterparty display(moneyAmount)

when choiceOf(Counterparty, moneyReturn)

to Counterparty dropCoins(tempTill, returnTill)

with moneyAmount = $0.00

then to Counterparty display(moneyAmount)

when threshold(moneyAmount, candyPrice)

to Holder (nickel | dime | quarter)

to CounterParty redirectNewCoinsTo(returnTill)

also display("ready to dispense -- please select candy")

then when (candySelection)

to Counterparty dropCandy(candyRacks, candySelection)

with to PermanentTill dropCoins(TempTill)

with moneyAmount = $0.00

continue
```

Como é que especificamos o comportamento de uma máquina de venda
automática em uma linguagem projetada para a elaboração de contratos? As
moedas de 5, 10 e 25 centavos, e as operações como jogar moedas de uma
gaveta para outra podem ser pensadas como direitos e obrigações? Eu acho
que sim. Eles não são direitos e obrigações legais, com certeza. Não há
contrato explícito entre o fornecedor e os clientes da máquina de doces
e, se fosse o caso, provavelmente renunciaria à responsabilidade por
violar a maioria das cláusulas em nosso código. O que este código
descreve é o comportamento lógico e típico de uma máquina de venda
automática. Ele também reifica o entendimento implícito que muitos
clientes têm ao usar uma máquina de venda automática. Assim, ele modela
um "encontro de mentes" semelhante ao contrato entre o cliente e o
fornecedor, mediado pela máquina.

Aqui está uma facada na descrição formal do hipotético "auto repo auto".
O carro é controlado por um proplet e ele analisa os títulos de
propriedade para determinar a autoridade de propriedade. O proplet
permite que apenas o proprietário intitulado entre e conduza o carro.
"Titular" é o banco que fez o empréstimo e "Contraparte" é o novo
proprietário. Como acima, ignoramos o vendedor de carros; o banco
originalmente dono do carro. Este exemplo destaca a capacidade do idioma
de descrever sucintamente contratos, mas também sua incapacidade de
descrever a segurança real que aplicará o contrato. Obviamente, falta
muito aqui, incluindo os itens que faltam no contrato de empréstimo de
carro acima. Do ponto de vista de contratos inteligentes, a principal
coisa que falta é que não há nada para motivar o "Holder getTitle (car)"
no último when, nem qualquer maneira especificada aqui para aplicá-lo.
E, é claro, toda conexão entre propriedade e autoridade para entrar, dar
partida e dirigir o carro está aqui implícita -- o comportamento real do
proplet a esse respeito teria que levar em conta a segurança, o uso de
emergência, etc.

Durante todo esse trabalho, na verdade, apenas adicionamos uma cláusula
ao nosso contrato de compra de carro acima. A cláusula perde o título e
está estruturada como as cláusulas de dano que vimos. Um evento
breachedPerformance() é gerado se for detectado (pelo Titular, por um
auditor de terceiros ou pelo proplet) que a Counterparty falhou em
efetuar um pagamento de acordo com o cronograma especificado pelo loan
[empréstimo].

```ruby
loan(payment, schedule) =

for schedule

when withinPeriod(schedule.next)

payment

carPurchase(car, downPayment, monthlyPayment, schedule) =

to Counterparty getTitle(car) with to Holder downPayment

then

to Holder loan(monthlyPayment, schedule)

when breachedPerformance(loan)

to Holder getTitle(car)
```

## Nota Técnica -- Uma Sintaxe Legível por Computador

Aqui está uma especificação formal da gramática da linguagem em
"Backus-Naur Form" (BNF). A especificação é para uma versão planejada e
legível por computador da linguagem e existem algumas pequenas
diferenças, como o uso de colchetes {} em vez de guias para indicar o
aninhamento. O BNF é usado para definir o que os linguistas chamam de
"gramáticas sem contexto". Também é usado, como aqui, para definir a
sintaxe dos idiomas que os computadores também podem interpretar e
executar. Também incluo mais algumas discussões sobre os significados
das palavras e estruturas, especialmente sobre como o computador pode
interpretá-las. Como você pode ver, essa é uma linguagem em evolução, um
trabalho em andamento com muitos problemas não resolvidos. Suas
sugestões para alterar ou adicionar mais tipos de termos contratuais ao
nosso idioma são bem-vindas.

```ruby
agent = Holder | Counterparty

## faz com que o contrato pareça diferente em cada lado

period = (startTime,finishTime)

# period é a janela dentro da qual o desempenho deve ser

# executado, por exemplo uma opção europeia deve ser exercida

# entre o início e o fim do dia útil em que

# expira.

[for periodIterator "{" ...periodIterator.next... "}"] [then ... periodIterator.next...]*

# direitos executados em ordem temporal.

# sequência de períodos usados como entradas para a sequência de eventos withinPeriod(p).

# isso pode ser, mais geralmente, um iterador de eventos? mas os períodos têm

# uma ordem natural, enquanto outros tipos de eventos podem ocorrer em qualquer ordem.

# cada periodIterator.next gera um evento capturado pelo

# próximo tempral event (withinPeriod() se o iterador gerar

# períodos, aftertime() ou beforeTime() se gerar horas)

# *down [baixo]* do *for [para]*. O "lançamento" implícito ocorre em periodIterator.next

# para que ainda possamos vê-lo, apenas por pouco, como propagando

# o "lançamento".

# (isso é diferente da semântica normal de eventos em que lançamentos

# propagam *up [para cima]* na árvore de análise) -- devo alterá-lo para *up [cima]*

# e reescrever o código do iterador de agendamento acima? mas me confunde

# e talvez o comutador a colocá-lo *outside [fora]* do loop

event = choiceOf(agent) | withinPeriod(period) |

performed(right) | breachedPerformance(right) |

threshold(amount,threshold) | afterTime(time) | beforeTime(time)

right = throw event at [ contract | right] | passEvent([right | contract])

# gera um evento a ser capturado pelo contrato ou direito especificado.

# se contrato ou direito não for especificado, o primeiro when(event) parente

# é acionado.

right = throw event at [ contract | right] | passEvent([right | contract])

# gera um evento a ser capturado pelo contrato ou direito especificado.

# se contrato ou direito não for especificado, o primeiro when(event) parente

# é acionado.

# apenas use when withinPeriod (whenWritten, time)

# right = doBefore time {right}

# semanticamente equivalente:

# Holder right = O Counterparty obligation

right = getTitle(property)

# transferir título da propriedade do devedor para o credor

# consulte http://nakamotoinstitute.org/secure-property-titles/

right = null

right = [ when event "{" right "}" ]*

## visualize um "ponteiro de instruções" que

## segue aninhamento e eventos à medida que ocorrem.

## pode haver mais de um ponteiro de instrução

## se houver um "also [também]" ou dois eventos ocorrerem

## ao mesmo tempo, mas geralmente precisamos apenas pensar

## sobre um.

## uma cláusula está ativa ou inativa.

## quando uma cláusula when está ativa, ela está aguardando

## um evento ocorrer.

## quando o ponteiro da instrução está aninhado um when,

## when passa de inativo para espera.

## Uma série de when's no mesmo nível

## todos esperam que qualquer um deles seja acionado.

## Quando recebe um evento lançado abaixo

## dele, ou ele se torna ativo. Então

## as cláusulas abaixo dele se tornam ativas até

## os when's no nível abaixo. Os

## when's naquele nível vão de inativo

## para espera

## design alternativo sendo considerado: continue de onde parou

## a menos que [tenha] um "terminate" explícito no when

right = functionPerformance

## especificação funcional de um

## serviço específico vai aqui

## function sig, pre-, post-conditions

obligation = throw event at [contract | right]

# gera um evento a ser capturado pelo contrato ou direito especificado.

# se contrato ou direito não for especificado, o primeiro when parente

# é acionado.

# semanticamente equivalente: Holder obligation = Counterparty right

obligation = surrenderTitle(property)

# transferir o título da propriedade do devedor para o credor

# consulte http://nakamotoinstitute.org/secure-property-titles/

obligation = null

obligation = [ when event "{" obligation "}" ]*

## design alternativo sendo considerado: continue de onde parou

##, a menos que [tenha] um "terminate" explícito no when

obligation = functionPerformance

## especificação funcional de um

## serviço específico vai aqui

## function sig, pre-, post-conditions

contract = agent [right | obligation] ["with" agent [right | obligation]]*

## "with" permite compor Titular e Contraparte

## direitos vs. um ao outro

contract = [ when event "{" contract "}" ]*
```

## Funções Básicas

```ruby
doOn(right, period) =

when withinPeriod(p) { right }

# deve executar "right [direito]" dentro de (period [período])

# = obrigação com cupom zero = cupom

#

doOnDemand(right) =

when choiceOf(Holder) { right }

# deve executar o "right [direito]" a qualquer momento / sob demanda

#

doOn(contract, period) =

when withinPeriod(p) { contract }

# deve executar "contract [contrato]" dentro de (period [período])

#

doOnDemand(contract) =

when choiceOf(Holder) { contract }

# deve executar "contract [contrato]" a qualquer momento / sob demanda

#
```

## Mais Exemplos

```ruby
future(rightA, rightB, p) =

Holder doOn(rightA, p) with Counterparty doOn(rightB, p)

#

# [restrição adicional p = p não é mera composição algébrica]

callOptionAmerican(rightA, rightB, t) =

when withinPeriod(whenWritten, t)

when choiceOf(Holder)

Holder rightA with Counterparty rightB

#

callOptionEuro(rightA, rightB, p) =

when choiceOf(Holder)

Holder doOn(rightA, p)

with Counterparty doOn(rightB, p))

#

putOptionAmerican(rightA,rightB,t) =

when withinPeriod(whenWritten, t)

when choiceOf(Holder)

Holder rightA with Counterparty rightB

# semântica de eventos precisa armazenar choiceOf até

# ao esperar o próximo when

putOptionEuro(rightA,rightB,p) =

when choiceOf(Holder)

Holder doOn(rightB, p)

with Counterparty doOn(rightA, p))

#

note(right) = demandDeposit(right) =

Holder doOnDemand(right)

# [distinção entre portador e titular da conta não

# foi introduzido]

#

zeroCouponBond(right,p) = doOn(right, p)

#

callableZeroCouponBond(right,p) =

when choiceOf(Holder) { right }

when withinPeriod(p) { right }

#

bond(coupon, principal, schedule) =

for schedule {

doOn(coupon, schedule.next)

} then

doOn(principal, schedule.next)

bond(coupon, principal, schedule) =

for schedule {

doOn(coupon, schedule.next)

} then

doOn(principal, schedule.next)
```

## Perguntas Frequentes

**P: Já existem linguagem para especificar contratos
financeiros**[^7]**, qual é a novidade aqui?**

R: Essa é a primeira linguagem de especificação a generalizar estruturas
contratuais para qualquer tipo de direitos exclusivos, não apenas para
dinheiro. Esse também é a primeira linguagem que incorpora a natureza
dinâmica de muitos contratos (sua dependência de tempo ou eventos) de
maneira sucinta, completa e potencialmente executável.
Surpreendentemente, isso geralmente torna a especificação mais, não
menos, sucinta.

**P: Onde está o dinheiro?**

R: Essa linguagem é direcionada para uma economia de software e
dispositivos distribuídos que executam serviços um para o outro. Uma
economia monetária pode ser construída a partir de uma economia de
troca, mas não vice-versa. O dinheiro online real é muito mais sutil do
que uma mera variável compartilhada (ou mesmo a especificação de "notas
de banco" nessa linguagem). O dinheiro é apenas um tipo de direito
exclusivo fungível, e a estrutura dos contratos financeiros é
generalizada pela conversão de termos monetários em qualquer direito
exclusivo fungível.

**P: Que suposições você está fazendo?**

R: Essa é a pergunta mais importante a ser feita em qualquer novo
esquema! Eu identifiquei pelo menos as seguintes:

1.  Por enquanto, estou presumindo que questões de proteção e execução
    de desempenho foram abordadas em outros lugares
    (http://szabo.vwh.best.com/ tem muitos ensaios que enfocam esse
    tópico). Um objetivo final é criar protocolos para reforçar os
    átomos da linguagem e depois compor esses átomos mantendo a
    aplicabilidade.

5.  Duas premissas específicas de execução -- existe uma fonte de tempo
    acordada e segura, e a ocorrência de outros eventos definidos pode
    ser acordada pelas partes e/ou auditada por terceiros.

6.  Estou assumindo algum tipo de atomicidade para cada desempenho do
    átomo correto -- por exemplo, quando um evento aciona um "when", um
    functionPerformance em outro thread é suavemente revertido ou
    concluído.

7.  Existem apenas duas partes no contrato, o Titular e a Contraparte.

8.  Um contrato vem em duas formas de espelho, uma das quais pode ser
    deduzida da outra. Uma parte sempre se vê como o Titular. As
    obrigações do Titular sempre podem ser expressas e inferidas a
    partir dos direitos da Contraparte e vice-versa.

9.  Provavelmente estou fazendo outras suposições que ainda não descobri
    -- se você encontrar alguma, por favor me avise!

**P: Quais são alguns dos problemas dessa linguagem que você gostaria
que fossem resolvidos?**

R: Implementações que satisfazem as premissas acima para os átomos de
linguagem específicos e também para composições dos átomos. (Obviamente,
vários protocolos no campo "criptografia financeira", em minhas próprias
propostas, na linguagem E, etc. fornecem muitos blocos de construção
valiosos para essas soluções).

[^1]: Existem muitos casos de negócios que azedaram no último minuto,
    quando os vendedores consultam o departamento jurídico e descobrem
    que o negócio não é possível devido a uma cláusula em outro contrato
    -- por exemplo, uma promessa de não vender aos concorrentes de um
    cliente em um setor por um certo período. Pior, esse conflito não
    pode ser descoberto até que o compromisso contraditório tenha sido
    feito.

[^2]: A Linguagem de Programação E

[^3]: Proceedings of the Financial Cryptography Conferences,
    Springer-Verlag

[^4]: Composing contracts: an adventure in financial engineering -- Um
    tipo diferente de linguagem para especificar contratos financeiros,
    a fim de calcular seu risco e valor

[^5]: Lopez and Raymond, Medieval Trade in the Mediterranean World:
    Illustrative Documents, Columbia University Press 2001.

[^6]: Lopez and Raymond, Medieval Trade in the Mediterranean World:
    Illustrative Documents, Columbia University Press 2001.

[^7]: Proceedings of the Financial Cryptography Conferences,
    Springer-Verlag

---
Fonte:  
[nakamotoinstitute](https://nakamotoinstitute.org/contract-language/)
[bitnoticias](https://bitnoticias.com.br/o-evangelho-de-satoshi-nakamoto-cap-33-vers-1/)