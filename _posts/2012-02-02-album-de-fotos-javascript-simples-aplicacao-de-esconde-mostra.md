---
id: 1767
title: 'Album de fotos com javascript &#8211; simples aplicação de esconde mostra'
date: 2012-02-02T17:50:50+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1767
permalink: /javascript-puro/album-de-fotos-javascript-simples-aplicacao-de-esconde-mostra/
dsq_thread_id:
  - "2105016949"
categories:
  - Javascript
---
Boas!!
  
apenas para deixar registrado mesmo..
  
<!--more-->

Album de fotos, baseado em um escode/mostra, com a propriedade display.
  
Fiz em javascript puro, em poucos minutos. Foi mais dificil achar as imagens, e mais trabalhoso redimensionar elas, do que fazer o código js.. hehe

Enfim, online:

## <a href="http://wbruno.com.br/scripts/album-disney.html" target="_blank">Demonstração</a>

script usado:

<pre name="code" class="javascript">&lt;script type="text/javascript">
function id( el ){
	return document.getElementById( el );
}
function hide_all(){
	var els = id('content').getElementsByTagName('ul');
	
	for( var i=0; i&lt;els.length; i++ )
	{		
		els[i].style.display = 'none';
	}
}
/* http://www.javascriptkit.com/jsref/event.shtml */
function disablelink( e ){
	var evt = window.event || e
	if (evt.preventDefault) //supports preventDefault?
		evt.preventDefault()
	else //IE browser
		return false
}
function palco( src ){
	id('palco').innerHTML = '&lt;img src="'+src+'" alt="" />';
}
window.onload = function(){
	hide_all();
	var as = id('lista').getElementsByTagName('a');
	for( var i=0; i&lt;as.length; i++ )
	{
		as[i].onclick = function( e ){
			hide_all();
			var id_el = this.href.split('#')
       		
			id( id_el[1] ).style.display = 'block';		
			return disablelink( e );
		}
	}
	var as = id('content').getElementsByTagName('a');
	for( var i=0; i&lt;as.length; i++ )
	{
		as[i].onclick = function( e ){
			palco( this.href )	
			return disablelink( e );
		}
	}
}
&lt;/script>
</pre>