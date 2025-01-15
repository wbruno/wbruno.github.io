---
id: 2589
title: 'Cortando uma string nos primeiros &#8220;N&#8221; caracteres - JavaScript com Expressão Regular'
date: 2012-08-20T17:56:52+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2589
permalink: /expressao-regular/cortando-uma-string-nos-primeiros-n-caracteres-javascript-com-expressao-regular/
dsq_thread_id:
  - "2102376230"
categories:
  - Expressão Regular
---
Vou usar expressão regular com javascript, para mostrar como cortar uma string nos &#8220;N&#8221; primeiros caracteres.

Eu poderia usar a função .substr(), mas ai não teria graça.. hehe

<!--more-->



Fiz aqui rapidinho uma brincadeira para cortar uma frase nos primeiros 9 caracteres.

Fazendo a string:

``` html
<h1 id="title">Um titulo bem grande cheio de palavras esquisitas</h1>
```

Ser mostrada apenas como:

``` html
<h1 id="title">Um titulo...</h1>
```
E ao clicar, mostra a frase completa. Alternando cada clique, mostrando truncado e mostrando completo.

``` html
<html>
<head>
  <meta charset="utf8" />

  <script type="text/javascript">
  function id( el ){
    return document.getElementById( el );
  }
  String.prototype.truncate = function( max ){
    var er = new RegExp( "(^[\\w\\s]{"+max+"})(.*)$" );
    return this.replace( er,'$1' );
  }
  window.onload = function(){
    var $t = id('title');
    var strtitle = $t.innerHTML;

    $t.title = strtitle;
    $t.innerHTML = strtitle.truncate( 9 )+'...';

    $t.onclick = function(){
      this.innerHTML = this.innerHTML.length==12 ? this.title : this.title.truncate( 9 )+'...';

    }
  }
  </script>
  <style type="text/css">
  #title { cursor: pointer; }
  </style>
</head>
<body>
  <h1 id="title">Um titulo bem grande cheio de palavras esquisitas</h1>

</body>
</html>
```

Note que fiz 2 grupos na expressão regular. O primeiro grupo casa os &#8220;N&#8221; primeiros caracteres(letras simbolos e espaços <var>\w\s</var>), e o segundo grupo casa tudo oque vier depois(<var>.*</var>), em qualquer quantidade.

O replace troca tudo, pelo o que foi casado no primeiro grupo.

Dessa forma consigo o &#8220;efeito&#8221; de cortar depois dos &#8220;N&#8221; primeiros caracteres.

Caso tudo e coloco de novo os &#8220;N&#8221; primeiros.

Este post, é o primeiro exemplo prático do [Expressões Regulares – REGEX para iniciantes](https://wbruno.com.br/expressao-regular/expressoes-regulares-regex-para-iniciantes/).

## O método substr()

Fiz com ReGex, o mesmo que eu conseguiria com o **substr()**:

``` js
return this.substr( 0, max );
```

É isso galera. Por enquanto bem básico, mas me digam se está sendo fácil entender o que são, o tão temido mundo da expressão regular.
