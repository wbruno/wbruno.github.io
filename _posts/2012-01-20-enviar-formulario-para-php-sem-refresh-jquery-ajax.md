---
id: 1732
title: 'Enviar formulário para o php sem refresh &#8211; jQuery.ajax'
date: 2012-01-20T07:00:31+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1732
permalink: /ajax/enviar-formulario-para-php-sem-refresh-jquery-ajax/
dsq_thread_id:
  - "2100717333"
categories:
  - AJAX
tags:
  - formulário
---
Eu havia postado, como enviar um formulário com ajax, aproveitando o callback <a href="http://wbruno.com.br/2011/03/21/validar-enviar-formulario-ajax-usando-jquery-validate/" target="_blank">submitHandler do jQuery.validate</a>.

Porém, se vc não estiver usando esse plugin, e quiser apenas usar o ajax do jQuery, o seguinte basta:
  
<!--more-->

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js">&lt;/script>
	&lt;script type="text/javascript">
	jQuery(document).ready(function(){
		jQuery('#ajax_form').submit(function(){
			var dados = jQuery( this ).serialize();

			jQuery.ajax({
				type: "POST",
				url: "processa.php",
				data: dados,
				success: function( data )
				{
					alert( data );
				}
			});
			
			return false;
		});
	});
	&lt;/script>
&lt;/head>
&lt;body>
	&lt;form method="post" action="" id="ajax_form">
		&lt;label>&lt;input type="hidden" name="id" value="" />&lt;/label>
		&lt;label>Nome: &lt;input type="text" name="nome" value="" />&lt;/label>
		&lt;label>Email: &lt;input type="text" name="email" value="" />&lt;/label>
		&lt;label>Telefone: &lt;input type="text" name="telefone" value="" />&lt;/label>

		&lt;label>&lt;input type="submit" name="enviar" value="Enviar" />&lt;/label>
	&lt;/form>
&lt;/body>
&lt;/html>
</pre>

Primeiro eu importo a lib jQuery:

<pre name="code" class="html:firstLine[3]">&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js">&lt;/script></pre>

Nada de novo até aqui.

Faço corretamente, e disparo a minha função no evento onsubmit do formulário:

<pre name="code" class="javascript:firstLine[6]">jQuery('#ajax_form').submit(function(){</pre>

Vi alguns tutoriais( de blogs, fóruns e video aulas ), usando o evento **onclick** do botão submit(ou button), &#8220;fingem&#8221;, que isso funciona, e depois várias pessoas vão aos fóruns, por causa dos problemas gerados por esses códigos mal escritos e incorretos.

O correto é usar no **onsubmit** do form, e &#8220;desativar&#8221; ele, com aquele return false; que envio na linha 19

<pre name="code" class="javascript:firstLine[19]">return false;</pre>

Daí em diante, não tem segredo, é o mesmo miolo que usei para enviar com o jQuery.validate.
  
De graça, o método <a href="http://api.jquery.com/serialize/" target="_blank">.serialize()</a>, cria a query string com os dados do formulário, e usamos essa variavel para enviar a função ajax.

Ali no <var>success: function( data ) </var> (linha 13), é o callback que será disparado, assim que a requisição retornar(status 200 e tal).

Bom, é isso =)
  
Comentem, compartilhem. Sei que é um assunto já bastante &#8220;batido&#8221;, porém não me custava deixar um código bem escrito, até para tentar minimizar os efeitos dos maus tutoriais.