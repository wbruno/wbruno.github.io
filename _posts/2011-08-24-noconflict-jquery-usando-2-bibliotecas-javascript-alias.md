---
id: 1352
title: 'noConflict jQuery - Usando 2 bibliotecas javascript [ alias $ ]'
date: 2011-08-24T07:00:45+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1352
permalink: /jquery/noconflict-jquery-usando-2-bibliotecas-javascript-alias/
dsq_thread_id:
  - "2100728077"
categories:
  - jQuery
---
A maioria das bibliotecas javascript usam o símbolo $ como apelido das suas funções básicas.

O jQuery, disponibiliza naturalmente 2 formas de uso, com o $ e com a palavra jQuery.

<!--more-->

## Não existe conflito de jQuery + jQuery!

Se você tem um plugin que usa a lib jQuery, sei lá, um lightbox por exemplo. E depois precisa adicionar um tooltip que também usa a lib jQuery, **importe** apenas uma única vez a lib jQuery.

Tão simples quanto isso. Não existe conflito entre jQuery + jQuery. Apenas não importe 2 vezes a mesma lib, mesmo que em versões diferentes. Nesse caso, deixe apenas uma tag <script>, com um src para a lib, acima de todos os outros recursos(prefira usar sempre versões mais recentes), e pronto.

O método [.noConflict()](#noConflict), existe para conflitos **entre bibliotecas javascript diferentes**, como Prototype + jQuery, jQuery + MooTools..

## Como funciona o jQuery.noConflict() ? {##noConflict}

``` js
noConflict: function( deep ) {
    if ( window.$ === jQuery ) {
      window.$ = _$;
    }

    if ( deep && window.jQuery === jQuery ) {
      window.jQuery = _jQuery;
    }

    return jQuery;
  },
```

Note que a única coisa que esse método faz, é **retornar**, um objeto jQuery existente(já registrado no documento). Por isso, que a forma de usar, nos induz a _&#8216;trocar o nome&#8217;_ do apelido:

``` js
var $a = jQuery.noConflict()
```

E então, em vez de usar **$**, agora passo a usar **$a**

``` js
$a(document).ready(function(){
```

## $(&#8220;bla bla bla&#8221;) is null

Esse é o erro que aparecerá, caso vc tente primeiro usar jQuery, e depois prototype. Apenas a segunda lib vai funcionar, pois ela vai sobrescrever o uso do $.

## Resolvendo com noConflict()

Basta atribuir o novo objeto jQuery a um outro apelido, e usar ele então:

``` js
$a = jQuery.noConflict();
   $a(document).ready(function() {
    $a('#gallery a').lightBox();
  });
```

não sou muito fãn dessa forma de resolver, pois daria o trabalho de reescrever todo o script que dependesse de jQuery.. fora que não ficou &#8216;intuitivo&#8217; esse uso.

## Resolvendo apenas ao não usar o apelido $

No início deste post, eu disse que a lib disponibiliza também, a variável jQuery para ser usada.

``` js
jQuery(document).ready(function() {
  jQuery('#gallery a').lightBox();
});
```

Portanto, se sempre que eu tiver que fazer algo com jQuery, não usar o símbolo $, mas sim a variavel jQuery, não preciso me preocupar com conflito, pois apenas a outra lib, usaria o alias $.

## Resolvendo apenas passando um argumento

``` js
ready: function( fn ) {
    // Attach the listeners
    jQuery.bindReady();

    // Add the callback
    readyList.done( fn );

    return this;
  },
```

Esse é o trecho de código da lib, responsável pelo método .ready() que usamos, para aguardar o DOM carregar.

Note que o parâmetro do método é a nossa function anônima, que expliquei no post &#8216;<a href="https://wbruno.com.br/jquery/vixi-aprendi-jquery-mas-agora/" target="_blank">Aprendi jQuery, e agora?</a>&#8216;.

Oque posso fazer, é forçar um argumento $, e então me aproveitar da clousure, limitando o escopo do nosso alias:

``` js
jQuery(document).ready(function( $ ) {
  $('#gallery a').lightBox();
});
```

Bacana ne?! não precisei mecher em nada dentro do método .ready(), apenas iniciei ele com a variavel jQuery, e forcei a lib a me devolver o argumento $, como um objeto jQuery exclusivo desse escopo.

## Usando uma função anônima auto executável

Da mesma forma que a solução acima, eu poderia ter feito uma clousure, e:

``` js
(function( $ ){
     $(document).ready(function( $ ) {
      $('#gallery a').lightBox();
    });
  })(jQuery);
```

O parâmetro &#8216;para o mundo externo&#8217; a essa anônima, é **jQuery**, mas dentro dela, o argumento que recebo é um **$**. lindo não?

## [Demonstração Online](http://wbruno.com.br/scripts/noConflict.html)

É isso. Se vc conhece alguma outra forma, não entendeu, ou curtiu, comente. =)
