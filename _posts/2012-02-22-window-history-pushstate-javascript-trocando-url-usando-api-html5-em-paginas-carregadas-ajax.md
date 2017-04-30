---
id: 1792
title: 'window.history.pushState javascript &#8211; trocando a URL usando api html5 em páginas carregadas com ajax'
date: 2012-02-22T21:29:46+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1792
permalink: /ajax/window-history-pushstate-javascript-trocando-url-usando-api-html5-em-paginas-carregadas-ajax/
dsq_thread_id:
  - "2100792728"
categories:
  - AJAX
---
Bem simples, só editei o trecho que era necessário para enviar um **history.pushState**, no final da requisição ajax, que carrega a página em uma div, sem dar refresh no restante do site.

<a href="http://wbruno.com.br/2011/05/27/navegacao-sem-refresh-%E2%80%93-carregando-conteudo-ajax-em-div-2/" target="_blank">http://wbruno.com.br/2011/05/27/navegacao-sem-refresh-%E2%80%93-carregando-conteudo-ajax-em-div-2</a>

<pre name="code" class="javascript:firstLine[18]">$.ajax({
	url: href,
	success: function( response ){
		//forçando o parser
		var response = $( '&lt;div>'+response+'&lt;/div>' );
				
		var data = response.find('#content').html();

		//apenas atrasando a troca, para mostrarmos o loading
		window.setTimeout( function(){
			content.fadeOut('slow', function(){
				content.html( data ).fadeIn();
							
				var title = response.find('title').text();
				window.history.pushState( href, title, href );
				document.title = title;
			});
		}, 500 );
	}
});
</pre>

Notem a linha:

<pre name="code" class="javascript:firstLine[31]">window.history.pushState( href, response.find('title'), href );</pre>

É essa nova função que veio junto com o HTML5, que faz toda a mágica.
  
Browsers antigos não implementam esse método.

Agora podemos parar de forçar a barra usando o document.location.hash, como nessa implementação aqui:
  
<a href="http://wbruno.com.br/2011/11/25/carregando-conteudo-ajax-trocando-url-jquery/" target="_blank">http://wbruno.com.br/2011/11/25/carregando-conteudo-ajax-trocando-url-jquery/</a>

## <a href="http://wbruno.com.br/scripts/fotos2.html" target="_blank">Demonstração</a>

É isso. Dúvidas ? pergunte, comente!