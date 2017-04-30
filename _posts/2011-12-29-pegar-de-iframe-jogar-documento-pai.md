---
id: 1672
title: 'Pegar &lt;title> de iframe, e jogar no documento pai'
date: 2011-12-29T11:33:54+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1672
permalink: /javascript-puro/pegar-de-iframe-jogar-documento-pai/
dsq_thread_id:
  - "2101210323"
categories:
  - Javascript
tags:
  - iframe
---
Dúvida que vi no fórum.

Pegar o valor da tag title de um iframe, e colocar ele em um titulo do lado de fora, do documento pai.
  
Não é &#8216;tão simples&#8217; assim, e notei um probleminha: &#8216;o iframe precisa ser carregado antes de tentarmos pegar o conteúdo dele&#8217;.

<!--more-->


  
Bom, resolvi dessa forma:

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript" src="jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
jQuery(document).ready(function(){
	jQuery('#menu a').click(function( e ){
		
		jQuery('#content').load(function(){
			var titulo = jQuery('#content').contents().find('title').text();		
			jQuery('#titulo').text( titulo );		
		});
	});
});
&lt;/script>
&lt;/head>
&lt;body>
	&lt;ul id="menu">
		&lt;li>&lt;a href="home.html" target="content">Home&lt;/a>&lt;/li>
		&lt;li>&lt;a href="cadastro.html" target="content">Cadastro&lt;/a>&lt;/li>
		&lt;li>&lt;a href="contato.html" target="content">Contato&lt;/a>&lt;/li>
	&lt;/ul>&lt;!-- /menu -->
	&lt;h1 id="titulo">Home&lt;/h1>
	&lt;iframe name="content" id="content" src="home.html"  width="99.9%" frameborder="0" scrolling="no" >&lt;/iframe>
&lt;/body>
&lt;/html></pre>

Por esse motivo, depois do clique, eu aguardo o evento &#8216;onload&#8217; do iframe:

<pre name="code" class="javascript">jQuery('#content').load(function(){</pre>

Sse vc não quiser incorporar a lib jQuery, e também para provar que jQuery é apenas javascript, segue a mesma funcionalidade, usando apenas js puro:

<pre name="code" class="javascript:firstLine[4]">function id( el )
{
	return document.getElementById( el );
}
window.onload = function()
{
	id('content').onload = function()
	{
		var titulo = this.contentWindow.document.getElementsByTagName('title')[0].innerHTML;
		id('titulo').innerHTML = titulo;	
	};	
}</pre>

é isso =)
  
Se for útil, comente e compartilhe. Esse é o único &#8216;pagamento&#8217; que peço pelos códigos(conhecimento) que disponibilizo.