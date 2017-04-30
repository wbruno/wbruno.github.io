---
id: 1557
title: 'Evitando duplicação de script &#8211; jQuery'
date: 2011-10-21T12:42:01+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1557
permalink: /jquery/evitando-duplicacao-de-script-jquery/
categories:
  - jQuery
---
Este post, é uma aplicação direta, dos conceitos que expliquei aqui: <a href="http://wbruno.com.br/2011/07/18/vixi-aprendi-jquery-mas-agora/" target="_blank">Aprendi jQuery, e agora ?</a>
  
Acabei de ver um user no fórum que precisava disparar uma mesma rotina, para campos input e select.

Porém, sabemos que para selects, o evento a ser usado, é o onchange, e para inputs, onkeypress|onblur..
  
<!--more-->


  
Exatamente por esse motivo, não podemos fazer simplesmente:

<pre name="code" class="javascript">$('input, select').blur(function(){
    alert( 'rotina' );
});</pre>

ou 

<pre name="code" class="javascript">$('input, select').change(function(){
    alert( 'rotina' );
});</pre>

pois não conseguiríamos separar os eventos, e fazer:

<pre name="code" class="javascript">$('input').blur(function(){
    alert( 'rotina' );
});
$('select').change(function(){
    alert( 'rotina' );
});</pre>

não é lega, pois estamos duplicando esse

<pre name="code" class="javascript:firstLine[2]">alert( 'rotina' );</pre>

Logo, lembrando do que falei lá em cima, no outro post, devemos poder fazer:

<pre name="code" class="javascript">var rotina = function(){
    alert( 'rotina' );
};
$('input').blur( rotina );
$('select').change( rotina );</pre>

E não é que funciona !! pois é.. javascript é uma linguagem maravilhosa de linda.. hehe

E se fosse mais complicado, precisa-se usar o **this**.. ?
  
Sem problemas. E se vc não confia em mim, teste por você mesmo:

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;script src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.4/jquery.min.js">&lt;/script>
	&lt;script>
	$(document).ready(function(){
		var verificacao = function(){
			var id = $( this ).attr('id');
			alert( id );
		};
	
		$('#id1').click( verificacao );
		$('#id2').click( verificacao );
	});
	&lt;/script>
&lt;/head>
&lt;body>

	&lt;span id="id1">aqui&lt;/span>
	&lt;span id="id2">aqui&lt;/span>
&lt;/body>
&lt;/html></pre>

é isso ai.
  
Sabia disso ? Ou não sabia ainda, e acabou duplicando scripts ?
  
Comente.