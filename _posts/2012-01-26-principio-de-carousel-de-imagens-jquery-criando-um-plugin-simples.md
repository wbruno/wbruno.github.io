---
id: 1748
title: 'Princípio de carousel de imagens com jQuery &#8211; Criando um plugin simples'
date: 2012-01-26T07:00:06+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1748
permalink: /jquery/principio-de-carousel-de-imagens-jquery-criando-um-plugin-simples/
dsq_thread_id:
  - "2101046897"
categories:
  - jQuery
tags:
  - carousel
  - plugin
---
Nos últimos meses, tenho usado bastante o efeito de carousel.
  
Como todo programador, me incomodo de ter que &#8216;me repetir&#8217;. Ou ter que repensar uma lógica que já resolvi uma vez.

Nem sempre &#8216;temos tempo&#8217; de parar, analisar e otimizar oque estamos fazendo.
  
Porém, **devemos** fazer isso.
  
<!--more-->


  
Fiz vários tipos de carouseis, porém por serem diferentes um dos outros, e alguns possuirem algumas peculiaridades, configurações extras, estilizações fora dos padrões, acabei fazendo os meus próprios códigos, e não usando nenhum plugin pronto.

Nesse post, vou deixar o start de um plugin de jQuery, que rapidamente fiz aqui.
  
Muitas melhorias precisam ser feitas, como:
  
-> possibilitar scroll vertical
  
-> não limitar a marcação a ser usada
  
-> permitir uso do easing..

e por ai vai.. nisso, eu acabaria recriando o cycle(ou chegando perto do efeito Hz dele). Não é essa a intenção.
  
Até agora é para ser simples mesmo, e muito mais simples de usar também.

Como todos os meus efeitos, esse não foge do meu padrão: resolvi as partes mais complicadas no css.
  
O js é simples. O instanciamento ainda mais.

É isso, sem mais, segue o código, e logo abaixo a demonstração.
  
A grande &#8216;sacada&#8217;, é deixar o plugin se virar com a animação, (setas prev e next), e termos uma chamada simples e limpa assim:

<pre name="code" class="javascript:firstLine[48]">/* fim plugin carousel */
jQuery(document).ready(function(){
	jQuery('#slide').carousel();
	jQuery('#slide2').carousel();
});
</pre>

## <a href="http://wbruno.com.br/scripts/simple_carousel.html" target="_blank">Demonstração</a>

=) Vejam como fiz:

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
/* carousel */
jQuery.fn.carousel = function( settings ){
	var $this = jQuery( this );
	var defaults = {
		prev: '.nav-left',
		next: '.nav-right',
		pos: 0,
		speed: 1000
	}
	settings = jQuery.extend(defaults, settings); 
	
	
	var lis = $this.find('li');
	var width_li = lis.eq(0).width()+ parseInt( lis.eq(0).css('marginLeft') )+parseInt( lis.eq(0).css('marginRight') );
	var ul = $this.find('ul');
	
	
	var prev = $this.find( settings.prev );
	var next = $this.find( settings.next );

	ul.css({width: (width_li*lis.length)+'px'});
	
	
	/* .nav-left */
	prev.click(function(){
		if( settings.pos>0 ){
			settings.pos--;
			_move( ul, settings.pos, width_li, settings.speed );
		}
	});
	/* .nav-right */
	next.click(function(){
		if( lis.length-1>settings.pos ){
			settings.pos++;
			_move( ul, settings.pos, width_li, settings.speed );
		}
	});

	/* funcoes privadas */
	_move = function( ul, pos, width_li, speed ){
		var new_left =  -1*pos*width_li;
		ul.animate({left:new_left+'px'},settings.speed);
	}
	
	return $this;
};
/* fim plugin carousel */
jQuery(document).ready(function(){
	jQuery('#slide').carousel();
	jQuery('#slide2').carousel();
});
&lt;/script>
&lt;style type="text/css">
* { margin: 0; padding: 0; }
#slide { width: 460px; height: 300px; }
	#slide li { width: 460px; height: 300px; }
#slide2 { width: 140px; height: 105px; padding: 10px 25px; background: #000; }
	#slide2 li { width: 140px; height: 105px; }
hr { margin: 50px; }

/* css do plugin */
.carousel { position: relative; }
.overflow { overflow: hidden; height: 100%; position: relative; }
.carousel ul { position: absolute; top: 0; left: 0; }
.carousel li { float: left; }
.nav { position: absolute; top: 50%; z-index: 3;
	background: url('images/nav.png') no-repeat;
	width: 36px; height: 36px; margin-top: -18px;
	cursor: pointer;
}
.nav-left { left: 10px; }
.nav-right { right: 10px; background-position: right top; }
	.nav-left:hover { background-position: left -36px; }
	.nav-right:hover { background-position: right -36px; }
/* css do plugin */
&lt;/style>
&lt;/head>
&lt;body>

	&lt;div id="slide" class="carousel">
		&lt;div class="nav nav-left">&lt;/div>
		&lt;div class="overflow">
			&lt;ul>
				&lt;li>&lt;img src="images/1.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="images/2.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="images/3.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="images/4.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="images/5.jpg" alt="" />&lt;/li>
			&lt;/ul>
		&lt;/div>
		&lt;div class="nav nav-right">&lt;/div>
	&lt;/div>&lt;!-- /slide -->
	
	&lt;hr />
	
	&lt;div id="slide2" class="carousel">
		&lt;div class="nav nav-left">&lt;/div>
		&lt;div class="overflow">
			&lt;ul>
				&lt;li>&lt;img src="images/mini1.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="images/mini2.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="images/mini3.jpg" alt="" />&lt;/li>
				&lt;li>&lt;img src="images/mini4.jpg" alt="" />&lt;/li>
			&lt;/ul>
		&lt;/div>
		&lt;div class="nav nav-right">&lt;/div>
	&lt;/div>&lt;!-- /slide -->
&lt;/body>
&lt;/html>

</pre>