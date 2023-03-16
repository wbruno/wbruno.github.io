---
id: 3061
title: Como fazer menu fixo apartir de certa rolagem da página
date: 2013-08-10T08:58:54+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3061
permalink: /javascript-puro/como-fazer-menu-fixo-apartir-de-certa-rolagem-da-pagina/
dsq_thread_id:
  - "2100787842"
categories:
  - Javascript
---
Dois caras perguntaram isso no fórum essa semana, e eu mesmo precisei fazer em um trabalho meu.

[<img src="/wp-content/uploads/2013/05/js-logo.jpg" alt="js-logo" width="800" height="341" class="aligncenter size-full wp-image-2978" srcset="/wp-content/uploads/2013/05/js-logo.jpg 800w, /wp-content/uploads/2013/05/js-logo-300x127.jpg 300w" sizes="(max-width: 800px) 100vw, 800px" />](/wp-content/uploads/2013/05/js-logo.jpg)

<!-- more -->

Então lá vai.

O evento é o **window.onscroll**, pois até que o **position: sticky;** saia do rascunho da w3c, não temos nada &#8220;de graça&#8221; e pronto para fazer isso.

Então escutamos no evento onscroll, a posição atual da página, e ai, se chegar a ser maior que tal valor, podemos aplicar oque precisamos.

## Em javascript puro

Bem simples:

``` js
window.onscroll = function(){
   var top = window.pageYOffset || document.documentElement.scrollTop
   if( top > 300 ) {
       console.log('Maior que 300');
   }
}
```

## Em jQuery

Apenas caso vc já esteja com a lib incorporada, pois não vale nenhum pouco a pena coloca-la apenas por causa disso:

``` js
var $w = $(window);

$w.on("scroll", function(){
   if( $w.scrollTop() > 300 ) {
       console.log('Maior que 300');
   }
});
```

É isso! comentem caso usem!
