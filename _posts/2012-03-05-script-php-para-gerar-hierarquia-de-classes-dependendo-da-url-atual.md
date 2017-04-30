---
id: 1829
title: Script php para gerar hierarquia de classes dependendo da URL atual
date: 2012-03-05T07:00:35+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1829
permalink: /php/script-php-para-gerar-hierarquia-de-classes-dependendo-da-url-atual/
dsq_thread_id:
  - "2105652623"
categories:
  - PHP
---
Fiz um post semana passada, sobre como podemos melhor aproveitar o elemento **body** dos nossos sites:

<a href="http://wbruno.com.br/2012/03/01/elemento-body-nos-nossos-sites-como-melhor-aproveita-lo/" target="_blank">http://wbruno.com.br/2012/03/01/elemento-body-nos-nossos-sites-como-melhor-aproveita-lo/</a>

E nele eu cito, que o _&#8220;trabalho&#8221;_ do server-side, seria gerar essas classes no body, ou então nós mesmos fazer isso &#8220;na mão&#8221;, página por página.

Sou preguiçoso então&#8230;
  
<!--more-->


  
Por exemplo, se a URL for:

<u>site.com.br/</u> ou <u>site.com.br/index.html</u>
  
a classe do elemento body, deve ser:

<pre name="code" class="html">&lt;body class="home"></pre>

E para cada nível, a class deve refletir:
  
<u>site.com.br/frutas.html</u>

<pre name="code" class="html">&lt;body class="frutas"></pre>

Mas se começar a &#8220;complicar&#8221;, e mais níveis surgirem..

<u>site.com.br/frutas/banana.html</u>

<pre name="code" class="html">&lt;body class="frutas banana"></pre>

Ou:
  
<u>site.com.br/frutas/banana/nanica.html</u>

<pre name="code" class="html">&lt;body class="frutas banana nanica"></pre>

Para ser eficiente, a class do nosso body, deve refletir essa &#8220;realidade&#8221;.
  
Criei um conjunto de funções em php, que fazem isso. Analisam a URL requisitada (REQUEST_URI), e devolvem essa estrutura:

<pre name="code" class="php">&lt;?php

/**
 * @return boolean, true caso a URI seja a home do site
 */
function is_home(){
	return stripos( $_SERVER['REQUEST_URI'], 'index.html' ) 
		|| !stripos( $_SERVER['REQUEST_URI'], '.html' );
}
/**
 * @return string, class=""(html) de acordo com o URI atual
 */
function get_body_class(){
	if( is_home() ) return 'class="home"';
	
	$pieces = explode( '/', $_SERVER['REQUEST_URI'] );
	$class = Array();
	foreach( $pieces AS $part ){
		$class[] = str_replace( '.html', '', $part );
	}
	
	return 'class="'.implode( ' ', $class ).'"';	
}
/**
 * @see get_body_class()
 */
function body_class(){ echo get_body_class(); }
</pre>

Agora que terminei de escrever, percebi que você pode usar também para um **bread crumb**, ne?!
  
Me diz o que você acha.
  
É isso =)