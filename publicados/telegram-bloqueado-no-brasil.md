---
title:  "Telegram bloqueado no Brasil - Como Burlar"
date:   2022-03-19
author:
  - CyberDef
  - Cypherpunks Brasil
categories:
  - Tutorial
tags:
  - Cripto Anarquia
  - Censura
description: "Certo dia o telegram foi bloqueado por um político cujo formato fálico da cabeça destoa. Veja como burlar esse bloqueio"
---

```
Guia criado por: CyberDef, Cypherpunks Brasil
```

[```ver lista de contribuidores```](/about/#contribuidores)

[Alexandre de Moraes](https://desciclopedia.org/wiki/Alexandre_de_Moraes) determinou que os [ISPs](https://pt.wikipedia.org/wiki/Fornecedor_de_acesso_%C3%A0_internet) bloqueassem o acesso de usuários ao Telegram. E eles obviamente o fizeram, sob ameaça de multa de R$ 500.000,00 (troco de bar para o parasita, para nós muita coisa). Além disso, usuários que burlarem o bloqueio pagam multa de R$ 100.000,00

Telegram foi acusado de abrigar canais de pedofilia, venda de armas ilegais, estelionato, e falsificação de documentos. Mas... o canal que o [STF](https://desciclopedia.org/wiki/Supremo_Tribunal_Federal) solicitou bloqueio até agora foi de um opositor político

![media](../stuff/bessa-depica.webp)

## Beleza, mas como a gente burla?

Depende de como for feito o bloqueio

### Se o App tiver sido removido das lojas de aplicativos

- Baixe e instale pela loja de apps F-Droid: https://f-droid.org/en/packages/org.telegram.messenger

- Não tem o F-Droid? Baixe ele aqui: https://f-droid.org/pt_BR/

- Baixe através do site oficial do Telegram: https://telegram.org/dl/android/apk

- Use as versões Web (para navegador):
  - Versão K: https://web.telegram.org/k/
  - Versão Z: https://web.telegram.org/z/

- Direto do código fonte (usuários avançados): https://github.com/DrKLO/Telegram

### Se manipularem o DNS

- Vá até as configurações do seu aparelho e busque por "DNS Privado". Ou vá até "Mais configurações de conexão" ou "Configurações avançadas de conexão".

- Clique em "DNS Privado" e escolha a opção "Automático" ou em "Nome do host do provedor de DNS privado" e insira um destes hosts:
  - Quad9 (da IBM): dns.quad9.net / dns11.quad9.net (com filtro anti conteúdo adulto)
  - Cloudfare: 1dot1dot1dot1.cloudflare-dns.com
  - OpenDNS (Cisco): doh.opendns.com / doh.familyshield.opendns.com (com filtro anti conteúdo adulto)

- Se não funcionar - configure na rede do seu smartphone (somente Wifi):

- Use aplicativos:
  - DNSCloak (para Iphone): baixe da AppStore
  - Nebulo (para Android): baixe da PlayStore

- Configure direto no seu roteador: https://support.opendns.com/hc/en-us/sections/206253627

- Configure direto no Navegador  https://support.opendns.com/hc/en-us/articles/360038086532-Using-DNS-over-HTTPS-DoH-with-OpenDNS

- Verifique se está configurado corretamente:
  Acesse o site https://www.dnsleaktest.com/ e clique em "Extended test"
  **Deverá aparecer o IP do provedor de DNS e não do seu Provedor de Internet (Oi, Vivo, Tim, Claro e etc)**
  
### Se tentarem banir os endereços de IP dos servidores do Telegram

- Use um dos proxies fornecidos pelo Telegram:
  Canais de Proxy: https://t.me/ProxyMTProto e https://t.me/proxyme

- Use uma VPN: 
  Não vou recomendar nenhuma. Faça sua própria pesquisa. 
  Este ranking de VPNs é um dos poucos confiáveis: https://techlore.tech/vpnchart.html
  Segundo o site, as melhores são: ProtonVPN, IVPN e Mullvad.

- Use o Tor Browser (para o Telegram versão Web). https://www.torproject.org/download/

- User o Orbot. Este app encaminha o tráfego de aplicativos pela rede Tor, fazendo com que pareça que você está em outro país. Download pela Play Store ou F-Droid

- NO IPHONE: Por precaução, adicione o Telegram-Webk no seu iPhone, para o caso dos governos bloquearem o acesso, ou mesmo a Apple remover o App da sua App Store!

- No Safari, abra o endereço webk.telegram.org

- Faça o seu login e autorize no App original 

- Depois que fez o login e consegue ver todas as suas conversas, clique no botão “compartilhar”

- Adicione o WebK na tela de início escolhendo a opção “Adicionar à Tela de Início”

- Agora foi adicionado um ícone na sua tela com o logo do Telegram, que você poderá utilizar exatamente como o App nativo! Deste modo você poderá sempre acessar seu Telegram!

---
Fonte: 
- [CyberDef - YouTube](https://www.youtube.com/channel/UC4BrnREinCBUenQZi4ZU95w)
- [CyberDef - Telegram](https://t.me/CYBERDEF_OFICIAL)