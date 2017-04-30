---
id: 1613
title: Slideshow JavaScript com botões de comando(play,stop,prev e next) usando o jQuery.Cycle
date: 2011-11-24T00:47:12+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1613
permalink: /jquery/slideshow-javascript-botoes-de-comandoplaystopprev-next-usando-jquery-cycle/
dsq_thread_id:
  - "2100808187"
categories:
  - jQuery
tags:
  - plugin
  - slideshow
---
Coisa rápida&#8230; nosso velho e conhecido slideshow.
  
Porém, denovo, apenas para deixar registrado aqui, a flexibilidade de uso do plugin jQuery.Cycle, e a facilidade de implementação.

<!--more-->

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.0/jquery.min.js">&lt;/script>
&lt;script type="text/javascript" src="js/jquery.cycle-2.97.all.min.js">&lt;/script>
&lt;script type="text/javascript">
jQuery(document).ready(function(){
	jQuery('#slideshow2').cycle({
		fx: 'fade',
		next: '#proxima',
		prev: '#anterior'
	});
	jQuery('#pausa').click(function(){
		$('#slideshow2').cycle('pause');
	});
	jQuery('#play').click(function(){
		$('#slideshow2').cycle('resume');
	});
});
&lt;/script>
&lt;style type="text/css">
* {
	margin: 0; padding: 0; border: none;
}
body { font: 12px Arial; }
#slideshow2 {
	list-style: none;
	height: 185px;
	width: 220px;
	overflow: hidden;
}
#slideshow2 li {
	height: 100%;	
}
#slideshow2 p {
	font-weight: bold;
	font-size: 13px;
}
#ctrls img { cursor: pointer; }
&lt;/style>
&lt;/head>
&lt;body>
	&lt;ul id="slideshow2">
		&lt;li>
			&lt;a href="?noticia=2660/nivel-de-estoques-de-aco-e-positivo--mas-perspectiva-e-de-queda-dos-precos-do-setor">
				&lt;img src="uploads/20111123-213901.jpg" alt="Metalurgia e Distribuição" />
			&lt;/a>
			&lt;p>Nível de estoques de aço é positivo, mas perspectiva é de queda d...&lt;/p>
		&lt;/li>
		&lt;li>
			&lt;a href="?noticia=2660/nivel-de-estoques-de-aco-e-positivo--mas-perspectiva-e-de-queda-dos-precos-do-setor">
				&lt;img src="uploads/20111123-213612.jpg" alt="Metalurgia e Distribuição" />
			&lt;/a>
			&lt;p>Inscrições para concurso da Petrobras começam nesta quinta salári...&lt;/p>
		&lt;/li>
		&lt;li>
			&lt;a href="?noticia=2660/nivel-de-estoques-de-aco-e-positivo--mas-perspectiva-e-de-queda-dos-precos-do-setor">
				&lt;img src="uploads/20111122-230224.jpg" alt="Metalurgia e Distribuição" />
			&lt;/a>
			&lt;p>Engenheiro norte-americano cria moto elétrica com uma roda só&lt;/p>
		&lt;/li>	
	&lt;/ul>&lt;!-- /slideshow2 -->
	
	&lt;div id="ctrls">
		&lt;img src="img/slide_anterior.gif" width="76px" height="20px" alt="anterior" id="anterior" />
		&lt;img src="img/slide_play.gif" width="23px" height="20px" alt="play" id="play" />
		&lt;img src="img/slide_pausa.gif" width="23px" height="20px" alt="pausa" id="pausa" />
		&lt;img src="img/slide_proxima.gif" width="73px" height="20px" alt="proxima" id="proxima" />
	&lt;/div>&lt;!-- /ctrls -->
&lt;/body>
&lt;/html>
</pre>

É isso ai. Comentem! 

## [Demonstração](/scripts/slide-ctrls.html)