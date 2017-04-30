---
id: 1025
title: 'JavaScript não obstrutivo &#8211; usando a função window.confirm()'
date: 2011-06-02T07:00:19+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1025
permalink: /javascript-puro/javascript-nao-obstrutivo-usando-funcao-window-confirm/
dsq_thread_id:
  - "2101352397"
categories:
  - Javascript
---
Alguns &#8216;cases&#8217; rápidos e simples, de como podemos usar javascript para melhorar a vida do usuário, sem estragar a navegação dele, e ainda deixar tudo funcionando, caso não haja suporte a js, ou o script simplesmente pare de funcionar.
  
<!--more-->

## confirm() indo para uma página

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript">
function id( el ){
	return document.getElementById( el );
}
window.onload = function(){
	id('link').onclick = function(){
		return confirm( 'Deseja ir para '+this.href+' ?' );
	}
}
&lt;/script>
&lt;/head>
&lt;body>
	&lt;a href="http://wbruno.com.br" id="link">wbruno&lt;/a>
&lt;/body>
&lt;/html>
</pre>

Veja que o código javascript é super simples. Não precisa de muito, e nem de nada complicado.

## confirm() em um formulário

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript">
function id( el ){
	return document.getElementById( el );
}
window.onload = function(){
	id('form').onsubmit = function(){
		return confirm( 'Tem certeza que deseja enviar o formulário ?' );
	}
}
&lt;/script>
&lt;/head>
&lt;body>
	&lt;form action="" method="post" id="form">
		Email: &lt;input type="text" name="email" />
		&lt;input type="submit" name="ok" value="ok" />	
	&lt;/form>
&lt;/body>
&lt;/html>
</pre>

Algumas aplicações que vejo são: &#8216;confirmar exclusão de registro&#8217; (tanto pelo link direto, qnto pelo formulário), confirmar abertura de link externo, onde o usuário &#8216;sai&#8217; do teu site&#8230;

A metodologia é simples: &#8216;Faça funcionar mesmo sem suporte a javascript&#8217;.
  
O difícil é a maioria dos programadores de hoje em dia, levarem em consideração ela.