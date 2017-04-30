---
id: 1139
title: Carousel jQuery usando jCarousel
date: 2011-06-24T23:08:05+00:00
author: William Bruno
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

Eu já havia mostrado como fazer um [Carousel usando o Cycle](http://wbruno.com.br/2011/04/15/carousel-jquery-usando-cycle/), então fica tb a dica de como usar o plugin jCarousel.

O HTML bem simples:

<pre name="code" class="html">&lt;ul id="mycarousel" class="jcarousel-skin-tango"> 
	&lt;li>&lt;img src="http://static.flickr.com/66/199481236_dc98b5abb3_s.jpg" width="75" height="75" alt="" />&lt;/li> 
	&lt;li>&lt;img src="http://static.flickr.com/75/199481072_b4a0d09597_s.jpg" width="75" height="75" alt="" />&lt;/li> 
	&lt;li>&lt;img src="http://static.flickr.com/57/199481087_33ae73a8de_s.jpg" width="75" height="75" alt="" />&lt;/li> 
	&lt;li>&lt;img src="http://static.flickr.com/77/199481108_4359e6b971_s.jpg" width="75" height="75" alt="" />&lt;/li> 
	&lt;li>&lt;img src="http://static.flickr.com/58/199481143_3c148d9dd3_s.jpg" width="75" height="75" alt="" />&lt;/li> 
	&lt;li>&lt;img src="http://static.flickr.com/72/199481203_ad4cdcf109_s.jpg" width="75" height="75" alt="" />&lt;/li> 
	&lt;li>&lt;img src="http://static.flickr.com/58/199481218_264ce20da0_s.jpg" width="75" height="75" alt="" />&lt;/li> 
	&lt;li>&lt;img src="http://static.flickr.com/69/199481255_fdfe885f87_s.jpg" width="75" height="75" alt="" />&lt;/li> 
	&lt;li>&lt;img src="http://static.flickr.com/60/199480111_87d4cb3e38_s.jpg" width="75" height="75" alt="" />&lt;/li> 
	&lt;li>&lt;img src="http://static.flickr.com/70/229228324_08223b70fa_s.jpg" width="75" height="75" alt="" />&lt;/li> 
&lt;/ul></pre>

e o js mais simples ainda:

<pre name="code" class="javascript">&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.1/jquery.min.js">&lt;/script> http://wbruno.com.br/scripts/jcarousel.html
&lt;script type="text/javascript" src="http://sorgalla.com/projects/jcarousel/lib/jquery.jcarousel.min.js">&lt;/script> 

&lt;script type="text/javascript">
jQuery(document).ready(function() {
    jQuery('#mycarousel').jcarousel();
});
&lt;/script> 
</pre>

Veja que importamos a biblioteca jQuery, **antes** do plugin, e logo depois fizemos o instanciamento do nosso carousel, pelo ID que definimos.

E lógico, o css:

<pre name="code" class="html">&lt;link rel="stylesheet" type="text/css" href="http://sorgalla.com/projects/jcarousel/skins/tango/skin.css" /> </pre>

CSS básico do skin, define posicionamento e mais algumas coisas.

Sim, eu fiz um copy & paste do exemplo1 do site. Na verdade é um teste de SEO.
  
Depois publico o resultado.

## [Demonstração](http://wbruno.com.br/scripts/jcarousel.html)