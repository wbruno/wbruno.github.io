---
id: 2763
title: Como remover máscaras com Expressões Regulares
date: 2012-10-30T07:00:15+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2763
permalink: /expressao-regular/como-remover-mascaras-com-expressoes-regulares/
dsq_thread_id:
  - "2101168248"
categories:
  - Expressão Regular
tags:
  - máscara
---
Para entender Expressões Regulares, é preciso conseguir enxergar os padrões das strings.

Um telefone possui o seguinte padrão:

<var>(xx) xxxx-xxxx</var> ou no caso de São Paulo(neste momento): <var>(xx) 9xxxx-xxxx</var>
  
Sendo cada x, um número 1,2,3,4,5,6,7,8 ou 9.

Eu posso escrever uma ER que case com os telefones assim:

``` js
([0-9]{2}) 9?[0-9]{4}-[0-9]{4}
```

Sendo o 9 ali &#8220;opcional&#8221;. Para remover a máscara de números de telefone, posso procurar quais são os caracteres que não quero, e tirá-los:

``` js
str.replace('(','').replace(')', '').replace(' ','').replace('-','');
```

Mas isso é deveras trabalhoso.

Eu poderia fazer uma Expressão Regular para pegar todos esses caracteres e remover eles:

``` js
str.replace(/[\(\)\.\s-]+/g,'');
```

Mas ai, tb ainda não tá bacana.

Posso pensar ao contrário: remover tudo, menos oque eu quero:

``` js
str.replace(/[^0-9]+/g,'');
```

Ou seja, removo tudo oque não for números de 0 até 9. Ou se preferir: <var>/[\D]+/g</var> == <var>/[^\d]+/g</var>

Lembrando que **\d** é o mesmo que [0-9].