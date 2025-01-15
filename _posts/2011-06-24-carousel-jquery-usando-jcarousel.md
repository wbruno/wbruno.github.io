---
id: 1139
title: Carousel jQuery usando jCarousel
date: 2011-06-24T23:08:05+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1139
permalink: /jquery/carousel-jquery-usando-jcarousel/
dsq_thread_id:
  - "2101118297"
categories:
  - jQuery
tags:
  - carousel
  - plugin
---
Analisando o meu Analytics, **Carousel jQuery**, é a principal fonte de pesquisa, que trazem os visitantes ao meu site.

Portanto, vou deixar um exemplo de uso do plugin **jCarousel** aqui nesse post.

<!--more-->

Eu já havia mostrado como fazer um [Carousel usando o Cycle](https://wbruno.com.br/jquery/carousel-jquery-usando-cycle/), então fica tb a dica de como usar o plugin jCarousel.

O HTML bem simples:

``` html
<ul id="mycarousel" class="jcarousel-skin-tango">
  <li><img src="http://static.flickr.com/66/199481236_dc98b5abb3_s.jpg" width="75" height="75" alt="" /></li>
  <li><img src="http://static.flickr.com/75/199481072_b4a0d09597_s.jpg" width="75" height="75" alt="" /></li>
  <li><img src="http://static.flickr.com/57/199481087_33ae73a8de_s.jpg" width="75" height="75" alt="" /></li>
  <li><img src="http://static.flickr.com/77/199481108_4359e6b971_s.jpg" width="75" height="75" alt="" /></li>
  <li><img src="http://static.flickr.com/58/199481143_3c148d9dd3_s.jpg" width="75" height="75" alt="" /></li>
  <li><img src="http://static.flickr.com/72/199481203_ad4cdcf109_s.jpg" width="75" height="75" alt="" /></li>
  <li><img src="http://static.flickr.com/58/199481218_264ce20da0_s.jpg" width="75" height="75" alt="" /></li>
  <li><img src="http://static.flickr.com/69/199481255_fdfe885f87_s.jpg" width="75" height="75" alt="" /></li>
  <li><img src="http://static.flickr.com/60/199480111_87d4cb3e38_s.jpg" width="75" height="75" alt="" /></li>
  <li><img src="http://static.flickr.com/70/229228324_08223b70fa_s.jpg" width="75" height="75" alt="" /></li>
</ul>
```
e o js mais simples ainda:

``` html
<script type="text/javascript"> type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.1/jquery.min.js"></script> http://wbruno.com.br/scripts/jcarousel.html
<script type="text/javascript" src="http://sorgalla.com/projects/jcarousel/lib/jquery.jcarousel.min.js"></script>

<script type="text/javascript">
jQuery(document).ready(function() {
    jQuery('#mycarousel').jcarousel();
});
</script>
```

Veja que importamos a biblioteca jQuery, **antes** do plugin, e logo depois fizemos o instanciamento do nosso carousel, pelo ID que definimos.

E lógico, o css:

``` html
<link rel="stylesheet" type="text/css" href="http://sorgalla.com/projects/jcarousel/skins/tango/skin.css" /> ```

CSS básico do skin, define posicionamento e mais algumas coisas.

Sim, eu fiz um copy & paste do exemplo1 do site. Na verdade é um teste de SEO.

Depois publico o resultado.

## [Demonstração](http://wbruno.com.br/scripts/jcarousel.html)
