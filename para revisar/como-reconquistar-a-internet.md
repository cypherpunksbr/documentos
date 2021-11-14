---
title:  "Como podemos reconquistar a Internet criando internets em letra minúscula"
date:   2020-11-11
author:
  - Tech Learning Collective
categories:
  - Artigo
tags:
  - internet  
  - tecnologia
  - liberdade
---
```
Traduzido por: Iann Zorkot
Revisado por: C4SS, Instituto Ágora, Cypherpunks Brasil
```

# Como podemos reconquistar a Internet criando internets em letra minúscula
## Tech Learning Collective
===exibe no card daqui pra baixo===

Em abril de 2001, cinco meses antes do 11 de setembro, Bram Cohen começou a projetar um novo protocolo de compartilhamento de arquivos que mudaria quase sozinho a face das indústrias de música, TV e cinema nas próximas duas décadas. A tecnologia em si não era uma ideia completamente nova. Afinal, tecnologias semelhantes, como o conhecido File Transfer Protocol (FTP), já haviam sido projetadas e implantadas para copiar arquivos entre computadores. O que o tornou tão potente foi a maneira como ele refletiu a estrutura orgânica fraturada de seu meio subjacente, a própria Internet.

Em vez de tratar cada arquivo como um único todo indivisível, essa nova tecnologia separou cada arquivo em um conjunto de peças de tamanhos semelhantes e tratou cada peça independentemente de qualquer outra. Ao contrário das tecnologias cliente-servidor anteriores, como o FTP, esta nova tecnologia “ponto a ponto” poderia recuperar qualquer parte do todo de qualquer outro ponto que já tivesse uma cópia dessa parte, mesmo que esse ponto não tivesse todas as partes como um servidor tradicional faria.

Essa nova tecnologia foi chamada de BitTorrent, e sua tecnologia de transferência de arquivos segmentados é, até hoje, a ruína de guardiões corporativos como a Record Industry Association of America (RIAA) e a Motion Picture Association of America (MPAA). O BitTorrent teve sucesso porque espelhou a natureza descentralizada da rede na qual foi implantado, a Internet. O BitTorrent e a Internet são tecnologias que não requerem nenhuma permissão especial ou produto para se conectar, interoperar ou estender. Se você tiver um computador executando um sistema operacional com uma pilha de software TCP / IP instalada, como qualquer Windows, macOS ou distribuições GNU / Linux modernos, poderá ampliar a Internet. Tudo o que você precisa fazer é conectar seu computador a outro computador já pré-conectado a ela.

Ainda podemos aprender com o sucesso do BitTorrent vinte anos depois? Se quisermos aceitar a “oferta de liberdade da Internet”, como previsto por gerações anteriores otimistas, devemos (re) aprender esta lição vital: a Internet é tangencial. Precisamos apenas criar uma internet.

A Internet (com I maiúsculo) é o nome de uma rede específica. A Internet “hospeda” computadores com nomes como Google, Facebook e Wall Street Journal. Em contraste, a palavra internet (com i minúsculo) descreve qualquer rede de redes interconectadas. Uma internet pode hospedar tudo.

Essa distinção é absolutamente crítica. Para conectar seu computador à Internet, você deve desembolsar moeda fiduciária para uma empresa como a Comcast, Verizon ou Rogers. Existem, no entanto, muitas internet às quais você pode se conectar gratuitamente, como o Guifi na Espanha ou o NYCMesh aqui na cidade de Nova York. Ao contrário da Internet, você pode até criar uma nova internet por conta própria, opcionalmente conectando-a a qualquer outra internet que deseje e possa se conectar a você.

Antes da Internet ser A Internet, ela era simplesmente uma internet. Para reconquistar a Internet das forças da industrialização que sufocam a promessa de liberdade online, devemos nos concentrar primeiro na construção de novas internets: devemos quebrar a Internet e nosso entendimento dela em pedaços, assim como os arquivos segmentados do BitTorrent, para que possamos colaborativamente reconstruí-la e, no processo, ameaçar o literal percentual de mercado e o metafórico percentual de mentes que esses monopólios atualmente têm sobre nós.

O que é preciso para construir uma internet? Precisamos de computadores, é claro, mas não especialmente poderosos ou caros. Como o Homebrew Server Club explica, “laptops pessoais são bons servidores caseiros, pois estão amplamente disponíveis, são relativamente poderosos e economizam energia”. Conecte dois laptops usando um cabo Ethernet comum (RJ-45) e você terá o início de uma internet. Adicione um terceiro laptop, ou talvez um Raspberry Pi, e você poderá executar um serviço dedicado, como um site da Web ou um catálogo de endereços ou calendário compartilhado. Você pode até criar uma conexão Wi-Fi para clientes em roaming (talvez sua nova internet minúscula esteja em um infoshop*), tudo sem nunca se conectar à Internet propriamente.

