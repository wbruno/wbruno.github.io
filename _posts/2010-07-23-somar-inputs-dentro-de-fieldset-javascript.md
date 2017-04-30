---
id: 63
title: Somar inputs dentro de fieldset javascript
date: 2010-07-23T23:54:41+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=63
permalink: /javascript-puro/somar-inputs-dentro-de-fieldset-javascript/
categories:
  - Javascript
tags:
  - cálculo
---
<pre name="code" class="html">&lt;html&gt;
&lt;head&gt;
&lt;script type="text/javascript"&gt;
	function id( el ){
		return document.getElementById( el );
	}
	function soma(){
		var inputs = id('campos').getElementsByTagName('input');

		var soma =0;
		for( var i=0; i&lt;inputs.length; i++ ){
			soma += parseInt( inputs[i].value );
		}
		id('resultado').value = soma;
	}
	window.onload = function(){
		id('somar').onclick = function(){
			soma();
		}
	}
	&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
	&lt;form action="" method="post"&gt;
		&lt;fieldset id="campos"&gt;
			&lt;label&gt;&lt;input type="text" name="valor[]" value="2" /&gt;&lt;/label&gt;
			&lt;label&gt;&lt;input type="text" name="valor[]" value="5" /&gt;&lt;/label&gt;
			&lt;label&gt;&lt;input type="text" name="valor[]" value="8" /&gt;&lt;/label&gt;
			&lt;label&gt;&lt;input type="text" name="valor[]" value="9" /&gt;&lt;/label&gt;
			&lt;label&gt;&lt;input type="text" name="valor[]" value="1" /&gt;&lt;/label&gt;
		&lt;/fieldset&gt;

		&lt;input type="button" name="somar" id="somar" value="Somar" /&gt;
		&lt;label&gt;Total Soma: &lt;input type="text" name="resultado" id="resultado" /&gt;&lt;/label&gt;
	&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;?
</pre>