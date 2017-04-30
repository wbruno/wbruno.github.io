---
id: 770
title: Carousel jQuery usando o Cycle
date: 2011-04-15T15:20:48+00:00
author: William Bruno
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
  
[<img src="http://wbruno.com.br/wp-content/uploads/2011/04/Screen-shot-2011-04-15-at-2.39.36-PM1.png" alt="" title="Screen-shot-2011-04-15-at-2.39.36-PM" width="650" height="133" class="aligncenter size-full wp-image-774" srcset="http://wbruno.com.br/wp-content/uploads/2011/04/Screen-shot-2011-04-15-at-2.39.36-PM1.png 650w, http://wbruno.com.br/wp-content/uploads/2011/04/Screen-shot-2011-04-15-at-2.39.36-PM1-300x61.png 300w" sizes="(max-width: 650px) 100vw, 650px" />](http://wbruno.com.br/wp-content/uploads/2011/04/Screen-shot-2011-04-15-at-2.39.36-PM1.png)
  
<!--more-->


  
Posso dividir em 4 partes, o HTML que precisamos:

## Container

<pre name="code" class="html:firstLine[58]">&lt;div id="wrap_carousel"></pre>

Engloba o resto, e dá o contexto de posicionamento, que precisamos.

## Setas

<pre name="code" class="html:firstLine[59]">&lt;img src="left_arrow.jpg" alt="" id="prev" /></pre>

e

<pre name="code" class="html:firstLine[69]">&lt;img src="right_arrow.jpg" alt="" id="next" /></pre>

Voltar e Avançar no carousel. Controles manuais da exibição.

## Caixa para overflow

<pre name="code" class="html:firstLine[60]">&lt;div id="carousel"></pre>

Esta é a segunda parte mais importante do nosso html. Com ela, escondemos as próximas fotos(para conseguirmos o efeito de &#8216;rolar passando&#8217;).

## Blocos de Conteúdo

É a parte mais importante do nosso HTML, para esse efeito.

<pre name="code" class="html:firstLine[61]">&lt;ul>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_1.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_2.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_3.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_4.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_5.jpg" alt="" />&lt;/li>
			&lt;/ul>
</pre>

Como são exibidas de 5 em 5 imagens, cada bloco de conteudo nosso, possui exatamente essas 5 imagens.
  
Quando o **cycle**, fizer a transição, ele irá rolar esse bloco para escondê-lo, e trazer o próximo para ser exibido.

Se quisessemos mostrar de 3 em 3 fotos, cada bloco nosso, deveria ter 3 <li>, com as respectivas imagens. E assim por diante.

Assim como da outra vez, em que fizemos uma [galeria de fotos com jQuery](http://www.wbruno.com.br/2011/03/14/banner-galeria-slideshow-adcast-mostrando-um-pouco-poder-cycle-jquery/), o script é ridículo:

<pre name="code" class="javascript:firstLine[61]">$(document).ready(function(){
	$('#carousel').cycle({
		fx:   		'scrollHorz',
		prev: 		'#prev',
		next: 		'#next'
	});

});
</pre>

Código completo com o css:

<pre name="code" class="html:firstLine[1]">&lt;html>
&lt;head>

&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js">&lt;/script>
&lt;script type="text/javascript" src="http://cloud.github.com/downloads/malsup/cycle/jquery.cycle.all.latest.js">&lt;/script>

&lt;script type="text/javascript">
$(document).ready(function(){
	$('#carousel').cycle({
		fx:   		'scrollHorz',
		prev: 		'#prev',
		next: 		'#next'
	});

});
&lt;/script>
&lt;style type="text/css">
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
&lt;/style>
&lt;/head>
&lt;body>
	&lt;div id="wrap_carousel">
		&lt;img src="left_arrow.jpg" alt="" id="prev" />
		&lt;div id="carousel">
			&lt;ul>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_1.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_2.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_3.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_4.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_5.jpg" alt="" />&lt;/li>
			&lt;/ul>
			&lt;ul>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_6.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_7.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_8.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_9.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_10.jpg" alt="" />&lt;/li>
			&lt;/ul>
			&lt;ul>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_11.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_12.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_13.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_14.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="http://www.egrappler.com/contents/jscarouselv2/demo/images/img_15.jpg" alt="" />&lt;/li>
			&lt;/ul>
		&lt;/div><!-- carousel -->
		&lt;img src="right_arrow.jpg" alt="" id="next" />
	&lt;/div>

<!-- /wrap_carousel -->
&lt;/body>
&lt;/html>
</pre>

## <a href="http://www.wbruno.com.br/scripts/carousel.html" target="_blank">Demonstração online do Carousel</a>