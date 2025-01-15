---
id: 899
title: Adicionar paginador no Modal jQuery.FancyBox
date: 2011-05-09T09:49:18+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=899
permalink: /jquery/adicionar-paginador-fancybox/
dsq_thread_id:
  - "2101120190"
categories:
  - jQuery
tags:
  - plugin
---
Salve galera !!

&#8216;De bobeira&#8217; por aqui, aproveitei o tempo para estudar um pouco do fancybox.

É uma ótima opção de modal, e possui uma <a href="http://fancybox.net/api" target="_blank">API bem clara</a>, e de fácil utilização.

O callback, nos possibilita fazer mágica. Desenvolvi um script rápido, aproveitando o método publico **jQuery.fancybox.pos()**, para criar um paginador entre as fotos da galeria.

<!--more-->



Usei o **titleFormat**: <a href="http://fancybox.net/blog" target="_blank">http://fancybox.net/blog</a>.

``` js
function formatTitle(title, currentArray, currentIndex, currentOpts) {
    return '<div id="tip7-title"><span class="fb_pager">'+pager( currentArray, currentIndex )+'Imagem ' + (currentIndex + 1) + ' de ' + currentArray.length + '</span><span><a href="javascript:;" onclick="$.fancybox.close();"><img src="/data/closelabel.gif" /></a></span>' + (title && title.length ? '<p>' + title + '</p>' : '' ) + '</div>';
}
function pager( currentArray, currentIndex ){
  var p = '<p class="pageItem">';
  for( var i=1; i<=currentArray.length; i++ )
  {
    var active = ( currentIndex==(i-1) ) ? 'class="active"' : ''
    p += '<a href="#" rel="'+(i-1)+'"'+active+'>'+i+'</a>';
  }
  return p+'</p>';
}
jQuery(document).ready(function(){
  jQuery('.pageItem a').live('click', function( e ){
    e.preventDefault();
    jQuery.fancybox.pos( jQuery( this ).attr('rel') );
  });
});
```

Esse é o código adicional, e então no momento de instanciar o plugin, basta declarar que vamos usar o callback, e a function que deverá ser chamada:

``` js
jQuery('.gallery').fancybox({
    titleFormat     :       formatTitle
  });
```

é isso. =)
