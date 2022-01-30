---
title:  "Reputação negativa"
date:   1996-01-01
categories:
  - Artigo
tags:
  - Reputação
author:
  - Nick Szabo
---
```
Traduzido por: Steffan Diorgy 
Revisado por: Cypherpunks Brasil
```
[```ver lista de contribuidores```](/about/#contribuidores)


<small>Nick Szabo</small>  

#### 1996  

===exibe no card daqui pra baixo===

Um problema importante e geral parece ser o de marcar uma fonte de comportamento negativo para reconhecimento futuro. A tag pode ser usada para informações negativas compartilhadas publicamente (por exemplo, classificações de crédito) ou mantidas em sigilo (por exemplo, matar arquivos). A fonte de comportamento pode ser não humana (por exemplo, reconhecer padrões de vírus para fins de verificação de vírus). Onde a fonte de comportamento é adaptável e interessada, ela tem um incentivo para falsificar a marcação: um devedor para mudar nomes para evitar pagar suas dívidas, um vírus para embaralhar seu padrão para evitar varredura, e assim por diante. Se a tag tiver uma reputação positiva maior (onde zero é a reputação de um recém-chegado), esse incentivo será perdido e o lado negativo da reputação - a falta de reputação - deve ser suportado.

Os sistemas de credenciamento digital podem facilitar esse tratamento negativo da reputação?

Reputação específica do serviço, também conhecida localmente, pode não ser capaz de realizar esse rastreamento de reputação negativa. Se um nym local acumular mais credenciais negativas do que positivas, ele pode simplesmente ser substituído por um nym local recém-chegado para este serviço, sem prejudicar o capital de reputação positivo dos nyms locais de outras fontes de comportamento. Fontes hostis podem continuamente falsificar novatos inocentes. As contrapartes perdem a capacidade de determinar um histórico de arquivos hostis de morte anterior, varredura de vírus, classificações de crédito, etc.

As [credenciais chaumianas](http://www.chaum.com/publications/Security_Wthout_Identification.html) também dão ao titular da credencial o controle sobre a transferência de credenciais entre seus nyms locais, criando um incentivo para mostrar credenciais positivas e ocultar as negativas. Para remediar isso, as contrapartes podem exigir "credenciais não-negativas" (em uma forma como "Alice em muitas transações registradas por mim na área X nunca fez coisas ruins x, y, z"), credenciais não-negativas são limitadas para áreas que podem ser bem controladas. Uma delas pode ser a classificação de crédito, desde que uma esteja fazendo a maior parte das transações de crédito através de nyms locais ligados a uma pessoa.

Onde as credenciais de Chaumian são inaplicáveis, podemos aumentar o custo de entrada para ser maior do que o de um recém-chegado. Isso nos dá dois pontos de reputação claramente definidos para comparar em uma escala bastante subjetiva: limite de participação e reputação de recém-chegado. Ambos são subjetivos no olho da parte que escolhe se quer ou não participar de uma atividade com o nym.

Um limiar de participação maior do que a reputação de recém-chegados se choca com o objetivo desejável, que é capaz de fazer um novo começo. Aliás, a menos que os nyms anteriores e suas reputações positivas estejam ligadas a seus novos nyms, os pioneiros não podem começar, de modo que a própria instituição não possa ser iniciada. O mesmo vale para o crescimento institucional.

Tags que agrupam os resultados de uma ampla variedade de transações - nyms globais, também conhecidos como IDs universais, também conhecidos como "Nomes Verdadeiros" - parecem fornecer o maior incentivo para que as partes carreguem suas credenciais negativas. A maioria das pessoas acumulou reputação positiva suficiente em algumas áreas que é quase impossível para eles começarem suas vidas inteiras como recém-chegados.

Um grande problema surge com credenciais negativas quando elas são usadas, não apenas para evitar a participação em uma atividade específica com uma parte, mas para retaliação contra essa parte. A retribuição pode tomar alguma forma on-line não violenta, como calúnia, ataque de negação de serviço e assim por diante, mas a forma mais preocupante de retribuição é um ataque físico violento. Poderíamos ter marcas digitais que, enquanto rastreavam fontes de comportamento negativo no mundo digital, permanecessem estritamente desvinculadas de qualquer tipo de dados de localização física? Infelizmente, temos vários sistemas importantes, como telefones celulares, endereços de envio, etc., que fornecem essa ligação.

A questão pode ser a de decidir quais destas três dimensões são mais importantes e como podem ser trocadas:

*   Os ganhos a serem obtidos de rastreamento e, assim, evitar fontes de comportamento negativo
*   Os ganhos a serem obtidos a partir de um mundo digital não violento (isto é, um reino virtual no qual qualquer ação digital não pode ter consequências fisicamente violentas).
*   A inconveniência (e talvez impraticabilidade) de particionar os mundos físico e digital em diferentes sistemas de ID (mais realisticamente, algum subconjunto "puro" do mundo digital completamente particionado a partir de dispositivos de localização, informações físicas de envio, etc.)

Tenha em mente também que, na prática, elas são avaliadas principalmente por um mercado que evolui de seu estado atual, e não por filosofias éticas abstratas.

Robin Hanson observou que, em um mundo de nyms globais, o uso de um nym local pode sinalizar a ocultação de credenciais negativas, de modo que o uso de nyms globais esteja em equilíbrio. Um outro problema com os nyms locais é que nossos relacionamentos muitas vezes não são perfeitamente compartimentáveis ​​em tipos de serviço padrão, e até onde eles estão, gostaríamos de expandi-los em novas áreas. Sugiro que, no mínimo, vamos querer revelar progressivamente mais nyms locais às nossas contrapartes, à medida que nossos relacionamentos com eles se tornarem mais próximos e mais coexpostos.

Enquanto o equilíbrio nym global pode manter por muitos de nossos relacionamentos, pode haver muitas áreas onde os benefícios da [privacidade](http://szabo.best.vwh.net/smart_contracts_glossary.html#privity) de localizar nyms superam os custos de ser menor ou incapaz de diferenciar os recém-chegados de inimigos. (Por "prividade" eu me refiro a toda a tarefa geral de proteger as relações de terceiros hostis; confidencialidade e proteção de propriedade contra roubo são dois exemplos de privacidade). Por exemplo, o serviço de rastreamento de preferências em www.firefly.com aumenta a participação por meio do uso de pseudônimos e sofre pouca exposição de hostis. Por outro lado, as transações de crédito normalmente exigem informações de identificação, porque a exposição contratual normalmente supera os benefícios da privacidade.

As chaves públicas globais da nym, que têm muitas desvantagens em termos de privacidade, podem ser a melhor maneira de rastrear a reputação negativa, mas não são uma panacéia. Há um enigma importante em um sistema de chaves baseado em ID: o conflito entre a capacidade de obter uma nova chave quando a antiga é ou pode ser abusada por outra (revogação da chave) e a capacidade de outra ter certeza de estar lidando com ela. com a mesma pessoa novamente. Isso também pode oferecer uma oportunidade para as partes revelarem seletivamente credenciais positivas e ocultarem as negativas. Por exemplo, uma pessoa com uma classificação de crédito ruim pode revogar a chave sob a qual essa classificação é distribuída e criar uma nova, enquanto atualiza seletivamente suas credenciais positivas para a nova chave (por exemplo, fazer com que sua alma mater crie um novo diploma). [Autoridades](http://szabo.best.vwh.net/authorities.html) de revogação de chave podem combinar forças com agências de classificação de crédito para evitar esse apagamento da história negativa, mas isso lhes dá um controle ainda mais centralizado - não apenas sobre identidades, mas sobre importantes elementos de reputação associados a esses documentos. Isso viola ainda mais os princípios da separação de poderes e da segregação de funções, proporcionando uma oportunidade adicional para a emissão fraudulenta ou revogação de identidades, juntamente com a comunicação fraudulenta de informações de reputação.

A chave universal (não criptográfica) universal nos EUA, o SSN, é muito difícil de revogar. Muito mais fácil mudar seu nome. Essa política provavelmente não é um acidente, já que a maior vitória econômica da identificação global de nim é o rastreamento de reputações negativas, que a revogação pode derrotar. Enquanto o SSN for uma chave de banco de dados compartilhada, não usada com a finalidade de identificar com segurança uma transação sem rosto, há pouca necessidade de revogação além do apagamento indesejado do histórico negativo. Combinar uma chave de autenticação secreta, que deve ser revogável, com uma ID universal pública é bastante problemática.

* * *

Por favor, envie seus comentários para nszabo@law.gwu.edu

Direito autoral © 1996 por Nick Szabo  
Permissão para redistribuir sem alteração previamente concedida.


---
Fonte: [Negative Reputation - Nick Szabo](https://nakamotoinstitute.org/negative-reputation/)