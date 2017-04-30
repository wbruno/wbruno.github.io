---
id: 1663
title: 'Carregando sem refresh, várias áreas diferentes de um site &#8211; jQuery.ajax'
date: 2011-12-29T10:55:46+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1663
permalink: /ajax/carregando-sem-refresh-varias-areas-diferentes-de-um-site-jquery-ajax/
dsq_thread_id:
  - "2102321307"
categories:
  - AJAX
---
Eu já postei aqui no meu blog, como <a href="http://wbruno.com.br/2011/03/30/navegacao-sem-refresh-carregando-conteudo-ajax-em-div/" target="_blank">carregar conteudo com ajax em div</a>, daí, aprimorei aquele código, e mostrei como <a href="http://wbruno.com.br/2011/05/27/navegacao-sem-refresh-%E2%80%93-carregando-conteudo-ajax-em-div-2/" target="_blank">carregar conteudo com ajax, colocando também um gif de loading</a>.. e também como fazer tudo isso de cima, ainda <a href="http://wbruno.com.br/2011/11/25/carregando-conteudo-ajax-trocando-url-jquery/" target="_blank">trocando a URL, e usando um plugin na página interna</a>.

Hoje é dia de carregar várias divs &#8216;separadas&#8217;, várias áreas diferentes com ajax.
  
<!--more-->


  
Já vi no fórum um cara(com dúvida) resolvendo isso, de uma forma &#8216;natural&#8217; do ponto de vista de pensamento humano, mas terrível para performance e manutenção do site.

O código que ele usou era mais ou menos assim:

<pre name="code" class="javascript:firstLine[6]">jQuery(document).ready(function(){
	var sidebar = jQuery('#sidebar');
	var content = jQuery('#content');
	var other = jQuery('#other');
	
	jQuery('#menu a').click(function( e ){
		e.preventDefault();
		if( jQuery( this ).attr('href')=='home.html' )
		{
			sidebar.load('home_sidebar.html');
			content.load('home_content.html');
			other.load('home_other.html');
		}
		else if( jQuery( this ).attr('href')=='cadastro.html' )
		{
			sidebar.load('cadastro_sidebar.html');
			content.load('cadastro_content.html');
			other.load('cadastro_other.html');
		}
	});
});
</pre>

Ou seja, a cada clique em um link do menu, ele fazia 3 requests. Um para cada &#8216;área&#8217; do site.
  
Tinha que manter 3 arquivos distintos para cada link, e esse jogo de if/else para saber quais arquivos ele deve invocar.

> Isso deve ter um &#8216;mau cheiro&#8217;.

A cada clique fazer 3 requisições, e ter que manter 3 arquivos separados para cada área.. além de que o site &#8216;não vai funcionar corretamente&#8217;, se o suporte a js estiver desabilitado&#8230; muitos motivos para evidenciar que algo está errado.

> Mas então, o que podemos fazer?

A minha sugestão, é aproveitar o ótimo parser de HTML da lib jQuery, fazer um único request, e então direcionar cada conteúdo para o local específico.

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript" src="jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
jQuery(document).ready(function(){
	var sidebar = jQuery('#sidebar');
	var content = jQuery('#content');
	var other = jQuery('#other');
	
	request( 'home.html' );
	
	function m_load( data )
	{
		var text = jQuery( '&lt;div>'+data+'&lt;/div>' );//forçando o parser
		
		sidebar.html( text.find('#sidebar').html() );
		content.html( text.find('#content').html() );
		other.html( text.find('#other').html() );
		
		jQuery(document).attr( 'title', text.find('title').html() );
	}
	function request( file )
	{
		jQuery.ajax({
			url: file,
			success: function( data )
			{
				m_load( data );
			}
		});	
	}
	jQuery('#menu a').click(function( e ){
		e.preventDefault();
		request( jQuery( this ).attr('href') );
	});
});

&lt;/script>
&lt;/head>
&lt;body>
	&lt;ul id="menu">
		&lt;li>&lt;a href="home.html">Home&lt;/a>&lt;/li>
		&lt;li>&lt;a href="cadastro.html">Cadastro&lt;/a>&lt;/li>
		&lt;li>&lt;a href="contato.html">Contato&lt;/a>&lt;/li>
	&lt;/ul>&lt;!-- /menu -->
	&lt;div id="sidebar">
		
	&lt;/div>&lt;!-- /sidebar -->
	&lt;div id="content">
		
	&lt;/div>&lt;!-- /content -->
	&lt;div id="other">
		
	&lt;/div>&lt;!-- /other -->
&lt;/body>
&lt;/html>
</pre>

Note que além de fazer o parser do retorno:

<pre name="code" class="javascript:firstLine[14]">var text = jQuery( '&lt;div>'+data+'&lt;/div>' );//forçando o parser
		
		sidebar.html( text.find('#sidebar').html() );
		content.html( text.find('#content').html() );
		other.html( text.find('#other').html() );</pre>

eu também faço a troca do title do documento:

<pre name="code" class="javascript:firstLine[20]">jQuery(document).attr( 'title', text.find('title').html() );</pre>

## [Demonstração](http://wbruno.com.br/scripts/index_3areas.html)

Se vc tiver o firebug instalado, confira na aba Net|Rede -> xhr que faço apenas uma requisição.