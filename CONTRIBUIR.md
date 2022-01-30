# Contribua com o Projeto

## Contribuição em código aberto usando Github
No Github você só pode alterar projetos que você mesmo tenha criado, ou seja, somente os repositórios que estiverem em ```github.com/seu-nome-de-usuário/nome-do-seu-projeto``` poderão ser alterados diretamente por você. De qualquer forma, isso não te impede de enviar contribuições para projetos criados por outras pessoas. Por exemplo, para contribuir com o nosso projeto, em vez de ir até o repositório original ```github.com/cypherpunksbr/documentos```, você precisará:

1. Fazer uma cópia (Fork) desse repositório
   * Após o Fork, você terá uma cópia exata do repositório original ```github.com/cypherpunksbr/documentos``` que estará em ```github.com/seu-nome-de-usuário/documentos```

2. Criar uma "área de trabalho" (Branch) para fazer suas alterações

3. Fazer as alterações **na sua cópia** ```github.com/seu-nome-de-usuário/documentos``` e **dentro da branch** criada no passo anterior

4. "Enviar" suas alterações através de uma Pull Request (PR)

[Tutorial completo de como executar cada um desses passos diretamente pelo site do Github]

## Como ajudar o projeto Cypherpunks Brasil?

### Existem diversas formas de contribuir com nosso projeto. Vamos listar algumas:

