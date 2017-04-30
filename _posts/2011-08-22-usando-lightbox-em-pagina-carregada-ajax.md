---
id: 1343
title: Usando lightbox em página carregada com ajax
date: 2011-08-22T20:39:59+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1343
permalink: /ajax/usando-lightbox-em-pagina-carregada-ajax/
dsq_thread_id:
  - "2101061489"
categories:
  - AJAX
tags:
  - lightbox
---
Quando trazemos um conteúdo com ajax, inserimos novos elementos no nosso documento.

Porém, convém notar, que essa inserção ocorre **após** o DOM estar pronto [document.ready], e que o que veio com ajax, é apenas **texto puro**. Seja formatado em XML, jSON.. mas ainda assim apenas <u>texto</u>.
  
<!--more-->


  
É por esse motivo que os elementos trazidos com ajax, ainda não possuem os eventos/plugins atrelados a eles, e por isso &#8216;não funcionam&#8217;.

Para ilustrar, veja esse exemplo, usando o código do lightbox do jQuery

## <a href="http://wbruno.com.br/scripts/lightbox-ajax1.html" target="_blank">lightbox carregado com ajax [não funcionando]</a>

Baixei do <a href="http://leandrovieira.com/projects/jquery/lightbox/" target="_blank">site oficial do plugin</a>.
  
Note que com esse script:

<pre name="code" class="javascript:firstLine[28]">$(document).ready(function() {
		$('#content').load('lightbox.html');
		$('#gallery a').lightBox();
	});
</pre>

Não esperamos a requisição terminar. O método **.load()**, faz a requisição de modo assíncrono, isto, é o restante do script não aguarda a requisição terminar para prosseguir. Portanto, a nossa tentativa de instanciar o plugin não funciona.

Temos que fazer essa rotina, assim que os novos elementos forem inseridos no DOM. Olhando o manual do <a href="http://api.jquery.com/load/" target="_blank">.load do jQuery</a>, notamos que a lib disponibiliza um callback para essa situação.

<pre name="code" class="javascript:firstLine[28]">$(document).ready(function() {
		$('#content').load('lightbox.html', 
			function(){
				$('#gallery a').lightBox();
			}
		);
	});
</pre>

E agora, tudo funciona

## <a href="http://wbruno.com.br/scripts/lightbox-ajax2.html" target="_blank">lightbox carregado com ajax [ funcionando ]</a>

Simples, não ?
  
Nem tanto. Não é &#8216;apenas isso&#8217;, ou &#8216;somente isso&#8217;. A solução é simples, porém, sem toda a teoria que me levou a ela, eu não conseguiria saber que era isso que eu deveria fazer.