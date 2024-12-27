---
id: 1070
title: Atrelar evento em elementos que não existiam no DOM
date: 2011-05-31T01:18:51+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1070
permalink: /ajax/atrelar-evento-em-elementos-nao-existiam-dom/
dsq_thread_id:
  - "2104895113"
categories:
  - AJAX
tags:
  - dom
---
Salve salve galera !!

Bom, eu já havia postado como carregar [conteudo com ajax, apenas com javascript puro](https://wbruno.com.br/ajax/carregando-conteudo-ajax-trocando-url-jquery/).

Porém, se junto com o **xmlHttp.responseText**, vierem alguns links, eles não terão o evento onclick, atrelados. Pois nós fizemos o &#8216;bind&#8217; da function no window.onload, e nossos novos elementos foram trazidos muito depois desse instante.

<!--more-->

Para entendimento, rode esse script isoladamente:

``` html
<html>
<head>
  <script type="text/javascript">
  window.onload = function(){
    id('teste').innerHTML = '<span id="ae">aeee</span>';

    attach( id('ae'), teste );
  }

  function attach( el, f ){
    if( window.addEventListener )
      el.addEventListener("click", f, false);
    else
      el.attachEvent("click", f );
  }
  function id( el ){
    return document.getElementById( el );
  }
  function teste(){
    alert( 'ae' );
  }
  </script>
</head>
<body>
  <div id="teste"></div>
</body>
</html>
```

Entendeu oque fizemos ?

Criamos uma tag <a> dentro da div#teste com javascript. E logo depois de criar, nos fizemos o bind do evento.

Precisaremos do mesmo para &#8216;dar vida&#8217; aos nossos novos elementos que trouxemos com ajax.

``` js
var as = id('content').getElementsByTagName('a');
      for( var i=0; i<as.length; i++ ){
        var arq = pega_arq( as[i].href );
        if( window.addEventListener )
          as[i].addEventListener( 'click', function(){ abre( arq ); }, false );
        else
          as[i].attachEvent( 'click', function(){ abre( arq ); } );
      }
```

Note que primeiro guardamos apenas os nossos &#8216;novos links&#8217; (os que estiverem dentro da div#content), na variavel as.

depois com um loop for(), iteramos por essas tags <a>, e vamos uma a uma, adicionando no evento **onclick** a function **abre()**, responsável pela requisição ajax.

``` js
as[i].addEventListener( 'click', function(){ abre( arq ); }, false );
```

Aqui, usamos uma function anônima, pois queremos que a **arq()** só seja executada, no evento onclick.

## <a href="http://wbruno.com.br/scripts/ajax/" target="_blank">Demonstração Online</a>
