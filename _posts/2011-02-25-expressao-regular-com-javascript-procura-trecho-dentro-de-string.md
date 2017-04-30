---
id: 118
title: Expressao Regular com javascript, procura trecho dentro de string
date: 2011-02-25T20:00:35+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=118
permalink: /expressao-regular/expressao-regular-com-javascript-procura-trecho-dentro-de-string/
dsq_thread_id:
  - "2105313711"
categories:
  - Expressão Regular
---
<pre name="code" class="html">&lt;script type="text/javascript"&gt;
	function id( el ){
		return document.getElementById( el );
	}
	function busca( q )
	{
		var seek = new RegExp( '\\b'+q );
		id('debug').innerHTML = seek;

		var texto = "Expressões regulares em Javascript para iniciantes!";

		if (texto.search( seek ) != -1)
			id('result').innerHTML = 'Encontrado na posição: '+ texto.search( seek );
		else
			id('result').innerHTML = 'Não encontrado!';
	}
	&lt;/script&gt;
	&lt;input type="text" name="q" onkeypress="busca( this.value );" /&gt;

	&lt;div id="result"&gt;&lt;/div&gt;
	&lt;div id="debug"&gt;&lt;/div&gt;

</pre>