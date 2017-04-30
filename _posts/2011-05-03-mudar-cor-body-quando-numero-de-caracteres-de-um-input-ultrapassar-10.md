---
id: 888
title: Mudar cor do body quando o número de caracteres de um input, ultrapassar 10
date: 2011-05-03T22:17:54+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=888
permalink: /javascript-puro/mudar-cor-body-quando-numero-de-caracteres-de-um-input-ultrapassar-10/
categories:
  - Javascript
---
De novo, incrível como a galera tenta meter jQuery em tudo.
  
Dessa vez, era &#8216;fácil&#8217; fazer com javascript puro.. mas como o camarada não sabia como fazer, tentou apelar, e mesmo assim não conseguiu.

De novo, vamos estudar js puro galera !!

<pre name="code" class="html">&lt;script type="text/javascript">
window.onload = function(){
	document.getElementById('nome').onkeypress = function(){
		var bgcolor = this.value.length>=10 ? '#003' : '#fff';
		document.body.style.backgroundColor = bgcolor;
	}
}
&lt;/script>

&lt;form action="" method="post">
	&lt;input type="text" name="nome" id="nome" />
	&lt;input type="button" value="Botão"  />
&lt;/form>
</pre>

=)