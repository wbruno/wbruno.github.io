---
id: 1630
title: 'Habilitar e Desabilitar inputs e textarea ao clicar em botão &#8211; JavaScript'
date: 2011-11-27T17:09:51+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1630
permalink: /javascript-puro/habilitar-desabilitar-inputs-textarea-ao-clicar-em-botao-javascript/
dsq_thread_id:
  - "2102530361"
categories:
  - Javascript
---
Um botão habilita e outro desabilita, setando .disabled = true;

<!--more-->

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript">
function toogle_disabled( bool )
{
	var input = document.getElementsByTagName('input');
	var textarea = document.getElementsByTagName('textarea');

	for( var i=0; i&lt;=(input.length-1); i++ )
	{
		if( input[i].type!='button' ) 
			input[i].disabled = bool;
	}
	for( var i=0; i&lt;=(textarea.length-1); i++ )
	{
		textareat[i].disabled = bool;
	}
}
&lt;/script>
&lt;/head>
&lt;body>
	&lt;form>
		&lt;input type="button" onclick="toogle_disabled( false )" value="Habilitar" />
		&lt;input type="button" onclick="toogle_disabled( true )" value="Desabilitar" />

		&lt;br />&lt;br />        
		Nome: &lt;input type="text" name="nome" />
		Local: &lt;input type="text" name="local" />
		&lt;br>
		Nome: &lt;input type="text" name="nome2" />
		Local: &lt;input type="text" name="local2" />

	&lt;/form>
&lt;/body>
&lt;/html>
</pre>