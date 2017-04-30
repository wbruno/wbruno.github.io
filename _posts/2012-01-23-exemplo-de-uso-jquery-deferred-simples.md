---
id: 1739
title: 'Exemplo de uso jQuery.Deferred &#8211; simples'
date: 2012-01-23T07:00:54+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1739
permalink: /jquery/exemplo-de-uso-jquery-deferred-simples/
dsq_thread_id:
  - "2101351878"
categories:
  - jQuery
---
Talvez esteja faltando algo &#8220;simples&#8221;, situações &#8220;cotidianas&#8221;, ou sei lá oque.
  
<!--more-->


  
Estou vendo muitas pessoas no fórum com a mesma dúvida: &#8220;usar o objeto Deferred do jQuery&#8221;, &#8220;pegar o retorno de uma requisição ajax&#8221;, e coisas relacionadas.

Eu sempre indico o ótimo tutorial do Maujor:
  
[http://www.maujor.com/blog/2011/02/01/o-objeto-deferred-da-jquery-1-5](http://www.maujor.com/blog/2011/02/01/o-objeto-deferred-da-jquery-1-5 "O Objeto Deferred da jQuery 1.5"), porém talvez por ser tão completo, e ter tantas informações, alguns iniciantes podem não estar &#8220;entendendo&#8221;.

Vou deixar alguns exemplos práticos(todos com o mesmo resultado), de algumas formas de usar o Deferred:

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js">&lt;/script>
	&lt;script type="text/javascript">
	jQuery(document).ready(function(){
		/* retorna undefined */
		jQuery('#ajax_form_undefined').submit(function(){
			var form = jQuery( this );
			var ret = envia_form_nao_funciona( form );
			alert( ret );
			return false;
		});
		
		/* enviando ajax_form com done */
		jQuery('#ajax_form').submit(function(){

			var ret = envia_form( jQuery( this ) );
			ret.done(function( dados ){
				alert( dados );
			});
			
			return false;
		});
		
		/* enviando ajax_form2 com then */
		jQuery('#ajax_form2').submit(function(){

			var ret = envia_form( jQuery( this ) );
			ret.then(function( dados ){
				alert( dados );
			});
			
			return false;
		});
		
		/* enviando ajax_form3 com success */
		jQuery('#ajax_form3').submit(function(){

			var ret = envia_form( jQuery( this ) );
			ret.success(function( dados ){
				alert( dados );
			});
			
			return false;
		});
	});
	function envia_form_nao_funciona( form )
	{
		jQuery.ajax({
			type: form.attr('method'),
			url: form.attr('action'),
			data: form.serialize(),
			success: function( dados ){
				return dados 
			}
		});		
	}
	function envia_form( form )
	{
		return jQuery.ajax({
			type: form.attr('method'),
			url: form.attr('action'),
			data: form.serialize()
		});		
	}
	&lt;/script>
&lt;/head>
&lt;body>
	&lt;h2>Exemplo do que "não funciona"(retorna undefined)&lt;/h2>
	&lt;form method="post" action="processa.php" id="ajax_form_undefined">
		&lt;label>&lt;input type="hidden" name="id" value="" />&lt;/label>
		&lt;label>Nome: &lt;input type="text" name="nome" value="nome1" />&lt;/label>
		&lt;label>Email: &lt;input type="text" name="email" value="email1" />&lt;/label>

		&lt;label>&lt;input type="submit" name="enviar" value="Enviar" />&lt;/label>
	&lt;/form>
	
	&lt;h2>Recebendo com done&lt;/h2>
	&lt;form method="post" action="processa.php" id="ajax_form">
		&lt;label>&lt;input type="hidden" name="id" value="" />&lt;/label>
		&lt;label>Nome: &lt;input type="text" name="nome" value="nome2" />&lt;/label>
		&lt;label>Email: &lt;input type="text" name="email" value="email2" />&lt;/label>

		&lt;label>&lt;input type="submit" name="enviar" value="Enviar" />&lt;/label>
	&lt;/form>
	
	&lt;h2>Recebendo com then&lt;/h2>
	&lt;form method="post" action="processa.php" id="ajax_form2">
		&lt;label>&lt;input type="hidden" name="id" value="" />&lt;/label>
		&lt;label>Nome: &lt;input type="text" name="nome" value="nome3" />&lt;/label>
		&lt;label>Email: &lt;input type="text" name="email" value="email3" />&lt;/label>

		&lt;label>&lt;input type="submit" name="enviar" value="Enviar" />&lt;/label>
	&lt;/form>

	&lt;h2>Recebendo com success&lt;/h2>	
	&lt;form method="post" action="processa.php" id="ajax_form3">
		&lt;label>&lt;input type="hidden" name="id" value="" />&lt;/label>
		&lt;label>Nome: &lt;input type="text" name="nome" value="nome4" />&lt;/label>
		&lt;label>Email: &lt;input type="text" name="email" value="email4" />&lt;/label>

		&lt;label>&lt;input type="submit" name="enviar" value="Enviar" />&lt;/label>
	&lt;/form>
&lt;/body>
&lt;/html>
</pre>

## <a href="http://wbruno.com.br/scripts/ajax_form_deferred.html" target="_blank">Demonstração online</a>

Convém lembrar que &#8220;precisamos&#8221; do deferred por causa do **assincronismo** das requisições, ou seja, o objeto ajax, envia para o servidor, o servidor processa, e o objeto ajax trás o retorno, sem refresh, porém também, sem que o restante do script aguarde esse retorno.

É essa diferença entre &#8220;sincrono&#8221; e &#8220;assincrono&#8221;. Note que enviando em modo sincrono **async: false,**, eu consigo &#8220;pegar o retorno&#8221; do ajax.

<pre name="code" class="javascript">jQuery(document).ready(function(){
		/* retorna undefined */
		jQuery('#ajax_form_sincrono').submit(function(){
			var form = jQuery( this );
			var ret = envia_form_sincrono( form );
			alert( ret );
			return false;
		});

	});
	function envia_form_sincrono( form )
	{
		var ret = '';
		jQuery.ajax({
			type: form.attr('method'),
			url: form.attr('action'),
			data: form.serialize(),
			async: false,
			success: function( dados ){
				ret = dados;
			}
		});
		return ret;
	}
</pre>

E ai ? qual dos dois usar ? sincrono ? ou assincrono com o deffered ?
  
Não sei, isso depende da sua aplicação, e é assunto para um próximo post talvez.

Usou ? comente.. este é o &#8220;meu pagamento&#8221; pelo que escrevo: o teu comentário.