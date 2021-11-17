---
title:  "Truledger"
date:   2008-01-01
categories: 
  - Artigo
tags:
  - Dinheiro eletrônico
  - Protocolo
  - Token
author:
  - Bill St. Clair
---

```
Traduzido por: Matheus Bach
Revisado por: Cypherpunks Brasil
```
[```ver lista de contribuidores```](/about/#contribuidores)


## Bill St. Clair

###### 2008

===exibe no card daqui pra baixo===

[Truledger](http://truledger.com/) é um cofre e um sistema de negociação anônimo digitalmente assinado. Assim como [Loom](https://loom.cc/), ele permite que qualquer pessoa publique ativos (moedas digitais). Ao contrário do Loom, que se baseia inteiramente em uma (muito boa) obscuridade para segurança, as assinaturas digitais da Truledger permitem que o servidor e o cliente comprovem entre si que concordaram com seus respectivos saldos em um determinado momento. Isso é feito enquanto permite a destruição do histórico de transações de negociações concluídas. O Truledger fornecerá inicialmente negociação baseada em servidor. Eventualmente, fornecerá contas digitais e certificados ao titular. No entanto, estes exigirão armazenamento permanente do histórico de transações (a menos que expirem).

[doc/db.txt](http://truledger.com/doc/db.txt) fornece uma descrição concisa do banco de dados e do protocolo do servidor Truledger. Esta página tenta apresentar o protocolo em inglês puro.

O Truledger usa criptografia de chave pública para assinar todas as mensagens passadas entre sua interface da web e o servidor Truledger. As assinaturas digitais são uma maneira praticamente infalsificável de garantir que uma mensagem tenha sido escrita por seu suposto autor. O Truledger usa OpenSSL para sua criptografia de chave pública. Você provavelmente usa OpenSSL toda vez que visita um site seguro, https://qualquersitecomhttps.com/, assim como o servidor da web. Eu não fiz sozinho. Acabei de usar a mesma tecnologia comprovada e segura que protege a web. Você pode ler mais sobre criptografia de chave pública, assinaturas digitais e hash [aqui](http://en.wikipedia.org/wiki/Public-key_cryptography) e [aqui](http://www.pgpi.org/doc/pgpintro/).

Vou usar quatro atores nos cenários a seguir. "Servidor" é o nome do servidor Truledger. "Bob" e "Sue" são dois clientes, que negociarão entre si. "Spammer" é um terceiro cliente, desconhecido por Bob ou Sue.

### Cenário: Abrindo uma Conta

Sue (via e-mail ou mensagem instantânea): Eai, Bob. Dê uma olhada na Truledger. Vá para Truledger.com, faça o download do client e instale-o no seu computador. Em seguida, crie uma chave privada e me envie seu ID, e eu darei alguns tokens de uso para que você possa criar uma conta.

Bob (via e-mail ou mensagem instantânea): Obrigado, Sue! Instalei o client Truledger e criei uma chave privada. Aqui está o meu ID.

Sue (através do client Truledger): Ei, Servidor, aqui está uma nova solicitação. Dê-me um número de transação, por favor. Assinado: Sue

Servidor: aqui está um novo número de transação.
 Assinado: Servidor

Sue: Ei, Servidor, aqui está o número da transação que você me deu. Por favor, gaste 50 tokens de uso no ID de Bob, com uma mensagem de "Hey Bob. Bem-vindo ao Truledger!" Pago 2 tokens de uso como taxa de transação, que retornarei quando Bob aceitar o pagamento. Meu saldo após esta transação será 1025 tokens de uso. O hash da minha caixa de saída após esta transação será X.
 Assinado: Sue

Servidor: processei seu gasto de 50 tokens de uso no ID de Bob. Concordo que a taxa de transação no momento desta transação seja 2 tokens de uso e que seu saldo após esta transação seja 1025 tokens de uso. Concordo com você no seu hash da caixa de saída.
 Assinado: Servidor

Sue (via e-mail ou mensagem instantânea): OK, Bob. Dei 50 tokens de uso para você. Agora você pode criar uma conta no Truledger.com. Envie-me uma mensagem via Truledger quando você se registrar.

Bob (via seu cliente Truledger): Olá Servidor. Aqui está meu ID e minha chave pública. Qual é o seu ID e chave pública?
 Assinado: Bob

Servidor: aqui está minha identificação (ID) e chave pública.
 Assinado: Servidor

Bob: Aqui está meu ID e minha chave pública, por favor crie uma conta para mim.
 Assinado: Bob

Servidor: registrei seu ID e chave pública. Alguém lhe deu fichas suficientes para se registrar. Bem-vindo ao Truledger.
 Assinado: Servidor

---

Para assinar uma mensagem, você precisa ter uma chave privada. Para verificar a assinatura em uma mensagem, você precisa ter a chave pública correspondente. O Truledger identifica os clientes pelo hash de sua chave pública, seu ID. O ID é uma sequência 40 caracteres formados de numeros letras de A a F, ou seja, uma representação hexadecimal de um número de 160 bits. Você identifica sua conta para o cliente do Truledger com uma senha, usada para criptografar sua chave privada no seu disco. Você só precisará copiar e colar seu ID quando desejar informar a um parceiro comercial como lhe enviar dinheiro pela primeira vez ou semear sua conta com tokens de uso, como Sue fez para Bob.

Os tokens de uso são uma ideia do sistema [Loom](https://loom.cc/) de Patrick Chkoreff. Eles são uma maneira de cobrar pelos recursos do servidor. Você precisa comprar armazenamento para os saldos da sua conta e conceder armazenamento temporário para transações. Os tokens de uso são a "moeda" usada para fazer isso. O Truledger também suporta taxas em outros tipos de ativos, para gerenciamento de servidores que desejam ganhar mais do que a venda de tokens de uso. O Truledger usa o sistema de arquivos como um banco de dados. Um arquivo no banco de dados do Truledger custa um token de uso. Os arquivos variam em tamanho, mas geralmente têm cerca de 8K,principalmente assinaturas.

Perceba que Bob precisou enviar sua chave pública para o servidor duas vezes, uma vez quando solicitou a chave pública do servidor e outra vez quando se registrou. Toda mensagem enviada para e de Truledger é assinada digitalmente. Só é possível verificar uma assinatura digital se você souber a chave pública do assinante. A chave pública de um novo cliente não está no banco de dados até depois do registro, portanto, as duas primeiras mensagens, nas quais o novo cliente obtém a chave pública do servidor, precisam incluir a chave pública do cliente, para que ele possa verificar as assinaturas do servidor e a solicitação de registro nestas dus mensagens. Após a conclusão do registro, as mensagens subseqüentes precisam levar apenas o ID; a chave pública pode ser procurada no banco de dados.

Mensagens reais enviadas (com a assinatura que acompanha cada item omitido entre parênteses):

``` {.snippet}
Sue: (<suesid>,gettime,<servidorid>,<req#>)
Servidor: (<servidorid>,time,<suesid>,<time#>)
Sue: (<suesid>,spend,<servidorid>,<time#>,<bobsid>,<tokenid>,50,Hey Bob\. Bem-vindo ao Truledger!).
        (<suesid>,tranfee,<servidorid>,<time#>,<tokenid>,2).
        (<suesid>,balance,<servidorid>,<time#>,<tokenid>,1025).
        (<suesid>,outboxhash,<servidorid>,<time#>,X)
Servidor: (<servidorid>,@spend,(<suesid>,spend,<servidorid>,<time#>,<bobsid>,<tokenid>,50,Hey Bob\. Bem-vindo ao Truledger!)).
        (<servidorid>,@tranfee,(<suesid>,tranfee,<servidorid>,<time#>,<tokenid>,2)).
        (<servidorid>,@balance,(<suesid>,balance,<servidorid>,<time#>,<tokenid>,1025)).
        (<servidorid>,@outboxhash,(<suesid>,outboxhash,<servidorid>,<time#>,X))
Bob: (<bobsid>,servidorid,<pubkey>)
Servidor: (<servidorid>,register,<servidorid>,<pubkey>,Truledger)
Bob: (<bobsid>,register,<servidorid>,<pubkey>,Bob)
Servidor: (<servidorid>,@register,(<bobsid>,register,<servidorid>,<pubkey>,Bob))
```

### Cenário: Recebendo ativos

Bob: Olá servidor. Aqui está o meu ID e um novo número de solicitação. O que há na minha caixa de entrada?
 Assinado: Bob

Servidor: sua caixa de entrada contém 50 tokens uso vindos de Sue com a mensagem "Hey, Bob. Bem-vindo ao Truledger!" Ele também contém uma taxa de 10 tokens de uso do servidor com uma mensagem de "Taxa de registro". Aqui estão dois números de transação que você pode usar para aceitar esses gastos e gastar você mesmo
 Assinado: Servidor

Bob: Aqui está meu ID e o primeiro número de transação que você me deu. Aceite os gastos de Sue com uma mensagem "Obrigado, Sue. Estou empolgado com Truledger!" e aceite a cobrança do servidor. Meu saldo após esta transação será de 39 tokens de uso.
 Assinado: Bob

Servidor: processei os gastos de Sue e a cobrança do servidor. Concordo que seu saldo após esta transação seja de 39 tokens de uso.
 Assinado: Servidor

---

Um possível ataque a um servidor eletrônico pode ser a repetição de uma mensagem interceptada. A menos que o protocolo proteja isso, isso pode causar problemas. Exceto para a solicitação do servidor, a solicitação de registro e uma solicitação do último número da solicitação do cliente, toda solicitação de informações deve ser acompanhada por um número maior que o último número da solicitação usada pelo cliente e toda transação deve ser acompanhada de uma transação número que é fornecido pelo servidor. O servidor mantém um contador, que é incrementado toda vez que alguém pede um número de transação. Isso impossibilita a reprodução de solicitações que revelam informações ou iniciam transações sem a senha e a chave privada do cliente. No mundo do Truledger, sua senha e sua chave privada são sua identidade. Guarda-os bem.

Outro possível ataque de reprodução é interceptar uma mensagem para um servidor e enviá-la para outro. Os clientes podem se proteger contra isso, tendo IDs diferentes, portanto, pares de chaves pública / privada diferentes, para servidores diferentes. Mas será muito conveniente usar o mesmo ID. Seus amigos o reconhecerão e você terá apenas uma senha para lembrar. Portanto, o ID do servidor está incluído em quase todas as solicitações. Solicitações destinadas a outro servidor não funcionarão.

Você provavelmente está se perguntando por que o saldo de Bob após a transação é de 39, em vez de 40, tokens de uso. Ele conseguiu 50 tokens de uso de Sue e pagou ao servidor 10 tokens de uso pela taxa de registro. O token de uso adicional é o preço do novo arquivo usado para armazenar o saldo do token de uso. Tokens de uso de custos de armazenamento. O tear cobra 1 token de uso para cada 16 bytes de armazenamento. Eu considerei a cobrança por byte, mas decidi que a cobrança por arquivo era mais fácil de lidar, embora não fosse tão justa. Só faz sentido se os tamanhos das mensagens forem limitados, é claro. Se você recebesse mensagens em megabytes, o Truledger teria que cobrar por byte ou por kilobyte.

Mensagem atual enviada:

``` {.snippet}
Bob: (<bobsid>,getinbox,<serverid>,<req#>)
Servidor: (<servidorid,@getinbox,(<bobsid>,getinbox,<servidorid>,<req#>)).
        (<servidorid>,inbox,<time3#>,(<suesid>,spend,<servidorid>,<time#>,<bobsid>,<tokenid>,50,Hey Bob\. Bem-vindo ao Truledger!)).
        (<servidorid>,inbox,<time4#>,(<servidorid>,spend,<serverid>,<time2#>,<bobsid>,<tokenid>,-10,Taxa de Registro)).
        (<servidorid>,time,<bobsid>,<time5#>).
        (<servidorid>,time,<bobsid>,<time6#>)
Bob: (<bobsid>,processinbox,<servidorid>,<time5#>,<time3#>|<time4#>).
       (<bobsid>,spend|accept,<servidorid>,<suesid>,<time#>,Obrigado Sue\. Estou empolgado com Truledger!).
       (<bobsid>,spend|accept,<servidorid>,<servidorid>,<time2#>).
       (<bobsid>,balance,<servidorid>,<time5#>,<tokenid>,39)
Servidor: (<servidorid>,@processinbox,(<bobsid>,processinbox,<serverid>,<time5#>,<time3#>|<time4#>)).
        (<servidorid>,@spend|accept,(<bobsid>,spend|accept,<servidorid>,<suesid>,<time#>,Obrigado Sue\. Estou empolgado com Truledger!)).
        (<servidorid>,@spend|accept,(<bobsid>,spend|accept,<servidorid>,<servidorid>,<time2#>)).
        (<servidorid>,@balance,(<bobsid>,balance,<servidorid>,<time5#>,<tokenid>,39))
```

### Cenário: fechando uma transação

Sue: Olá Servidor. Aqui está o meu ID e um novo número de solicitação. O que há na minha caixa de entrada?
 Assinado: Sue

Servidor: sua caixa de entrada contém uma aceitação de Bob dos seus 50 token de uso gastos com a mensagem "Obrigado Sue. Estou empolgado com Truledger!" Aqui estão dois números de transação que você pode usar para fechar essa transação e fazer um novo gasto.
 Assinado: Servidor

Sue: Aqui está meu ID e o primeiro número de transação que você me deu. Limpe os gastos para Bob. Meu saldo após esta transação será 1027 tokens de uso. O hash da minha caixa de saída após esta transação será Y.
 Assinado: Sue

Servidor: Limpei os gastos para Bob (e reembolsei os tokens de uso que estavam alugando os locais da caixa de saída e da caixa de entrada). Concordo que seu saldo após esta transação seja 1027 tokens de uso. E eu concordo que o hash da sua caixa de saída após esta transação é Y.
 Assinado: Servidor

---

Existem três partes principais de uma conta do Truledger: os saldos, a caixa de saída e a caixa de entrada. O valor é armazenado nos três locais. Quando você gasta, seu saldo para o ativo gasto é debitado e a solicitação de gasto é armazenada na sua caixa de saída e na caixa de entrada do destinatário. Você recebe dois tokens de uso para conceder os novos arquivos de caixa de saída e caixa de entrada. Quando o destinatário aceita os gastos, o saldo do ativo gasto é creditado, o aviso de gasto é removido da caixa de entrada e um aviso de aceitação de gasto é adicionado à sua caixa de entrada. Quando você reconhece a aceitação dos gastos, a solicitação de gastos é removida da caixa de saída, o aviso de aceitação é removido da caixa de entrada e os dois tokens de uso que você pagou para alugar esses arquivos são creditados no seu saldo. Esse processo de três etapas é necessário, porque o servidor não pode modificar seus saldos sem sua permissão assinada e não pode modificar os saldos do destinatário sem sua permissão assinada.

Você pode estar se perguntando o que é um "hash da caixa de saída". Seus saldos mais sua caixa de saída representam a parte da sua conta que você e o servidor concordaram. Sua caixa de entrada é alterada sem o seu conhecimento, mas o servidor precisa da sua permissão assinada para alterar sua caixa de saída (gastar) ou seus saldos. Como sua caixa de saída pode ficar grande, em vez de enviar todo o conteúdo toda vez que você gasta ou reconhece a aceitação (ou rejeição) de uma despesa por um destinatário, você calcula um hash da sua caixa de saída e envia-o , e o servidor responde com um reconhecimento desse hash da caixa de saída (obrigado a Patrick Chkoreff por essa ideia).

Mensagem atual enviada:

``` {.snippet}
Sue: (<suesid>,getinbox,<servidorid>,<req2#>)
Server: (<servidorid,@getinbox,(<suesid>,getinbox,<servidorid>,<req2#>)).
        (<servidorid>,inbox,<time7#>,(<bobsid>,spend|accept,<servidorid>,<suesid>,<time#>,Obrigado Sue\. Estou empolgado com Truledger!)).
        (<servidorid>,time,<bobsid>,<time8#>).
        (<servidorid>,time,<bobsid>,<time9#>)
Sue: (<suesid>,processinbox,<servidorid>,<time8#>,<time7#>).
       (<suesid>,balance,<servidorid>,<time8#>,<tokenid>,1027).
       (<suesid>,outboxhash,<servidorid>,<time8#>,Y)
Server: (<servidorid>,@processinbox,(<suesid>,processinbox,<servidorid>,<time8#>,<time7#>)).
        (<servidorid>,@balance,(<suesid>,balance,<servidorid>,<time8#>,<tokenid>,1027)).
        (<servidorid>,@outboxhash,(<suesid>,outboxhash,<servidorid>,<time8#>,Y))
```

### Cenário: Prevenção de Spam

Spammer (provavelmente rodando através de um software automatizado): Ei, servidor. Aqui está um novo número de solicitação. Dê-me um número de transação, por favor.
 Assinado: Spammer

Servidor: aqui está um novo número de transação.
 Assinado: Servidor

Spammer: Ei, servidor. Aqui está o número da transação que você me deu. Gaste 0 tokens de uso na identificação de Bob, com a mensagem "Seja milonaro, imvista na Unik Forebis". Pago 2 tokens de uso como taxa de transação, que retornarei quando Bob aceitar os gastos. Meu saldo após esta transação será 2425 tokens de uso. O hash da minha caixa de saída após esta transação será Z.
 Assinado: Spammer

Servidor: processei seu gasto de 0 tokens de uso no ID de Bob. Concordo que a taxa de transação no momento desta transação é de 2 tokens de uso e que seu saldo após esta transação é de 2425 tokens de uso. Concordo com você no seu hash da caixa de saída.
 Assinado: Servidor

Bob: Olá servidor. Aqui está o meu ID e um novo número de solicitação. O que há na minha caixa de entrada?
 Assinado: Bob

Servidor: sua caixa de entrada contém 0 tokens de uso gastos do Spammer com a mensagem "Seja milonaro, imvista na Unik Forebis". Aqui estão dois números de transação que você pode usar para aceitar esses gastos do Spammer e receber como saldo.
 Assinado: Servidor

Bob: Aqui está meu ID e o primeiro dos numeros de transação que você me deu. Rejeite o gasto de Spammer com a mensagem "Obrigado pelos tokens", e me dê os dois tokens de uso que ele pagou para enviar esse spam. Meu balanço depois desta transação será de 41 tokens de uso.
 Assinado: Bob

Servidor: Rejeitei o gasto do Spammer. Eu aceito que seu balanço após essa transação é de 41 tokens de uso.
 Assinado: Servidor

---

Gastos podem ser rejeitados. A quantia enviada volta para quem solicitou o gasto, mas Spends can be rejected. The amount spent goes back to the spender, mas o destinatário é quem embolsa a taxa de transação. Gastos zero servem para usar a Truledger cmo um serviç de mensagem simples. Mas não são de graça, a menos que o destinatário queira a mensagem. Na minha humilde opinião, spam existem tanto por que é praticamente de graça enviar um e-mail. Em um sistema em que cada mensagem de spam custa 2 tokens de uso, fazer spam será barato, mas não de graça. Duvido que isso venha a ser um grande problema. O tempo dirá.

Mensagem atual enviada:

``` {.snippet}
Spammer: (<spammersid>,gettime,<serverid>,<req#>)
Servidor: (<serverid>,time,<spammersid>,<time10#>)
Spammer: (<spammersid>,spend,<serverid>,<time10#>,<bobsid>,<tokenid>,0,Seja milonaro\. Imvista na Unik Forebis\.).
        (<spammersid>,tranfee,<serverid>,<time#>,<tokenid>,2).
        (<spammersid>,balance,<serverid>,<time#>,<tokenid>,2425).
        (<spammersid>,outboxhash,<serverid>,<time#>,Z)
Servidor: (<serverid>,@spend,(<spammersid>,spend,<serverid>,<time#>,<bobsid>,<tokenid>,0,Seja milonaro\. Imvista na Unik Forebis\.)).
        (<serverid>,@tranfee,(<spammersid>,tranfee,<serverid>,<time#>,<tokenid>,2)).
        (<serverid>,@balance,(<spammersid>,balance,<serverid>,<time#>,<tokenid>,2425)).
        (<serverid>,@outboxhash,(<spammersid>,outboxhash,<serverid>,<time#>,Z))
Bob: (<bobsid>,getinbox,<serverid>,<req2#>)
Servidor: (<serverid,@getinbox,(<bobsid>,getinbox,<serverid>,<req2#>)).
        (<serverid>,inbox,<time11#>,(<spammersid>,spend,<serverid>,<time10#>,<bobsid>,<tokenid>,0,Seja milonaro\. Imvista na Unik Forebis\.)).
        (<serverid>,time,<bobsid>,<time12#>).
        (<serverid>,time,<bobsid>,<time13#>)
Bob: (<bobsid>,processinbox,<serverid>,<time12#>,<time11#>).
       (<bobsid>,spend|reject,<serverid>,<spammersid>,<time12#>,<time10#>,Obrigado pelos tokens).
       (<bobsid>,balance,<serverid>,<time12#>,<tokenid>,41)
Servidor: (<serverid>,@processinbox,(<bobsid>,processinbox,<serverid>,<time12#>,<time11#>)).
        (<serverid>,@spend|reject,(<bobsid>,spend|accept,<serverid>,<spammersid>,<time12#>,<time10#>,)Obrigado pelos tokens).
        (<serverid>,@balance,(<bobsid>,balance,<serverid>,<time12#>,<tokenid>,41))
```

### Cenário: Emissão de ativos

Bob: Ei, servidor. Aqui está um novo número de solicitação. Dê-me um número de transação, por favor.
 Assinado: Bob

Servidor: aqui está um novo número de transação.
 Assinado: Servidor

Bob: Ei, servidor. Aqui está o número da transação que você me deu. Registre um novo ativo chamado "Bob GoldGrams". Tem uma escala de 7 e uma precisão de 3. O Seu ID é \<bobggid\>. Meu saldo após esta transação será de 39 tokens de uso e -1 \<bobggid\>.

Servidor: registrei o novo ativo "Bob GoldGrams". Concordo que seu saldo após esta transação seja de 39 tokens de uso e -1 \<bobggid\>.

---

LComo o Loom, o Truledger permite que os clientes criem seus próprios tipos de ativos. Então, se eles puderem convencê-los a fazer isso, outros clientes poderão negociar nesse tipo de ativo. O ID de um ativo do Truledger é o hash sha1 do ID do criador, sua escala, precisão e nome. Mas a mensagem que o cliente assina para criar o ativo e que o servidor assina para confirmar a criação também contém a identificação do servidor. Isso permite que o ativo seja registrado em vários servidores, com o mesmo ID, mas torna cada registro particularmente específico para um servidor específico. Portanto, faz sentido que um emissor de ativos forneça um serviço de transferência de seus ativos entre servidores nos quais está registrado; é evidente que Bob GoldGrams no servidor A é o mesmo ativo que Bob GoldGrams no servidor B.

Pretendo suportar a transferência de emissão de ativos, mas ainda não resolvi os empecilios.

Como na Loom, todos os valores no Truledger são armazenados como números inteiros. O valor da escala controla onde o ponto decimal fica na representação do mundo real desse valor: mova-o para a esquerda por locais da escala. A precisão controla o número mínimo de casas decimais impressas. Portanto, com uma escala de 7 e uma precisão de 3, o valor 12000000 será impresso pelos clientes da Truledger como 1.200, e o valor mínimo para a nova moeda de Bob é 0,0000001, um décimo milionésimo de um grama de ouro ou US \$ 0,000003 a US \$ 30 / grama: 3 dez milésimos de centavo. Olá micropagamentos.

Também como na Loom, a soma de todos os valores, em contas e caixas de saída, para determinado ativo é -1. Há um saldo negativo, de propriedade do emissor, que pode gastar o quanto quiser, vários saldos positivos, e várias entradas da caixa de saída. Um saldo de -1 na conta do emissor significa que não há saldos pendentes ou entradas na caixa de saída nesse ativo, então é aí que o saldo de Bob GoldGrams de Bob começa. Os usuários de um ativo precisam confiar no emissor quando ele diz, por fora da Truledger, que seu ativo tem um real valor ou é respaldado por algo de valor real e que ele nunca emitirá mais ativos virtuais do que o seu lastro. Bem, a menos que ele queira agir como um país, e emitir moeda fiduciária apoiada por sua Plena Fé e Crédito e nada mais. Boa sorte tentando convencer alguém.

Mensagem atual enviada:

``` {.snippet}
Bob: (<bobsid>,gettime,<serverid>,<req3#>)
Servidor: (<serverid>,time,<bobsid>,<time13#>)
Bob: (<bobsid>,asset,<serverid>,<bobggid>,7,3,Bob GoldGrams).
       (<bobsid>,balance,<serverid>,<time13#>,<tokenid>,39).
       (<bobsid,balance,<serverid>,<time13#>,<bobggid>,-1)
Servidor: (<serverid>,#asset,(<bobsid>,asset,<serverid>,<bobggid>,7,3,Bob GoldGrams)).
       (<serverid>,#balance,(<bobsid>,balance,<serverid>,<time13#>,<tokenid>,39)).
       (<serverid>,#balance,(<bobsid,balance,<serverid>,<time13#>,<bobggid>,-1))
```

### Cenário: várias subcontas

Bob: Eae, servidor. Aqui está um novo número de solicitação. Me dê um número de transação, por favor.
 Assinado: Bob

Servidor: Aqui está um novo número de transação.
 Assinado: Servidor

Bob: Olá, servidor. Aqui está o número da transação que você me deu. Faça um gasto zero comigo mesmo. Meu saldo após a transação será de 38 tokens de uso, -311.0347681 Bob GoldGrams na minha subconta padrão e 311.034768 Bob GoldGrams na minha subconta "Gun Safe".

Servidor: eu fiz esse gasto. Concordo que após a transação, seu saldo será de 38 tokens de uso, -311,0347681 Bob GoldGrams na sua conta padrão e 311,034768 Bob GoldGrams na sua subconta "Gun Safe".

Bob: Ei, servidor. Aqui está um novo número de solicitação. Dê-me um número de transação, por favor.
 Assinado: Bob

Servidor: Aqui está um novo número de transação.
 Assinado: Servidor

Bob: Ei, servidor. Aqui está o número da transação que você me deu. Gaste 2.4056304 Bob GoldGrams para Sue, com uma mensagem de "Bem, eu finalmente criei minha nova moeda, lastreada em Krugerands que estão no cofre de armas. Estou lhe enviando uma grama como agradecimento por ter me apresentado a Truledger e [1.4056304 gramas](https://www.google.com/search?q=(36+dólares+%2F+(796,60+dólares+por+onça+troy)+em+gramas) por 36 unidades de [Café Capulin](http://capulin.com/) , que você disse que me venderia, para que eu possa comprar mais café fino do Daniel Fourwinds que saboreamos em sua casa outro dia. Usei um preço de ouro de US\$ 796,60/onça, o melhor preço de venda na Kitco hoje de manhã.". Minha taxa de transação será de 2 tokens de uso. Meu saldo após esta transação será de 36 tokens de uso e 309,6291376 Bob GoldGrams na minha subconta "Gun Safe" Meu hash da caixa de saída após esta transação será A.
 Assinado: Bob

Servidor: Fiz o seu gasto de 2,4056304 Bob GoldGrams para Sue, com sua mensagem e uma taxa de transação de 2 tokens de uso. Concordo que seu saldo após esta transação seja de 36 tokens de uso e 309.6291376 Bob GoldGrams na sua subconta "Gun Safe". Concordo com o hash da caixa de saída.
 Assinado: Servidor

---

Truledger suporta a divisão de seus saldos em várias "subcontas". Assim como um servidor convencional fornece uma conta corrente e uma conta poupança, você pode usar essas subcontas para ajudar a gerenciar seus ativos. Você pode ter quantas subcontas desejar, limitado apenas aos tokens de uso que você tenha para pagar pelos arquivos.

Bob decidiu acompanhar seus Bob GoldGrams com uma subconta chamada "Gun Safe", com um saldo registrando quantos gramas de ouro em seu cofre ainda não foram colocados em circulação. Ele semeia com [10 onças](http://www.google.com/search?q=10+onças+troy+em+gramas) de gold, a parte de suas propriedades que ele está disposto a vender. Depois, ele gasta uma parte para Sue, pedindo unidades de Café Capulin suficientes para duas libras de Café Capulin (US\$ 17,95 por libra, enviado).

Perceba que você não precisa mencionar todos os seus saldos a cada gasto. Você menciona apenas os saldos que mudam. Observe também que não há taxa de transação para gastos consigo mesmo. A movimentação de ativos entre suas subcontas custa apenas tokens para novos arquivos. Não precisa ficar lotando a caixa de saída e a caixa de entrada.

Mensagem atual enviada:

``` {.snippet}
Bob: (<bobsid>,gettime,<serverid>,<req4#>)
Servidor: (<serverid>,time,<bobsid>,<time14#>)
Bob: (<bobsid>,spend,<serverid>,<time14#>,<bobsid>,<bobggid>,0).
        (<bobsid>,balance,<serverid>,<time14#>,<bobggid>,-3110347681).
        (<bobsid>,balance,<serverid>,<time14#>,<bobggid>,3110347680,Gun Safe)
Servidor: (<serverid>,@spend,(<bobsid>,spend,<serverid>,<time14#>,<bobsid>,<bobggid>,0)).
        (<serverid>,@balance,(<bobsid>,balance,<serverid>,<time14#>,<bobggid>,-3110347681)).
        (<serverid>,@balance,(<bobsid>,balance,<serverid>,<time14#>,<bobggid>,3110347680,Gun Safe))
Bob: (<bobsid>,gettime,<serverid>,<req5#>)
Servidor: (<serverid>,time,<bobsid>,<time15#>)
Bob: (<bobsid>,spend,<serverid>,<time15#>,<suesid>,<bobggid>,24056304,Bem, eu finalmente criei minha nova moeda, lastreada em Krugerands que estão no cofre de armas. Estou lhe enviando uma grama como agradecimento por ter me apresentado a Truledger e 1.4056304 gramas por 36 unidades de Café Capulin, que você disse que me venderia, para que eu possa comprar mais café fino do Daniel Fourwinds que saboreamos em sua casa outro dia. Usei um preço de ouro de US$ 796,60/onça, o melhor preço de venda na Kitco hoje de manhã.).
       (<bobsid>,tranfee,<serverid>,<time15#>,<tokenid>,2).
       (<bobsid>,balance,<serverid>,<time15#>,<bobggid>,3096291376,Gun Safe).
       (<bobsid>,outboxhash,<serverid>,<time15#>,A)
Servidor: (<serverid>,@spend,(<bobsid>,spend,<serverid>,<time15#>,<suesid>,<bobggid>,24056304,Bem, eu finalmente criei minha nova moeda, lastreada em Krugerands que estão no cofre de armas. Estou lhe enviando uma grama como agradecimento por ter me apresentado a Truledger e 1.4056304 gramas por 36 unidades de Café Capulin, que você disse que me venderia, para que eu possa comprar mais café fino do Daniel Fourwinds que saboreamos em sua casa outro dia. Usei um preço de ouro de US$ 796,60/onça, o melhor preço de venda na Kitco hoje de manhã.)).
       (<serverid>,@tranfee,(<bobsid>,tranfee,<serverid>,<time15#>,<tokenid>,2)).
       (<serverid>,@balance,(<bobsid>,balance,<serverid>,<time15#>,<bobggid>,3096291376,Gun Safe)).
       (<serverid>,@outboxhash,(<bobsid>,outboxhash,<serverid>,<time15#>,A))
```

### Cenário: Obtendo informações

Para ser feito

### Cenário: cancelando um gasto

Para ser feito

---

Copyright © 2008 Bill St. Clair, Todos os direitos reservados.

---

Fonte: 
https://truledger.com/doc/plain-english.html
https://nakamotoinstitute.org/truledger/