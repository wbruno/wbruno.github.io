---
id: 2973
title: 'Plugin jQuery em elemento criado dinamicamente com javascript &#8211; append jQuery'
date: 2013-05-17T10:51:44+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2973
permalink: /jquery/plugin-jquery-em-elemento-criado-dinamicamente-com-javascript-append-jquery/
dsq_thread_id:
  - "2101014691"
image: /wp-content/uploads/2013/05/jquery.png
categories:
  - jQuery
tags:
  - dom
---
Eu já postei como utilizar a função [.live() do jQuery](http://wbruno.com.br/ajax/metodo-live-jquery/), que inclusive foi removida na nova versão da biblioteca(para usarmos o método <var>.on()</var> no estilo delegate), já mostrei [como instanciar plugins depois de carregar um elemento com ajax](http://wbruno.com.br/ajax/usando-lightbox-em-pagina-carregada-ajax/).

Mas e como podemos fazer para chamar/ativar um plugin, em elementos criados dinamicamente, com o append ?
  
<!--more-->

## O problema &#8211; não funciona em elementos criados com append

<pre class="html">&lt;!doctype html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
	&lt;meta charset="UTF-8"&gt;
	&lt;title&gt;Document&lt;/title&gt;

	&lt;link rel="stylesheet" href="colorbox.css" /&gt;

	&lt;script src="http://code.jquery.com/jquery-1.9.1.min.js"&gt;&lt;/script&gt;
	&lt;script src="jquery.colorbox.js"&gt;&lt;/script&gt;
&lt;script&gt;
jQuery(document).ready(function(){
	var $add = jQuery('#add'),
		$insert = jQuery('#insert');

	jQuery('a').colorbox();

	$add.on('click', function(){
		$insert.append('&lt;a href="images/1.jpg"&gt;colorbox - nao funciona&lt;/a&gt;&lt;br /&gt;');
	});
});
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
	&lt;input type="button" name="add" id="add" value="add" /&gt;
	&lt;div id="insert"&gt;
		&lt;a href="images/1.jpg"&gt;colorbox&lt;/a&gt;&lt;br /&gt;
	&lt;/div&gt;&lt;!-- #insert --&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>

O motivo do colorbox só funcionar na tag <var><a></var> que já existe no documento, é pq nós atrelamos o plugin **apenas no carregamento** da página.
  
Logo, só funciona nos elementos **que já existiam** no instante em que a página terminou de carregar(evento disparado pelo dom.ready).

## A solução &#8211; instanciar o plugin novamente cada vez que inserir um elemento

Então, para que o colorbox funcione nos demais elementos, precisamos atrelar o plugin nestes elementos, assim que eles forem inseridos na página, ou seja, após o append.

<pre class="javascript">$add.on('click', function(){
	$insert.append('&lt;a href="images/1.jpg"&gt;colorbox&lt;/a&gt;&lt;br /&gt;');
	$insert.find('a').colorbox();
});</pre>

Simples assim. Note a linha abaixo do append. Estou chamando o plugin nos elementos que foram criados, logo após criar eles.

Ai sim, tudo funciona perfeitamente. O princípio é o mesmo para qualquer plugin que você quiser usar.

### Código da Solução

<pre class="html">&lt;!doctype html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
	&lt;meta charset="UTF-8"&gt;
	&lt;title&gt;Document&lt;/title&gt;

	&lt;link rel="stylesheet" href="colorbox.css" /&gt;

	&lt;script src="http://code.jquery.com/jquery-1.9.1.min.js"&gt;&lt;/script&gt;
	&lt;script src="jquery.colorbox.js"&gt;&lt;/script&gt;
&lt;script&gt;
jQuery(document).ready(function(){
	var $add = jQuery('#add'),
		$insert = jQuery('#insert');

	$add.on('click', function(){
		$insert.append('&lt;a href="images/1.jpg"&gt;colorbox&lt;/a&gt;&lt;br /&gt;');
		$insert.find('a').colorbox();
	});
});
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
	&lt;input type="button" name="add" id="add" value="add" /&gt;
	&lt;div id="insert"&gt;
		&lt;a href="images/1.jpg"&gt;colorbox&lt;/a&gt;&lt;br /&gt;
	&lt;/div&gt;&lt;!-- #insert --&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>

É isso galera, comentem caso usem. =)