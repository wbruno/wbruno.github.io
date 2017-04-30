---
id: 3422
title: Slideshow controlado pelo play e pause de uma música
date: 2015-06-07T14:58:03+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3422
permalink: /javascript-puro/slideshow-controlado-pelo-play-e-pause-de-uma-musica/
videourl:
  - ""
categories:
  - Javascript
---
<img src="/wp-content/uploads/2015/06/music-slide.png" alt="music-slide" width="870" height="358" class="aligncenter size-full wp-image-3423" srcset="/wp-content/uploads/2015/06/music-slide.png 870w, /wp-content/uploads/2015/06/music-slide-300x123.png 300w, /wp-content/uploads/2015/06/music-slide-788x324.png 788w" sizes="(max-width: 870px) 100vw, 870px" />

<!--more-->

Com a tag <audio> do html5, temos uma API JavaScript para manipular e ouvir os eventos dos controles do player. Quando a música inicia, as cores trocam. No pause, elas param, e no play elas tocam novamente, até o fim da música, quando tudo para. Bem simples, não ?

<pre>&lt;script>
(function(){
  'use strict';

  var $music = document.getElementById('music'),
      $items = document.getElementById('slide').querySelectorAll('.item'),
      itemsQuantity = $items.length;

  $items = [].slice.call($items);

  var i = 0;
  var itv;
  var SLIDE_TIME = 800;

  var start = function() {
    //..
  };

  $music.addEventListener('ended', function(event) {
    console.log('ended');
    clearInterval(itv);
  });
  $music.addEventListener('pause', function(event) {
    console.log('pause');
    clearInterval(itv);
  });
  $music.addEventListener('playing', function(event) {
    console.log('playing');
    itv = setInterval(start, SLIDE_TIME)
  });

}());
&lt;/script></pre>

Veja como implementei isso:

## Código

<https://github.com/wbruno/examples>

## Demonstração

<http://wbruno.github.io/examples/music-slide/>
