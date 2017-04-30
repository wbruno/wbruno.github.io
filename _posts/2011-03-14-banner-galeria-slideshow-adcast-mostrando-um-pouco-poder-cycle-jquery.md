---
id: 226
title: Banner, Galeria, Slideshow, AdCast mostrando um pouco do poder do Cycle jQuery
date: 2011-03-14T10:26:35+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=226
permalink: /jquery/banner-galeria-slideshow-adcast-mostrando-um-pouco-poder-cycle-jquery/
dsq_thread_id:
  - "2100742945"
categories:
  - jQuery
tags:
  - plugin
  - slideshow
---
Chamem como preferirem. Vamos lá! Mãos a massa.

Primeiro post desse tipo, de muitos que virão(tomara).

No final deste post, chegaremos neste resultado:[<img src="/wp-content/uploads/2011/03/slide.png" alt="" title="slideshow jquery cycle " width="640" height="271" class="aligncenter size-full wp-image-230" srcset="/wp-content/uploads/2011/03/slide.png 640w, /wp-content/uploads/2011/03/slide-300x127.png 300w" sizes="(max-width: 640px) 100vw, 640px" />](/wp-content/uploads/2011/03/slide.png)

Para não termos sempre &#8216;Mais do Mesmo&#8217;, em todos os posts que eu fizer, juro que logo mais faço um Bê a Bá, de como &#8216;baixar o jQuery, instalar, e começar a usar&#8217;.

<!--more-->



Site do Cycle: <a href="http://jquery.malsup.com/cycle/download.html" target="_blank">http://jquery.malsup.com/cycle/download.html</a>.

Só clicar no Download.

Uma busca rápida por wallpapers no Google Images, e:

<pre name="code" class="html">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript" src="js/jquery-1.5.min.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="js/jquery.cycle.all.min.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;
$(document).ready(function(){
	$('#slide_fotos').cycle({
		fx: 'fade',
		pager: '#pager'
	});
});
&lt;/script&gt;
&lt;style type="text/css"&gt;
* {
	list-style: none;
	margin: 0;
	padding: 0;
}
body {
	font: 12px Verdana, sans-serif;
	color: #000;
}
a { text-decoration: none; }
a:hover { text-decoration: underline; }
#slideshow {
	width: 640px;
	height: 270px;
	position: relative;
}
#slide_fotos p {
	position: absolute;
	right: 0;
	top: 210px;
	z-index: 3;
	padding: 10px 20px;
	background: url('../images/over_white.png');
}
#slide_fotos {
	height: 100%;
	overflow: hidden;
}
#pager {
	position: absolute;
	z-index: 10;
	top: 20px;
	right: 20px;
}
#pager a {
	color: #000;
	width: 17px;
	height: 17px;
	line-height: 15px;
	text-align: center;
	display: inline-block;
	font-size: 10px;
	margin: 2px;
	color: #fff;
}
#pager a.activeSlide {
	color: #000;
	background: url('../images/over_white.png');
}
&lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
	&lt;div id="slideshow"&gt;
		&lt;ul id="slide_fotos"&gt;
			&lt;li&gt;&lt;img src="images/medium/01.jpg" alt="" title="Foto 01" /&gt;
				&lt;p&gt;Primeira Imagem, céu azul!&lt;/p&gt;&lt;/li&gt;
			&lt;li&gt;&lt;img src="images/medium/02.jpg" alt="" title="Foto 02" /&gt;
				&lt;p&gt;Segunda Imagem, queda d'agua&lt;/p&gt;&lt;/li&gt;
			&lt;li&gt;&lt;img src="images/medium/03.jpg" alt="" title="Foto 03" /&gt;
				&lt;p&gt;Terceira Imagem, universo, negro&lt;/p&gt;&lt;/li&gt;
			&lt;li&gt;&lt;img src="images/medium/04.jpg" alt="" title="Foto 04" /&gt;
				&lt;p&gt;Quarta Imagem, praia calmaria&lt;/p&gt;&lt;/li&gt;
			&lt;li&gt;&lt;img src="images/medium/05.jpg" alt="" title="Foto 05" /&gt;
				&lt;p&gt;Quinta Imagem, montanhas, lago&lt;/p&gt;&lt;/li&gt;
			&lt;li&gt;&lt;img src="images/medium/06.jpg" alt="" title="Foto 06" /&gt;
				&lt;p&gt;Sexta Imagem, mais verde natureza&lt;/p&gt;&lt;/li&gt;
		&lt;/ul&gt;&lt;!-- /fotos --&gt;
		&lt;p id="pager"&gt;

		&lt;/p&gt;&lt;!-- /pager --&gt;
	&lt;/div&gt;&lt;!-- /slideshow --&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

Mais uma vez, o &#8216;grande truque&#8217;, é o CSS.

Veja que o javascript é mínimo.

<pre name="code" class="javascript:firstline[6]">$(document).ready(function(){
    $('#slide_fotos').cycle({
        fx: 'fade',
        pager: '#pager'
    });
});
</pre>

Existem muitas opções na documentação do Cycle, mas a beleza do slideshow, depende da sua criatividade, e de muito css.

<a href="http://www.wbruno.com.br/scripts/cycle-simples.html" target="_blank">Demo</a>
