---
id: 1602
title: 'Abrir modal do tuto do maujor, automaticamente ao carregar a página - jQuery'
date: 2011-11-22T13:59:30+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1602
permalink: /jquery/abrir-modal-tuto-maujor-automaticamente-ao-carregar-pagina-jquery/
dsq_thread_id:
  - "2100755657"
categories:
  - jQuery
tags:
  - modal
---
Bom, vira e mexe, alguém aparece no fórum perguntando, como fazer para o modal deste tutorial:

<a href="http://www.maujor.com/blog/2009/04/16/janela-modal-com-jquery/" target="_blank">http://www.maujor.com/blog/2009/04/16/janela-modal-com-jquery/</a>,

abrir automaticamente, ao carregar a página.

<!--more-->



Por esse motivo, estou criando este post, para deixar aqui, uma forma de fazer isso, e assim evitar que eu precise me repetir toda vez que alguém perguntar.

O primeiro passo, é encapsular a rotina em uma função:

``` js
function open_modal( id ){
  var maskHeight = $(document).height();
  var maskWidth = $(window).width();

  $('#mask').css({'width':maskWidth,'height':maskHeight});

  $('#mask').fadeIn(1000);
  $('#mask').fadeTo("slow",0.8);

  //Get the window height and width
  var winH = $(window).height();
  var winW = $(window).width();

  $(id).css('top',  winH/2-$(id).height()/2);
  $(id).css('left', winW/2-$(id).width()/2);
  $(id).fadeIn(2000);
};
$(document).ready(function() {

  $('a[name=modal]').click(function(e) {
    e.preventDefault();
    open_modal( $(this).attr('href') );
  });

  $('.window .close').click(function (e) {
    e.preventDefault();

    $('#mask').hide();
    $('.window').hide();
  });

  $('#mask').click(function () {
    $(this).hide();
    $('.window').hide();
  });
});
```

Feito isso, tudo continua funcionamento normalmente.. assim como era.

E para abrir automaticamente, podemos chamar então essa função que criei:

``` js
open_modal( '#dialog' );
```

Ficando então, assim o código completo:

``` js
function open_modal( id ){
  var maskHeight = $(document).height();
  var maskWidth = $(window).width();

  $('#mask').css({'width':maskWidth,'height':maskHeight});

  $('#mask').fadeIn(1000);
  $('#mask').fadeTo("slow",0.8);

  //Get the window height and width
  var winH = $(window).height();
  var winW = $(window).width();

  $(id).css('top',  winH/2-$(id).height()/2);
  $(id).css('left', winW/2-$(id).width()/2);
  $(id).fadeIn(2000);
};
$(document).ready(function() {

  $('a[name=modal]').click(function(e) {
    e.preventDefault();
    open_modal( $(this).attr('href') );
  });

  open_modal( '#dialog' );//abrindo o div#modal ao carregar a página

  $('.window .close').click(function (e) {
    e.preventDefault();

    $('#mask').hide();
    $('.window').hide();
  });

  $('#mask').click(function () {
    $(this).hide();
    $('.window').hide();
  });
});
```