- [Adicionando novos Documentos](#add-new-docs)
- [Traduzindo Documentos para Português (pt-br)](#translate-docs-ptbr)
- [Revisando e corrigindo Documentos já traduzidos](#review-translation)
- Melhorando ou criando tutoriais sobre qualquer assunto relacionado ao movimento cypherpunk
- [Melhorando nosso site cypherpunks.com.br](#website-improvements)
<!-- - Fazendo doações em criptomoedas ou outras formas de valor -->
- [Iniciando, liderando ou auxiliando a criação de novos projetos](#start-new-projects)
- [Divulgando o projeto Cypherpunks Brasil](#spread-the-word)

---

<div id='add-new-docs'/>

## Adicionando novos Documentos à biblioteca

Você pode adicionar qualquer tipo de documento relacionado ao movimento cypherpunk à nossa biblioteca

### Mão na massa:
> Dica: algumas palavras contém links que te levam a uma explicação de como fazer

**1.** Faça um [Fork](wiki/GITHUB-BROWSER.md#criando-um-fork) do nosso repositório no github.

**2.** Dentro de seu Fork, crie uma **nova** [Branch](wiki/GITHUB-BROWSER.md#criando-uma-nova-branch) com um nome que especifique o objetivo. Por exemplo ```adiciona-bitcoin-whitepaper```. Após criar essa branch, é dentro dela que você irá trabalhar.

**3.** Encontre o documento que deseja traduzir na internet, em livros, qualquer lugar, ou escreva você mesmo um texto autoral. Salve as informações importantes (link para a página web, nome do livro, autor, data de publicação), elas serão usadas nas próximas etapas.
O documento pode estar em qualquer idioma, incluindo o português (pt-br).

**4.** No seu fork, dentro da branch criada, salve o documento em um arquivo único de texto com extensão ```.md``` (Markdown). Se for um documento em língua estrangeira, salve-o na pasta ```/para traduzir/```. Se for um documento em Português (pt-br), salve-o na pasta ```/para revisar/```. Caso o documento contenha imagens ou outros arquivos adicionais, salve esses arquivos na pasta ```/stuff/```. No futuro você irá referenciar esses arquivos usando markdown caso necessário.

**5.** Formate o documento para seguir o padrão dos textos publicados. Formate o texto usando o padrão de sintaxe [```Markdown```](luong-komorebi/Markdown-Tutorial/blob/master/README_pt-BR.md). Tome cuidado para não esquecer de formatar nada, reconstrua as referências de links que estão no site, palavras em itálico, citações, parágrafos, imagens, tudo! Isso precisa estar muito bem feito para que quem venha a traduzir e ler o documento não fique com um texto mal formatado.

**6.** Adicione nosso cabeçalho. Esse cabeçalho serve para que nosso site (feito com [Hugo]) reconheça informações importantes e agregue isso na exibição ao leitor. Adicione o cabeçalho a seguir no início do documento, alterando as informações pelas informações do seu texto. Caso alguma das informações exigidas não faça sentido para o caso do seu documento, apague a linha:

```
---
title:  "Título do seu Documento aqui" com aspas
date:   data da publicação no formato dia-mês-ano (exemplo: 31-10-2008) sem aspas
categories:
   -  Artigo
author:
  -
tags:
  - tag util 1 sem aspas
  - tag util 2 sem aspas
  - tag util 3 sem aspas
---
```

**7.** Após ter feito isso seu documento está organizado e pronto para ser incluído no repositório raiz do projeto no GitHub. Para incluí-lo é necessário realizar um [Pull Request (PR)](wiki/GITHUB-BROWSER.md#criando-um-pull-request) da sua branch para a branch main do repositório raiz, exemplo: ```cypherpunksbr/documentos|main``` ```<--``` ```seu-nome-de-usuário/documentos|adiciona-bitcoin-whitepaper```. Após ter feito o PR, aguarde um dos membros da organização revisar suas alterações e aprovar seu trabalho. Obrigado por colaborar com o projeto!

---

<div id='translate-docs-ptbr'/>

## Traduzindo Documentos para Português (pt-br)

Você pode traduzir qualquer documento presente na pasta [```/para traduzir/```](para%20traduzir/) ou então caso queira traduzir um documento que não está nessa pasta você pode primeiro [adicionar novos Documentos à biblioteca](#add-new-docs)

### Mão na massa:
> Dica: algumas palavras contém links que te levam a uma explicação de como fazer

**1.** Faça um [Fork](wiki/GITHUB-BROWSER.md#criando-um-fork) do nosso repositório no github.

**2.** Dentro de seu fork, crie uma **nova** [Branch](wiki/GITHUB-BROWSER.md#criando-uma-nova-branch) com um nome que especifique o objetivo. Por exemplo ```traduz-bitcoin-whitepaper```. Após criar essa branch, é dentro dela que você irá trabalhar.

**3.** Encontre o documento que deseja traduzir dentro da pasta [```/para traduzir/```](para%20traduzir/). É nessa pasta que estão os documentos que aguardam tradução.

**4.** [Mova](wiki/GITHUB-BROWSER.md#renomeando-e-movendo-arquivos) o arquivo para a pasta correta. Antes de começar a traduzir é necessário que você sinalize para todos que você está traduzindo esse texto para que não aconteça de duas pessoas ao mesmo tempo estarem traduzindo a mesma coisa, gerando ineficiência e trabalho jogado fora. Para sinalizar a intenção de tradução você deve mover o arquivo do seu documento que está na pasta [```/para traduzir/```](para%20traduzir/) para a pasta [```/sendo traduzidos/```](sendo%20traduzidos/).

**5.** No passo anterior você moveu o documento apenas na sua cópia (fork) do projeto. Agora para mover no repositório original você precisa abrir um [Pull Request (PR)](wiki/GITHUB-BROWSER.md#criando-um-pull-request) da sua branch para a branch main do repositório raiz, exemplo: ```cypherpunksbr/documentos|main``` ```<--``` ```seu-nome-de-usuário/documentos|adiciona-bitcoin-whitepaper```. Após ter feito o PR, aguarde um dos membros da organização aprovar. Assim que aprovado você pode ir para o próximo passo.

**6.** Hora de traduzir o documento! A branch que você criou anteriormente continua no seu fork e é por lá que você continuará trabalhando. Encontre seu documento que está em ```/sendo traduzidos/dd-mm-aaaa-nome-do-seu-documento.md``` e faça a tradução. Entenda:
- Você pode usar ferramentas para agilizar a tradução como por exemplo Google Translate, mas tais ferramentas as vezes alteram a formatação e o sentido dos textos, tiram expressões de contexto, erram termos técnicos, etc. Portanto você precisará revisar bem o texto caso decida usá-las;
- Não quebre a formatação do documento. Usamos o padrão de sintaxe [```Markdown```](luong-komorebi/Markdown-Tutorial/blob/master/README_pt-BR.md) com a adição de um cabeçalho no inicio do texto que orienta nosso site a classificar os documentos;
- Algumas palavras não exigem tradução pois são tão difundidas como a forma original até mais do que a tradução, como por exemplo "blockchain". Nesses casos coloque a palavra seguida pela tradução entre parêntesis, depois use apenas a palavra original caso ache mais adequado;
- Caso não saiba qual a melhor traducão para um trecho de texto peça ajuda. Você pode fazer isso pedindo para um amigo, abrindo uma [Issue](wiki/GITHUB-BROWSER.md#abrindo-uma-issue) no github ou perguntando em nosso [grupo no telegram](https://t.me/criptologia);
- Se você traduziu um pedaço do trecho mas só vai poder continuar em outro momento, não tem problema, faça Commit da alteração ou salve o que já traduziu em outro local para poder continuar de onde parou
- Faça um bom trabalho. Saiba que você está ajudando outras pessoas a terem acesso facilitado a informação de qualidade e preservando/difundindo um pedaço da história para outro idioma.

**7.** [Mova](wiki/GITHUB-BROWSER.md#renomeando-e-movendo-arquivos) novamente o documento de pasta. Agora você já finalizou a tradução e irá mover o documento para a pasta de revisão. Para isso você deve mover o arquivo do seu documento que está na pasta [```/sendo traduzidos/```](sendo%20traduzidos/) para a pasta [```/para revisar/```](para%20revisar/)

**8.** Após mover no seu repositório, hora de replicar essa mudança no repositório original fazendo mais um [Pull Request (PR)](wiki/GITHUB-BROWSER.md#criando-um-pull-request) da sua branch para a branch main do repositório raiz assim como foi feito anteriormente, exemplo: ```cypherpunksbr/documentos|main``` ```<--``` ```seu-nome-de-usuário/documentos|traduz-bitcoin-whitepaper```. Após ter feito o PR, aguarde um dos membros da organização revisar suas alterações e aprovar seu trabalho. Obrigado por colaborar com o projeto!

---

<div id='review-translation'/>

## Revisando e corrigindo Documentos já traduzidos

Você pode revisar um documento que já esteja traduzido e disponível na pasta [```/para revisar/```](para%20revisar) ou que já possua pelo menos uma revisão na pasta [```/sendo revisados/```](sendo%20revisados).

### Mão na massa:

> Dica: algumas palavras contém links que te levam a uma explicação de como fazer

**1.** Faça uma cópia ([Fork](wiki/GITHUB-BROWSER.md#criando-um-fork)) do nosso repositório no Github.

**2.** Dentro de seu Fork (```github.com/seu-nome-de-usuário/documentos```), crie uma **nova** [Branch](wiki/GITHUB-BROWSER.md#criando-uma-nova-branch) com um nome que espeficique o objetivo. Por exemplo: ```revisa-bitcoin-whitepaper```.

**3.** Encontre o documento que deseja revisar na pasta [```/para revisar/```](para%20revisar). Caso este documento já possua pelo menos uma revisão, ele deverá estar na pasta [```/sendo revisados/```](sendo%20revisados).

> Diferentemente do processo de tradução, o processo de revisão acontece mais de uma vez. Sendo assim, se você deseja revisar um documento que ainda está em [```/para revisar/```](para%20revisar/), primeiro você deve [move-lo](wiki/GITHUB-BROWSER.md#renomeando-e-movendo-arquivos) para a pasta [```/sendo revisados/```](sendo%20revisados/) e fazer uma [Pull Request (PR)](wiki/GITHUB-BROWSER.md#criando-um-pull-request). Caso já exista pelo menos uma revisão deste documento, alguém já o terá movido, então ele deverá estar na pasta [```/sendo revisados/```](sendo%20revisados/)

**4.** Na pasta correta, clique no nome do documento escolhido e habilite o modo de edição do Github clicando no lápis :pencil2: (canto superior direito da tela)

**5.** Faça as alterações que achar necessárias

**6.** Terminou sua revisão? Agora você pode começar a PR!
> Não se esqueça de seguir o passo a passo corretamente, escrevendo uma boa mensagem de commit e conferindo se está "enviando" as alterações da sua Branch para a Branch principal do repositório raiz. ex.: ```cypherpunksbr/documentos|main``` ``` <-- ``` ```seu-nome-de-usuário/documentos|revisa-bitcoin-whitepaper```

---

<!--
<div id='add-tutorials'/>

## Melhorando ou criando tutoriais sobre qualquer assunto relacionado ao movimento cypherpunk

### Mão na massa:
> Dica: algumas palavras contém links que se você clicar nelas você será levado a uma explicação de como fazer

**1.** Faça um [Fork](wiki/GITHUB-BROWSER.md#criando-um-fork) do nosso repositório no github.

**2.** Dentro de seu Fork, crie uma **nova** [Branch](wiki/GITHUB-BROWSER.md#criando-uma-nova-branch) com um nome que especifique o objetivo. Por exemplo ```adiciona-tutorial-pgp```. Após criar essa branch, é dentro dela que você irá trabalhar.

---

-->

<div id='website-improvements'/>

## Melhorando nosso site

Quer ajudar a melhorar o [cypherpunks.com.br](https://cypherpunks.com.br/)?

**1.** Vá até o nosso [repositório no Github](https://github.com/cypherpunksbr/cypherpunks.com.br).

**2.** Faça o [Fork](wiki/GITHUB-BROWSER.md#criando-um-fork).

**3.** Dentro de seu Fork, crie uma **nova** [Branch](wiki/GITHUB-BROWSER.md#criando-uma-nova-branch) com um nome que especifique o objetivo. Por exemplo ```corrige-link-quebrado```.

**4.** Faça o [Pull Request (PR)](wiki/GITHUB-BROWSER.md#criando-um-pull-request).

> Não se esqueça de seguir o passo a passo corretamente, escrevendo uma boa mensagem de commit e conferindo se está "enviando" as alterações da sua Branch para a Branch principal do repositório raiz. ex.: ```cypherpunksbr/documentos|main``` ``` <-- ``` ```seu-nome-de-usuário/documentos|corrige-link-quebrado```

---

<!-- - Usando os produtos da [nossa loja](LINK) -->

---

<!--
<div id='donate'/>

## Fazendo doações em criptomoedas ou outras formas de valor

---

-->

<div id='start-new-projects'/>

## Crie novos projetos
Está inspirado? Iniciar um projeto do zero poderia ajudar a tornar o movimento cypherpunk ainda mais forte e descentralizado! Caso tenha alguma boa ideia que possa ajudar pessoas a se libertar por meio da criptologia, não hesite em colocar isso em prática. Inicie agora mesmo seu projeto de liberdade e conte sempre com o nosso apoio.

---

<div id='spread-the-word'/>

## Divulgue nosso projeto

[![Facebook](/wiki/img/facebook.svg "Facebook")][8] [![Twitter](/wiki/img/twitter.svg "Twitter")][7] [![Instagram](/wiki/img/instagram.svg "Instagram")][6] [![Youtube](/wiki/img/youtube.svg "Youtube")][5] [![RSS](/wiki/img/rss.svg "RSS")][4] [![Odysee](/wiki/img/odysee.svg "Odysee")][3] [![Telegram](/wiki/img/telegram.svg "Telegram")][2] [![Cypherpunks Website](/wiki/img/website.svg "Cypherpunks Website")][1]




<!-- LINKS LIST -->

[Branch]:wiki/GITHUB-BROWSER.md#criando-uma-nova-branch
[Fork]:wiki/GITHUB-BROWSER.md#criando-um-fork
[Pull Request (PR)]:wiki/GITHUB-BROWSER.md#criando-um-pull-request
[documentação oficial do Github]:https://docs.github.com/en/repositories/working-with-files
[Criando um fork]:wiki/GITHUB-BROWSER.md#criando-um-fork
[Criando uma nova Branch]:wiki/GITHUB-BROWSER.md#criando-uma-nova-branch
[Renomeando e movendo arquivos]:wiki/GITHUB-BROWSER.md#renomeando-e-movendo-arquivos
[Criando um Pull Request]:wiki/GITHUB-BROWSER.md#criando-um-pull-request
[Abrindo uma Issue]:wiki/GITHUB-BROWSER.md#abrindo-uma-issue
[Tutorial completo de como executar cada um desses passos diretamente pelo site do Github]:wiki/GITHUB-BROWSER.md
[Hugo]:https://gohugo.io/
[1]:https://cypherpunks.com.br
[2]:https://t.me/CypherpunksBrasil
[3]:https://odysee.com/@CypherpunksBrasil
[4]:https://cypherpunks.com.br/index.xml
[5]:https://www.youtube.com/c/CypherpunksBrasil
[6]:https://www.instagram.com/cypherpunksbrasiloficial
[7]:https://twitter.com/cypherpunksbr
[8]:https://facebook.com/cypherpunksbrasiloficial