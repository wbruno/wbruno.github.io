---
id: 770
title: Carousel jQuery usando o Cycle
date: 2011-04-15T15:20:48+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=770
permalink: /jquery/carousel-jquery-usando-cycle/
dsq_thread_id:
  - "2101078866"
categories:
  - jQuery
tags:
  - carousel
  - plugin
  - slideshow
---
Salve! mais uma vez aqui para mostrar, mais um pouco do poder do **plugin Cycle do jQuery**.

Sei que existem &#8216;plugins especificos&#8217;, bem robustos.. porém imagine a situação em que vc tem um **slideshow** e um **carousel** no mesmo site. Chamar 2 plugins, um para cada coisa, qndo na verdade, apenas o cycle resolveria.. não parece legal ne?!

Além de que _a forma de pensar_ é diferente. Aqui temos a iniciativa do **começar a fazer**. Criar o HTML, pensar no CSS necessário.. essa iniciativa faz a diferença.

O efeito que vou criar, é o mesmo do primeiro exemplo <a href="http://www.egrappler.com/contents/jscarouselv2/demo/jscarousel-2.0.0.htm" target="_blank">deste plugin de carousel</a>. Acredito que vai ajudar a abrir a mente, desmistificando algumas coisas, e entendendo o motivo de outras.

[<img src="/wp-content/uploads/2011/04/Screen-shot-2011-04-15-at-2.39.36-PM1.png" alt="" title="Screen-shot-2011-04-15-at-2.39.36-PM" width="650" height="133" class="aligncenter size-full wp-image-774" srcset="/wp-content/uploads/2011/04/Screen-shot-2011-04-15-at-2.39.36-PM1.png 650w, /wp-content/uploads/2011/04/Screen-shot-2011-04-15-at-2.39.36-PM1-300x61.png 300w" sizes="(max-width: 650px) 100vw, 650px" />](/wp-content/uploads/2011/04/Screen-shot-2011-04-15-at-2.39.36-PM1.png)

<!--more-->



Posso dividir em 4 partes, o HTML que precisamos:

## Container

``` html
<div id="wrap_carousel">
```
Engloba o resto, e dá o contexto de posicionamento, que precisamos.

## Setas

``` html
<img src="left_arrow.jpg" alt="" id="prev" />
```
e

``` html
<img src="right_arrow.jpg" alt="" id="next" />
```
Voltar e Avançar no carousel. Controles manuais da exibição.

## Caixa para overflow

``` html
<div id="carousel">
```
Esta é a segunda parte mais importante do nosso html. Com ela, escondemos as próximas fotos(para conseguirmos o efeito de &#8216;rolar passando&#8217;).

## Blocos de Conteúdo

É a parte mais importante do nosso HTML, para esse efeito.

``` html
<ul>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_1.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_2.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_3.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_4.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_5.jpg" alt="" /></li>
      </ul>
```

Como são exibidas de 5 em 5 imagens, cada bloco de conteudo nosso, possui exatamente essas 5 imagens.

Quando o **cycle**, fizer a transição, ele irá rolar esse bloco para escondê-lo, e trazer o próximo para ser exibido.

Se quisessemos mostrar de 3 em 3 fotos, cada bloco nosso, deveria ter 3 <li>, com as respectivas imagens. E assim por diante.

Assim como da outra vez, em que fizemos uma [galeria de fotos com jQuery](https://wbruno.com.br/jquery/banner-galeria-slideshow-adcast-mostrando-um-pouco-poder-cycle-jquery/), o script é ridículo:

``` js
$(document).ready(function(){
  $('#carousel').cycle({
    fx:       'scrollHorz',
    prev:     '#prev',
    next:     '#next'
  });

});
```

Código completo com o css:

``` html
<html>
<head>

<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
<script type="text/javascript" src="http://cloud.github.com/downloads/malsup/cycle/jquery.cycle.all.latest.js"></script>

<script type="text/javascript">
$(document).ready(function(){
  $('#carousel').cycle({
    fx:       'scrollHorz',
    prev:     '#prev',
    next:     '#next'
  });

});
</script>
<style type="text/css">
* { margin: 0; padding: 0; list-style: none; }
body {
  background-color: #2F2F2F;
  padding: 40px;
}
#wrap_carousel {
  background-color: #121212;
  border: 1px solid #7A7677;
  width:700px;
  height: 95px;
  padding: 13px 30px;
  position: relative;
}
#carousel li img {
  border: 1px solid #7A7677;
  width: 100%;
}
#carousel li {
  float: left;
  overflow: hidden;
  width: 120px;
  height: 95px;
  margin: 0 10px;
  display: inline;
}
#prev,
#next {
  position: absolute;
  top: 10px;
  cursor: pointer;
}
#prev {
  left: 10px;
}
#next {
  right: 10px;
}
</style>
</head>
<body>
  <div id="wrap_carousel">
    <img src="left_arrow.jpg" alt="" id="prev" />
    <div id="carousel">
      <ul>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_1.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_2.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_3.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_4.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_5.jpg" alt="" /></li>
      </ul>
      <ul>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_6.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_7.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_8.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_9.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_10.jpg" alt="" /></li>
      </ul>
      <ul>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_11.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_12.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_13.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_14.jpg" alt="" /></li>
        <li><img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_15.jpg" alt="" /></li>
      </ul>
    </div><!-- carousel -->
    <img src="right_arrow.jpg" alt="" id="next" />
  </div>

<!-- /wrap_carousel -->
</body>
</html>
```

## <a href="http://www.wbruno.com.br/scripts/carousel.html" target="_blank">Demonstração online do Carousel</a>
