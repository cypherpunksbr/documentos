---
title:  'Criptografia de Ponta-a-Ponta 101'
date:   2017-03-08
categories:
  - Artigo
tags:
  - Criptografia
  - Vigilância
  - Privacidade
  - Segurança
author:
  - Elle Armageddon
description: 'Neste artigo, damos uma introdução aos princípios da Criptografia, explicando a importância de seu uso no cotidiano e no que devemos nos atentar ao utilizá-la'
---

```
Tradução por: Cypherpunks Brasil
Revisão: Vinicius Yaunner
```

[```ver lista de contribuidores```](/about/#contribuidores)

# Introdução à Criptografia Ponta-a-Ponta

## E será que as Revelações do Vault 7 Significam que Criptografia é Inútil?

Se você usou a internet em qualquer ponto desde Maio de 2013, você provavelmente ouviu que deveria usar comunicações criptografadas. As revelações de Edward Snowden de que a Agência Nacional de Segurança (NSA, em inglês) registra todas nossas chamadas, mensagens e e-mails, foram a faísca para um surto no desenvolvimento e uso de apps e serviços de criptografia. Após apenas poucos anos, criptografia passou a ser amplamente utilizada para comunicação diária. Se você usa alguma dessas ferramentas criptográficas, você provavelmente também ouviu a frase "criptografia ponta-a-ponta", ou sua sigla, em inglês, "E2EE" (end-to-end encryption). O nome parece claro o suficiente: ponta-a-ponta significa que o conteúdo é criptografado de uma extremidade (geralmente seu celular ou computador) à outra extremidade (o celular ou computador do destinatário intencional da mensagem). Mas qual o nível de segurança é prometido a você, o usuário?

Desde o início da administração do Trump, a Alfândega e Proteção de Fronteiras dos EUA (CBP, sigla em inglês) tem intensificado a invasão da privacidade de viajantes. O CBP tem demandado que, tanto os cidadãos dos EUA, quanto os visitantes, desbloqueiem seus celulares e computadores e os entreguem para a inspeção do CBP. Eles também têm demandado que os viajantes providenciem senhas ou que loguem em suas redes sociais. Viajantes que não colaboram se deparam com a ameaça de serem proibidos de entrar.

Ontem, o Wikileaks publicou um "baú do tesouro" de documentos vazados da CIA (Agência Central de Inteligência dos EUA), incluindo o conhecimento desta sobre vulnerabilidades de segurança e métodos de exploração que a CIA pagou para manter em segredo, escondidos do público geral. Agora que esta informação vazou, não é apenas a CIA que tem acesso essas informações - todo mundo tem. O New York Times e outros jornais reportaram o ocorrido de forma equivocada, dizendo que a CIA havia quebrado a criptografia de aplicativos como Signal e WhatsApp, quando na verdade o que a CIA fez foi direcionar os ataques e comprometer dispositivos Android de pessoas específicas.

Em suma, essa revelação confirma a importância de usar comunicações criptografadas ponta-a-ponta, que impedem agentes estatais de fazerem varreduras de vigilância em larga escala. Criptografia ponta-a-ponta (E2EE) continua sendo importante.

> Muitas reportagens sobre o Vault 7 deram a impressão de que apps criptográficos, como o Signal, foram comprometidos. Na verdade, o comprometimento ocorreu no nível do dispositivo - na extremidade (endpoint) da comunicação criptográfica, não na criptografia em si. Não há qualquer motivo para se acreditar que a criptografia em si não funciona.

### Limitações: Extremidades em Texto Simples

Primeiramente, é importante entender que, se você consegue ler a mensagem, ela é um texto simples - ou seja, um texto que não está mais criptografado. Com a criptografia ponta-a-ponta, os elos fracos da corrente da segurança são: você (emissor) e seu dispositivo, o destinatário e o dispositivo dele. Se o destinatário consegue ler sua mensagem, qualquer um com acesso ao dispositivo dele também consegue. Um policial disfarçado poderia ler sua mensagem por sobre os ombros do destinatário, ou a polícia poderia confiscar o dispositivo do destinatário e forçar o acesso a ele. Se houver qualquer risco de qualquer destes eventos infelizes acontecerem, você deveria pensar duas vezes antes de enviar qualquer coisa que não gostaria de compartilhar com as autoridades.

Essa limitação particular também é relevante para as recentes revelações do [“Vault 7”,](https://pt.wikipedia.org/wiki/Vault_7) que demonstram como apps como Signal, WhatsApp e Telegram podem não ser úteis, caso um adversário (como a CIA) venha a obter acesso físico ao seu dispositivo, ou ao dispositivo do destinatário, e seja capaz de desbloqueá-lo. Muitas reportagens sobre o Vault 7 têm sido um tanto enganosas, dando a impressão que os apps por si só foram comprometidos. Neste caso, o comprometimento foi no nível do dispositivo - na extremidade (endpoint) da comunicação criptografada. A criptografia, por si própria, continua boa.

### Limitações: Vigilância Direcionada

Considerando que você não consegue controlar as condições de segurança do destinatário da sua mensagem, você deve considerar a possibilidade de que qualquer mensagem que você envia pode ser lida. Embora raros, existem casos de [poderes estatais visando pessoas através da vigilância direta.](https://www.vice.com/en/article/3da5qj/government-hackers-iphone-hacking-jailbreak-nso-group) Nestes casos, os alvos podem estar trabalhando com dispositivos infectados com malware, com a intenção de registrar toda comunicação que está entrando e saindo do dispositivo. Este comprometimento funciona no nível da extremidade da comunicação (dispositivo), tornando E2EE (criptografia ponta-a-ponta) inútil contra esses adversários em específico. Pois é difícil saber se você (ou o destinatário da sua mensagem) é alvo deste tipo de ataque, e é sempre bom ter como padrão não enviar informações muito sensíveis através de meios digitais de comunicação. Atualmente, tais ataques parecem ser raros, mas uma pessoa nunca deve correr riscos desnecessariamente.

### Limitações: Metadados

A terceira coisa que você precisa saber sobre E2EE é que ela não necessariamente protege seus metadados. Dependendo de como a comunicação é transmitida, registros (logs) ainda podem mostrar a hora e o tamanho da comunicação, assim como o remetente e o destinatário. Registros (logs) também podem mostrar a localização de ambos o remetente e o destinatário, no momento da comunicação. Mesmo embora isso, por si só, possa não ser tipicamente suficiente para mandar alguém para a prisão, isso pode ser útil para provar associações entre pessoas, estabelecendo proximidade com cenas de crime, e rastreando padrões de comunicação. Todos os pedaços de informações são úteis para estabelecer maiores padrões comportamentais, em casos de vigilância direta.

### Então... Por quê?

Então, se criptografia ponta-a-ponta não necessariamente protege o conteúdo de suas comunicações, e ainda por cima entrega metadados úteis, qual o ponto em utilizá-la?

Uma das coisas mais importantes que a E2EE faz, é garantir que seus dados nunca passarão por servidores de terceiros de forma legível. Desde que a criptografia ponta-a-ponta comece no momento que você clica em "enviar", e persiste até que chegue ao dispositivo do destinatário, quando uma empresa - como a Meta (Facebook) - é intimada a entregar os registros (logs) de suas comunicações, eles não possuem nenhum conteúdo em texto simples para entregar. Isso põe as autoridades numa posição na qual, se eles quiserem obter o conteúdo das suas comunicações, eles são forçados a gastar uma quantidade significativa de tempo e recursos tentando quebrar a criptografia. Nos EUA, seu direito a um julgamento célere pode tornar esta prova inútil para os procuradores, os quais podem não conseguir quebrar a criptografia rápido o suficiente para agradar ao juiz.

### Vigilância em Massa

Outro uso de criptografia ponta-a-ponta é tornar mais difícil a vigilância em massa da Agência Nacional de Segurança (dos EUA, sigla NSA, em inglês), dentre outras agências de aplicação da lei. Por não existir nenhum ponto intermediário no qual sua comunicação não-criptografada pode ser interceptada, o que é interceptado são os mesmos blocos de texto criptografados disponíveis numa intimação. Vigilância em massa é geralmente conduzida coletando-se quaisquer dados disponíveis e submetendo-os a um sistema automatizado de classificação, ao invés de submetê-los a análises individuais. O uso de criptografia previne contra uma peneiração algorítmica por conteúdo, portanto tornando este processo muito mais difícil, e que geralmente não vale a pena.

### Stingrays (arraias, em tradução literal)

Além da coleta de dados da NSA, agências federais e estaduais de aplicação da lei por todo o país (EUA) possuem, e frequentemente usam, simuladores de torres de telefonia celular, conhecidos como "IMSI catchers" (Captador Internacional de Identidade de Assinantes Móveis), ou "Stingrays" (arraias). IMSI Catchers se passam por torres de telefonia celular, a fim de enganar seu celular, para que ele entregue informações de identificação do mesmo, incluindo sua localização. Simuladores de torres de telefonia celular também interceptam e registram suas comunicações. Assim como com outros métodos de interceptação, criptografia significa que aquilo que é obtido seja altamente inutilizável, a não ser que a agência de aplicação da lei queira enfrentar o problema de quebrar essa criptografia.

### Criptografia em Repouso

Além de utilizar criptografia ponta-a-ponta para proteger o conteúdo de suas mensagens enquanto estão sendo enviadas, você pode usar a criptografia total de seu disco rígido para proteger suas informações enquanto estão armazenadas em seu dispositivo. Uma criptografia de disco apropriada significa que toda informação em seu dispositivo é indecifrável sem sua chave de criptografia (geralmente uma frase-passe), criando uma extremidade (endpoint) rígida na comunicação, muito mais difícil de ser comprometida. Mesmo embora criptografar as extremidades (endpoints) não seja necessariamente uma proteção contra alguns dos métodos mais pérfidos de vigilância, como malware, isso pode prevenir adversários que obtiverem seus dispositivos de extrair quaisquer dados úteis dos mesmos.

---

Criptografia ponta-a-ponta não é, de forma alguma, um escudo mágico contra a vigilância feita por nações, estados ou indivíduos maliciosos, mas o Vault 7 destaca como sua utilização pode ajudar a forçar uma mudança processual de uma vigilância em massa, para ataques direcionados com uso intensivo de recursos. Quando emparelhada com bom senso, dispositivos encriptados, e outras práticas de segurança, criptografia ponta-a-ponta pode ser uma ferramenta poderosa para reduzir significativamente sua superfície de ataque. O uso habitual e consistente desta, pode anular muitas das ameaças de baixo nível, e pode até mesmo fazer com que adversários de mais alto nível decidirem que atacar você simplesmente não vale o esforço.

#### Leituras Adicionais

* [Deserting the Digital Utopia](https://crimethinc.com/2013/10/04/feature-deserting-the-digital-utopia)

* [Prism: The Internet as New Enclosure](https://crimethinc.com/2013/06/10/prism-the-internet-as-new-enclosure)

* [The Internet as New Enclosure](https://crimethinc.com/2013/06/10/the-internet-as-new-enclosure)

---

Fonte: https://crimethinc.com/2017/03/08/end-to-end-encryption-101-what-does-e2ee-do-and-does-vault-7-mean-its-useless
