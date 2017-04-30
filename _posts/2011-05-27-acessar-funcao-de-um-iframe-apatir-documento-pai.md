---
id: 1044
title: Acessar função de um iframe, apatir do documento pai
date: 2011-05-27T15:00:45+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1044
permalink: /javascript-puro/acessar-funcao-de-um-iframe-apatir-documento-pai/
dsq_thread_id:
  - "2104774652"
categories:
  - Javascript
tags:
  - iframe
---
Operação inversa dessa vez..

para acessarmos uma função do documento pai, de dentro do iframe, o objeto **parent**, nos ajuda.

Porém e ao contrário ?
  
<!--more-->


  
Do documento pai, acessar uma function no iframe.

**index.html**

<pre name="code" class="html">&lt;input type="text" name="tal" id="tal" value="TalTal" />

&lt;input type="button" name="ok" id="ok" value="Ok" />

&lt;br />&lt;br />
&lt;iframe id="grid" src="grid.html">&lt;/iframe>



&lt;script type="text/javascript">
window.onload = function()
{
	var grid = id('grid').contentWindow;
	grid.escreve( id('tal').value );


	id('ok').onclick = function(){
		grid.escreve( id('tal').value );
	}
}
function id( el ){
	return document.getElementById( el );
}
&lt;/script>
</pre>

e o iframe: **grid.html**

<pre name="code" class="html">&lt;div id="ae">&lt;/div>


&lt;script type="text/javascript">
function escreve( str ){
        document.getElementById('ae').innerHTML = str;
}
&lt;/script>
</pre>