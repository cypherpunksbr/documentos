---
title:  "Composições Algorítmicas"
date:   2013-12-29
categories:
   - Artigo
tags:
  - criptografia
  - tutorial
  - segurança
author:
  - Isis Agora Lovecruft
---
```
Traduzido por: Vinicius Yaunner 
Revisado por: Cypherpunks Brasil
```
[```ver lista de contribuidores```](/about/#contribuidores)


## Isis Agora Lovecruft

Por muito tempo, não consegui descobrir para que servia o Twitter. Não tenho certeza se descobri isso ainda. Parece conveniente postar links para *white papers* de física e criptografia que li e, em seguida, receber um feedback fútil padrão da Internet  de pessoas de quem nunca ouvira falar.

Em um ponto, porque eu não conseguia descobrir o que fazer com o Twitter, decidi lançar um álbum bytebeat por meio de tweets. Já vi pessoas tweetarem links para suas novas músicas ou álbuns, ou o que quer que seja — isso é ridículo.

Então, comecei a criar composições algorítmicas em menos de 140 caracteres em python. O álbum, *fuck_your_bits*(hashtag = '# fyb'), está quase pela metade, mas meus amigos **[Moxie](https://moxie.org/)** e **[Emblem](https://twitter.com/emblem__)** apontaram que a função de busca por hashtags no Twitter não apenas indexaria as músicas do meu álbum nas últimas três semanas, mas também que os tweets na minha linha do tempo foram retirados da vista do público após um certo número de meses, dependendo de algum número indeterminado de outros algoritmos que calculavam a “popularidade do tweet”.

Porque as pessoas pedem o álbum completo, aqui está. Eu ainda vou continuar tweetando, porque a única outra coisa útil que posso pensar que cabe de forma impressionante em menos de 140 bytes é o shellcode.

~~~
python -c'import sys;[sys.stdout.write(chr((~t&t>>3^(((t>>((t>>11)%7+6))%15)*t))%256))for t in xrange(2**19)]'|aplay

python -c'import sys;[sys.stdout.write(chr(((~t>>2)*(2+(42&t*((7&t>>10)*2))<(24&t*((3&t>>14)+2))))%256))for t in xrange(2**18)]'|aplay

python -c'import sys;[sys.stdout.write(chr((((t*5&t>>7|t*9&t>>4|t*18&t/1024)|((t|7)>>5|(t|4)>>9)))%256))for t in xrange(2**18)]'|aplay

python -c'import sys;[sys.stdout.write(chr(((~t>>2)*((127&t*(7&t>>9))<(245&t*(4-(7&t>>13)))))%256))for t in xrange(2**20)]'|aplay -c 2 -r4444

python -c'import sys;[sys.stdout.write(chr((~t>>5>>(127&t*9&~t>>7<42&t*23^5&~t>>13)+3)%256))for t in xrange(2**18)]'|aplay -c2 -r2222

python -c'import sys;[sys.stdout.write(chr((((t>>(2|4)&((t%0x7369)|4|11|5))+(7|4|42)&t))%256))for t in xrange(2**18)]'|aplay -c2 -r4444

python -c'import sys;[sys.stdout.write(chr((((t*(t>>13|t>>8)|(t>>16)-t)-64))%256))for t in xrange(2**18)]'|aplay -r4444

python -c"import sys;[sys.stdout.write(chr(((0x7BB3+t>>11|(t>>(2|5)^(1515|42))|~t)|(2*t)>>6)%256))for t in xrange(2**20)]"|aplay -c2

x="if(t%2)else";python3 -c"[print(t>>15&(t>>(2$x 4))%(3+(t>>(8$x 11))%4)+(t>>10)|42&t>>7&t<<9,end='')for t in range(2**20)]"|aplay -c2 -r4
~~~