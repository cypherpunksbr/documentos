---
title:  "Tutorial GPG"
date:   2018-07-11
categories:
  - Tutorial
tags:
  - Criptografia
  - PGP
author:
  - OneTimePad
---

```
Escrito por: OneTimePad 
Revisado por: Jefferson, Cypherpunks Brasil
```
[```ver lista de contribuidores```](/about/#contribuidores)


**<span style="font-size: 24px;">Tutorial GPG</span>**
===exibe no card daqui pra baixo===

1.  [<span style="font-size: 12px;">Como instalar o GPG?</span>](#gpg1)
2.  [<span style="font-size: 12px;">Como criar uma chave GPG?</span>](#gpg2)
3.  [<span style="font-size: 12px;">Visualizando chaves instaladas</span>](#gpg3)
4.  [<span style="font-size: 12px;">Exportando a chave para um servidor de chaves</span>](#gpg4)
5.  <span style="font-size: 12px;">Criando um certificado de revogação</span>
6.  <span style="font-size: 12px;">Revogando uma chave</span>
7.  <span style="font-size: 12px;">Fazendo backup da sua chave (importante)</span>
8.  <span style="font-size: 12px;">Importando uma chave</span>
9.  <span style="font-size: 12px;">Configurando cliente de email (Thunderbird)</span>
10.  <span style="font-size: 12px;">Adicionando sua chave ao cypherpunks.com.br</span>

**<span id="gpg1" style="font-size: 24px;">1 - Como instalar o GPG</span>** No Ubuntu, abra o terminal (Ctrl + Alt + T) e instale o gpg:

    sudo apt-get install gnupg

<span id="gpg2" style="font-size: 24px;">**2 - Como criar uma chave GPG?**</span> Digite:

    gpg --full-generate-key

Depois escolha a opção (2) DSA e Elgamal ![](https://cypherpunks.com.br/wp-content/uploads/2018/11/full-generate-key.png) Escolha o tamanho da sua chave. Neste exemplo, optamos pelo tamanho máximo, isto é 3072 bits. ![](https://cypherpunks.com.br/wp-content/uploads/2018/11/full-generate-key_2.png)

Escolha o período de expiração. Essa opção é boa quando se quer que a chave seja inutilizada depois de um tempo. Mas para este exemplo, optamos por escolher uma chave que nunca expira, utilizando a opção (0) e logo em seguida, confirmando com "s".

![](https://cypherpunks.com.br/wp-content/uploads/2018/11/full-generate-key_3-1.png)

Preencha os campos com o seu nome, e-mail e com um comentário (opcional). Confirme apertando "o", ou altere apertando a letra inicial do que deseja alterar. Muda (N)ome, (C)omentário, (E)ndereço ou (O)k/(S)air?

![](https://cypherpunks.com.br/wp-content/uploads/2018/11/full-generate-key_4.png)

Agora vem a parte mais importante, **você precisa escolher uma senha!** É altamente recomendado que você saiba como escolher uma senha segura. Se tiver dúvidas, veja este artigo sobre como gerar uma senha segura e refaça o processo. Uma dica simples: **a sua senha precisa ser longa**, bem longa, e é altamente recomendável que também tenha números, letras maiúsculas e símbolos. **Mas o mais importante é, ela precisa ser longa.**

Assegure-se que digitou a senha corretamente, que você a lembra e prossiga. É desaconselhável salvar a senha de maneira digital. ![](https://cypherpunks.com.br/wp-content/uploads/2018/11/password.png) Feito isto, mova o ponteiro do seu mouse para todos os lados. Isto vai gerar entropia adicional para a sua chave. ![](https://cypherpunks.com.br/wp-content/uploads/2018/11/entropy-2.png) Depois deste processo, suas chaves foram geradas! Parabéns :) ![](https://cypherpunks.com.br/wp-content/uploads/2018/11/entropy_2.png) <span id="gpg3" style="font-size: 24px;">**3 - Visualizando chaves instaladas**</span>

    gpg --list-keys

![](https://cypherpunks.com.br/wp-content/uploads/2018/11/list-keys.png) <span id="gpg4" style="font-size: 24px;">**4- Exportando a chave para um servidor de chaves** </span> Basta digitar _gpg --keyserver "nome do servidor" --send-keys "codigo_da_sua_chave"_. Onde o código da sua chave é o mesmo exibido no _--list-keys_ (exemplo anterior):

    gpg --keyserver pgp.mit.edu --send-keys 82B9F18C369B01C3FD9AD68860F7A497E8AD7602

![](https://cypherpunks.com.br/wp-content/uploads/2018/11/keyserver.png) Servidores famosos: pgp.mit.edu keys.gnupg.net subkeys.pgp.net keyserver.pgp.com keyserver.ubuntu.com sks-keyservers.net [outros](https://sks-keyservers.net/status/)