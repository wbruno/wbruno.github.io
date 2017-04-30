---
id: 1598
title: 'Navegando pela lista do suggest com as setas do teclado &#8211; autocomplete teclado javascript'
date: 2011-11-19T01:15:30+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1598
permalink: /jquery/navegando-pela-lista-suggest-setas-teclado-autocomplete-teclado-javascript/
dsq_thread_id:
  - "2100729243"
categories:
  - jQuery
---
boas pessoal!

Eu já tinha colocado aqui, um <a href="http://wbruno.com.br/2010/01/08/suggest-ajax-jquery-phpmysql/" target="_blank">suggest jQuery com ajax</a>. Pensando como eu poderia deixar o usuário se movimentar pela lista de suggest, usando as setas do teclado, me dei conta que era desnecessário, tentar ficar trocando o .focus() dos elementos.

<!--more-->


  
Na verdade, eu só preciso &#8216;fingir&#8217; isso. Mostrar no input, o .text(), do item do suggest, e mostrar com um background em qual está.
  
Foi oq eu fiz. Bem simples.

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript" src="jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
jQuery(document).ready(function(){
	var active = -1;
	jQuery("input[name='autocomplete']").keypress(function( event ){		
		var suggest_a = jQuery('#suggest a');
		var qnts_a = suggest_a.length;
			
		if( 40==event.keyCode )//seta baixo
			active = active>=(qnts_a-1) ? 0 : active+1;
		else if( 38==event.keyCode )//seta cima
			active = ( active&lt;=0 ) ? qnts_a-1 : active-1;
		
		
		
		var a = suggest_a.removeClass('active').eq( active ).addClass('active');	
		jQuery( this ).val( a.text() );
	});
});
&lt;/script>
&lt;style type="text/css">
label { position: relative; }
#suggest {
	position: absolute;
	top: 20px;
	left: 0;
}
.active {
	background: #ccc;
}
&lt;/style>
&lt;/head>
&lt;body>
	&lt;label>
		&lt;input type="text" name="autocomplete" />
		&lt;ul id="suggest">
			&lt;li>&lt;a href="">Item 1&lt;/a>&lt;/li>
			&lt;li>&lt;a href="">Item 2&lt;/a>&lt;/li>
			&lt;li>&lt;a href="">Item 3&lt;/a>&lt;/li>
			&lt;li>&lt;a href="">Item 4&lt;/a>&lt;/li>
		&lt;/ul>&lt;!-- /suggest -->
	&lt;/label>
&lt;/body>
&lt;/html></pre>

</html>
  
e vc? faria de outro jeito ?

ainda vou pesquisar para ver como &#8216;costumam fazer por ai&#8217;. Essa foi a forma que eu pensei para resolver.