Em seguida, precisamos de imaginação. Sua internet pode ser pequena agora, mas pode crescer, assim como a internet original cresceu e se tornou A Internet que conhecemos hoje. Talvez você publique um site de poesia de resistência como parte de uma coleção de e-books (afinal, você está em um infoshop) e seus vizinhos despertos também queiram navegar pela coleção. Obtenha outro cabo Ethernet e conecte-os, sem necessidade de cartão de crédito.

Já existem internets como essas. Mencionamos o Guifi na Espanha e o NYC Mesh na cidade de Nova York, mas também há bolsões menores de internets em escala de bairro que oferecem serviços locais exatamente dessa maneira. Alguns até mesmo se conectam de volta à Internet (como o NYCMesh faz), para que possam oferecer simultaneamente serviços apenas locais, bem como acesso à Internet mais tradicional. Uma maneira de pensar sobre esses bolsões de computadores interconectados é a mesma que você pensaria sobre os vários computadores conectados à rede Wi-Fi em sua casa: você só paga por uma conexão, mas pode conectar centenas, se não mais, computadores naquela conexão ao mesmo tempo.

As tecnologias de interligação de redes, como o BitTorrent, são construídas na noção de partes menores, cada uma delas segmentos endereçáveis individualmente, que podem ser compostas juntas para criar um todo maior. Nem a Internet nem as transferências de arquivos BitTorrent são monólitos de fato. Isso significa que não precisamos da permissão de qualquer pessoa ou empresa, chave de licença ou produto comercial para criar o nosso próprio, para interconectá-los aos nossos pares e para executar e manter serviços úteis para eles. Já passou da hora de pararmos de pedir ou pagar pela permissão para construir o mundo em que queremos viver.

E se você morar longe do infoshop radical do nosso exemplo acima? Acontece que criar novas internets não é uma dicotomia, nem um jogo de soma zero. As internets que estão fisicamente distantes uma da outra ainda podem pegar carona com segurança em uma conexão de Internet – com I maiúsculo – existente para se unir usando as tecnologias de rede Virtual Private Network (VPN) e / ou Tor (serviço Onion). Novamente, é exatamente assim que partes fisicamente desarticuladas de redes pertencentes à comunidade e operadas de forma cooperativa, como aquelas que mencionamos anteriormente, são reconectadas. Una um número suficiente de internets operadas individualmente – isto é, passe outro cabo Ethernet para o próximo prédio, e o próximo, e o próximo – e teremos uma “Internet” recém-criada para rivalizar com a atual. Exceto que, desta vez, nós a possuiremos completamente, em vez de alugar o acesso a ela.

O fluxo de dados por links de telecomunicações é muito parecido com o fluxo de eletricidade por um fio ou água por um cano, não apenas em sua mecânica técnica, mas também em suas dependências humanas. A rede elétrica não poderia existir sem eletricistas. Água corrente em seu apartamento não seria possível sem encanadores competentes. Administradores de sistemas e engenheiros de rede - não programadores, bootcamps de código ou iniciativas de diversidade Big Tech – são necessários para criar e manter internets independentes como descrevemos aqui. Além disso, são esses componentes mais infraestruturais da autonomia das telecomunicações os primeiros pré-requisitos que devemos tomar para reconquistar a Internet de seus senhores corporativos e governamentais. Dito de outra forma, há muitos programadores mas não administradores de sistemas o suficiente, precisamente porque mais programadores são o que as corporações precisam no capitalismo, mas mais administradores de sistemas são o que as comunidades revolucionárias precisam para um futuro justo e equitativo.

É por isso que os esforços radicais de educação em tecnologia, como os do Tech Learning Collective, se concentram na infraestrutura em vez do código, onde os alunos aprendem habilidades de interligação de redes fundamentais esquecidas pelos “programas de corrida ao emprego” de várias “escolas de preparação para a corporação”. É por isso que projetos como a Shift-CTRL Space Library, que oferece uma coleção pré-empacotada de software para compartilhar mais facilmente coleções de e-books (PDFs, zines e mais), são construídos usando Software Livre amplamente disponível e independente de acesso à Internet – com I maiúsculo – como é tradicionalmente.

Já temos o poder, os materiais e o motivo para lutar e reconquistar a Internet. Mas não podemos começar pela última etapa, a construção de (ainda mais) aplicativos “novos”. Temos que começar com a primeira etapa primeiro: possuir nossa própria infraestrutura.

**Nota do Tradutor:**

* Infoshop é uma vitrina, banca ou centro social que serve como ponto de distribuição de informação anarquista, tipicamente na forma de livros, zines, adesivos e cartazes. Infoshops também servem como espaços de encontro e distribuição de recursos para grupos ativistas locais (Fonte: Wikipedia).

Fonte: [How we can win back the Internet by creating lowercase internets](https://c4ss.org/content/53903)