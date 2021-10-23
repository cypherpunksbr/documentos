# Contribua com o Projeto

## Como contribuir?

### Existem diversas formas de contrbuir com nosso projeto. Vamos listar algumas:
> clique no item para ir direto ao guia prático

- [Adicionando novos Documentos](#add-new-docs)
- [Traduzindo Documentos para Português (pt-br)](#translate-docs-ptbr)
- Revisando e corrigindo Documentos já traduzidos
- Melhorando ou criando tutoriais sobre qualquer assunto que englobe o movimento cypherpunk
- Melhorando nosso site ```cypherpunks.com.br```
- Divulgando o projeto Cypherpunks Brasil
- Fazendo doações em criptomoedas ou outras formas de valor
- Iniciando, liderando ou auxiliando a criação de novos projetos

---

<div id='add-new-docs'/>

## Adicionando novos Documentos à biblioteca

Você pode adicionar qualquer tipo de documento relaciondo ao movimento cypherpunk à nossa biblioteca

### Mão na massa:
> dica: algumas palavras contém links que se você clicar nelas você será levado a uma explicação de como fazer

**1.** Faça um [Fork](falta-colocar-referência-aqui) do nosso repositório no github.

**2.** Dentro de seu fork, crie uma nova [Branch](falta-colocar-referência-aqui) com um nome que espeficique o objetivo. Por exemplo ```adiciona-bitcoin-whitepaper```. Após criar essa branch, é dentro dela que você irá trabalhar.

**3.** Encontre o documento que deseja traduzir na internet, em livros, qualquer lugar, ou escreva você mesmo um texto autoral. Salve as informações importantes (link para a página web, nome do livro, autor, data de publicação), elas serão usadas nas próximas etapas.
O documento pode estar em qualquer idioma, incluindo o português (pt-br).

**4.** Dentro do seu fork e sua branch, salve o documento em um arquivo único de texto com extensão ```.md``` (Markdown) na pasta correta e com o nome correto. A pasta que ele será salvo depende do idioma que ele está. Caso ele esteja ele não esteja em pt-br ele precisa ser salvo na pasta ```/para traduzir/```, caso ele já esteja em pt-br ele pode ser salvo direto na pasta ```/para revisar/```. O nome do arquivo obedece a fomatação ```data-da-publicação-titulo.md```, por exemplo: ```25-09-2000-titulo-do-documento-aqui.md```. Caso o documento apresente imagens ou outros arquivos que precisam ser supridos para o documento, salve esses arquivos na pasta ```/stuff/``` do repositório. No futuro você irá referenciar esses arquivos usando markdown caso necessário.

**5.** Formate o documento para seguir o padrão dos textos publicados. Formate o texto usando o padrão de sintaxe [```Markdown```](luong-komorebi/Markdown-Tutorial/blob/master/README_pt-BR.md). Tome cuidado para não esquecer de formatar nada, reconstrua as referências de links que estão no site, palavas em itálico, citações, parâgrafos, imagens, tudo! Isso precisa estar muito bem feito para quem venha a traduzir e ler o documento não fique com um texto mal formatado.

**6.** Adicione nosso cabeçalho. Esse cabeçalho serve para que nosso site (feito com jekyll) reconheça informações importantes e agregue isso na exibição ao leitor. Adicione o cabeçalho a seguir no início do documento, alterando as informações pelas informações do seu texto. Caso alguma das informações exigidas não faça sentido para o caso do seu documento, apague a linha:

```
---
title:  "Título do seu Documento aqui" com aspas
date:   data da publicação no formato dia-mês-ano (exemplo: 31-10-2008) sem aspas
categories:
  - Biblioteca
tags:
  - tag util 1 sem aspas
  - tag util 2 sem aspas
  - tag util 3 sem aspas
---
```

**7.** Após ter feito isso seu documento está organizado e pronto para ser incluído no repositório raiz do projeto no GitHub. Para incuir ele é necessário realizar um [Pull Request (PR)](falta-colocar-referência-aqui) da sua branch para a branch main do repositório raiz, exemplo: ```cypherpunksbr/documentos|main``` ```<--``` ```matheusbach/documentos|adiciona-bitcoin-whitepaper```. Após ter feito o PR, aguarde um dos membros da organização revisar suas alterações e aprovar seu trabalho. Obrigado por colaborar com o projeto!

---

<div id='translate-docs-ptbr'/>

## Traduzindo Documentos para Português (pt-br)

Você pode traduzir qualquer documento presente na pasta [```/para traduzir/```](para%20traduzir/) ou então caso queira traduzir um documento que não está nessa pasta você pode primeiro [adicionar novos Documentos à biblioteca](#add-new-docs)

### Mão na massa:
> dica: algumas palavras contém links que se você clicar nelas você será levado a uma explicação de como fazer

**1.** Faça um [Fork](falta-colocar-referência-aqui) do nosso repositório no github.

**2.** Dentro de seu fork, crie uma nova [Branch](falta-colocar-referência-aqui) com um nome que espeficique o objetivo. Por exemplo ```traduz-bitcoin-whitepaper```. Após criar essa branch, é dentro dela que você irá trabalhar.

**3.** Encontre o documento que deseja traduzir dentro da pasta [```/para traduzir/```](para%20traduzir/). É nessa pasta que estão os documentos que aguradam tradução.

**4.** Mova o arquivo para a pasta correta. Antes de começar a traduzir é necessário que você sinalise para todos que você está traduzindo esse texto para que não aconteça de duas pessoas ao memso tempo estar traduzindo a mesma coisa, gerando ineficiência e cause trabalho jogado fora. Para sinalizar a intenção de tradução você deve mover o arquivo do seu documento que está na pasta [```/para traduzir/```](para%20traduzir/) para a pasta [```/sendo traduzidos/```](sendo%20traduzidos/).

**5.** Para que sua intenção de tradução vá do seu fork e sua branch para o repositório raiz você precisa abrir um [Pull Request (PR)](falta-colocar-referência-aqui) da sua branch para a branch main do repositório raiz, exemplo: ```cypherpunksbr/documentos|main``` ```<--``` ```matheusbach/documentos|adiciona-bitcoin-whitepaper```. Após ter feito o PR, aguarde um dos membros da organização aprovar. Assim que aprovado você pode prosseguir com as próximas etapas.

**6.** Hora de traduzir o documento! A branch que você criou anteriormente continua no seu fork e é por lá que você continuará trabalhando. Encontre seu documento que está em ```/sendo traduzidos/dd-mm-aaaa-nome-do-seu-documento.md```. Agora edite o arquivo, realizando a traudução em si. Entenda:
- Você pode usar ferramentas para agilizar a tradução como por exemplo Google Translate, mas essas ferramentas costumas desformatar o texto e é muito frequente elas deixarem o texto sem sentido por que traduziram palavras de forma inadequada, tiraram contexto de expressões, tentaram traduzir termos técnicos e falharam miseravelmente, etc., portanto você precisa revisar bem o texto quando usar essas ferramentas;
- Não quebre a formatação do documento. Usamos o padrão de sintaxe [```Markdown```](luong-komorebi/Markdown-Tutorial/blob/master/README_pt-BR.md) com a adição de um cabeçalho no inicio do texto que orienta nosso site a classificar os documentos;
- Algumas palavras não exigem tradução pois são tão difundidas como a forma original até mais do que a tradução, como por exemplo "blockchain". Nesses casos coloque a palavra seguida pela tradução entre parêntesis, depois use apenas a palavra original caso ache mais adequado;
- Caso não saiba qual a melhor traducão para um trecho de texto peça ajuda. Você pode fazer isso pedidno para um amigo, abrindo uma Issue no github ou perguntando em nosso [grupo no telegram](https://t.me/criptologia);
- Se você traduziu um pedaço do trecho mas só vai poder continuar em outro momento, não tem problema, faça Commit da alteração ou salve o que já traduziu em outro local para poder continuar de onde parou
- Faça um bom trabalho. Saiba que você está ajudando outras pessoas a terem acesso facilitado a informação de qualidade e preservando/difundindo um pedaço da história para outro idioma.

**7.** Mova novamente o documnto de pasta. Agora você já finalizou a tradução e irá mover o documento para a pasta onde acontece a revisão. Para isso você deve mover o arquivo do seu documento que está na pasta [```/sendo traduzidos/```](sendo%20traduzidos/) para a pasta [```/para revisar/```](para%20revisar/)

**8.** Após ter traduzido e movido, o documento está pronto para ser incluído no repositório raiz do projeto no GitHub. Para incuir ele é necessário realizar um [Pull Request (PR)](falta-colocar-referência-aqui) da sua branch para a branch main do repositório raiz, exemplo: ```cypherpunksbr/documentos|main``` ```<--``` ```matheusbach/documentos|traduz-bitcoin-whitepaper```. Após ter feito o PR, aguarde um dos membros da organização revisar suas alterações e aprovar seu trabalho. Obrigado por colaborar com o projeto!