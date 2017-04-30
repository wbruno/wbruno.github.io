---
id: 1038
title: Navegação sem refresh – carregando conteúdo com ajax em div 2
date: 2011-05-27T07:00:13+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1038
permalink: '/ajax/navegacao-sem-refresh-%e2%80%93-carregando-conteudo-ajax-em-div-2/'
dsq_thread_id:
  - "2100751624"
categories:
  - AJAX
tags:
  - navegação
---
Eu já havia postado essa solução: <http://wbruno.com.br/ajax/navegacao-sem-refresh-carregando-conteudo-ajax-em-div/>.

Porém, ai a galera começa a querer um &#8216;efeito de fade&#8217;, &#8216;um gif de carregando..&#8217;.
  
E para resolve isso, é melhor que descartemos a função **.load()** do jQuery, para usarmos uma em que temos mais controle do que está ocorrendo.
  
<!--more-->


  
Nesse caso, vou optar pelo **$.ajax**, já que **$.get** e **$.post**, são apenas atalhos para ela.
  
A maior alteração, será nesse trecho do script anterior:

<pre name="code" class="js:firstLine[11]">$("#content").load( href +" #content");</pre>

Vamos fazer algo mais sofisticado.

<pre name="code" class="html">&lt;html&gt;
&lt;head&gt;
	&lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" /&gt;

	&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.6.1/jquery.min.js"&gt;&lt;/script&gt;
	&lt;script type="text/javascript"&gt;
	$(document).ready(function(){
		var content = $('#content');

		//pre carregando o gif
		loading = new Image(); loading.src = 'loading.gif';
		$('#menu a').live('click', function( e ){
			e.preventDefault();
			content.html( '&lt;img src="loading.gif" />' );

			var href = $( this ).attr('href');
			$.ajax({
				url: href,
				success: function( response ){
					//forçando o parser
					var data = $( '&lt;div&gt;'+response+'&lt;/div&gt;' ).find('#content').html();

					//apenas atrasando a troca, para mostrarmos o loading
					window.setTimeout( function(){
						content.fadeOut('slow', function(){
							content.html( data ).fadeIn();
						});
					}, 500 );
				}
			});

		});
	});
	&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
	&lt;ul id="menu"&gt;
		&lt;li&gt;&lt;a href="index.html"&gt;Home&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="fotos.html"&gt;Fotos&lt;/a&gt;&lt;/li&gt;
		&lt;li&gt;&lt;a href="contato.html"&gt;Contato&lt;/a&gt;&lt;/li&gt;
	&lt;/ul&gt;&lt;!-- /menu --&gt;
	&lt;div id="content"&gt;
		&lt;h1&gt;Bem Vindo!&lt;/h1&gt;
		&lt;p&gt;Essa eh a home desse nome pseudo-site.&lt;/p&gt;
	&lt;/div&gt;&lt;!-- /content --&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

Apenas lembrando que as páginas internas, devem continuar com o código HTML completo, pois queremos que nosso site continue funcionando caso não haja suporte a javascript no navegador do usuário.

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
&lt;/head>
&lt;body>
	&lt;ul id="menu">
		&lt;li>&lt;a href="index.html">Home&lt;/a>&lt;/li>
		&lt;li>&lt;a href="fotos.html">Fotos&lt;/a>&lt;/li>
		&lt;li>&lt;a href="contato.html">Contato&lt;/a>&lt;/li>
	&lt;/ul>&lt;!-- /menu -->
	&lt;div id="content">
		&lt;h1>Fotos&lt;/h1>
		

		Fotos fotos fotos
	&lt;/div>&lt;!-- /content -->
&lt;/body>
&lt;/html>
</pre>

## <a href="http://wbruno.com.br/scripts/ajaxdiv.html" target="_blank">Demonstração</a>

## Se vc já usou esse script

E **teve problemas** com os outros scripts do seu site, veja estes links:

[Usando lightbox em página carregada com ajax](http://wbruno.com.br/2011/08/22/usando-lightbox-em-pagina-carregada-ajax/) 
  
[Carregando conteudo com ajax, trocando a URL com jQuery](http://wbruno.com.br/2011/11/25/carregando-conteudo-ajax-trocando-url-jquery/) 
  
[O método .live() do jQuery](http://wbruno.com.br/2011/03/18/metodo-live-jquery/) 
  
[Como debugar JavaScript com o Firefox ? – erros comuns](http://wbruno.com.br/2011/03/31/como-debugar-javascript-firefox-erros-comuns/)