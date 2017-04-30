---
id: 475
title: Adicionar inputs, com opção de removê-los
date: 2011-04-01T07:00:13+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=475
permalink: /jquery/adicionar-inputs-opcao-de-remove-los/
dsq_thread_id:
  - "2104496516"
categories:
  - jQuery
tags:
  - framework
---
Post rápido hoje.
  
Script melhorado de uma dúvida que surgiu no iMasters.
  
Sobre esse mesmo assunto, eu já tinha feito [esse post aqui meu](http://www.wbruno.com.br/2011/02/04/criar-input-no-onblur-e-receber-dados-array-php/), porém como o fluxo de interação do usuário é diferente, valeu a pena postar &#8216;de novo&#8217;.

<!--more-->

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript" src="http://code.jquery.com/jquery-1.5.1.min.js">&lt;/script>
&lt;script type="text/javascript">
$(document).ready(function(){

	var input = '&lt;label>Nome: &lt;input type="text" name="foto[]" /> &lt;a href="#" class="remove">X&lt;/a>&lt;/label>';

	$("input[name='add']").click(function( e ){
		$('#inputs_adicionais').append( input );
	});

	$('#inputs_adicionais').delegate('a','click',function( e ){
		e.preventDefault();
		$( this ).parent('label').remove();
	});

});
&lt;/script>
&lt;style type="text/css">
fieldset { border: none; }
label { display: block; }
.remove { color:black;font-weight:bold;text-decoration:none; }
&lt;/style>
&lt;/head>
&lt;body>

	&lt;form action="" method="post">
		&lt;label>&lt;input type="button" name="add" value="Add" />&lt;/label>
			&lt;label>Nome: <input type="text" name="foto[]" />&lt;/label>

		&lt;fieldset id="inputs_adicionais">
		&lt;/fieldset>
	&lt;/form>
&lt;/body>
&lt;/html>
</pre>

Alguns pontos importantes
  
-> Uso o .delegate() no lugar do [.live()](http://www.wbruno.com.br/2011/03/18/metodo-live-jquery/)
  
-> indentei corretamente o script
  
-> sempre uso aspas duplas para delimitar os valores dos atributos HTML
  
-> não desperdiço IDs, e uso bem os seletores da lib
  
-> semântica na marcação do formulário

É isso ai. Se tiverem alguma sugestão de script, podem me encaminhar.