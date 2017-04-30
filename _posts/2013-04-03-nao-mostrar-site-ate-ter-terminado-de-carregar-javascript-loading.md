---
id: 2938
title: 'Não mostrar site até ter terminado de carregar &#8211; JavaScript (loading)'
date: 2013-04-03T14:43:42+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2938
permalink: /html/nao-mostrar-site-ate-ter-terminado-de-carregar-javascript-loading/
dsq_thread_id:
  - "2100912298"
categories:
  - HTML
---
Com js eu escondo o elemento de id=&#8221;all&#8221;, para depois no evento onload mostrar ele novamente, e ai esconder o gif de loading.

Código bem simples, não, não me orgulho dele. Apenas fiz pq tem outros muito piores por ai, e um cara no iMasters perguntou.

Note que usei 5 wallpapers grandes, para demorar um pouco para carregar, e o efeito ser visto.
  
Não é obstrutivo, pois escondo com js.

<pre name="code" class="javascript">&lt;!doctype html>
&lt;html lang="en">
&lt;head>
	&lt;meta charset="UTF-8">
	&lt;title>Teste&lt;/title>

&lt;script type="text/javascript">
function id(el) {
	return document.getElementById(el);
}
function hide(el) {
	id(el).style.display = 'none';//escondendo tudo
}
window.onload = function() {
	id('all').style.display = 'block';//liberando qndo terminar
	hide('loading');
}
&lt;/script>
&lt;style>
#loading { 
	display: block;
	width: 200px;
}
.content { margin: 0 auto; }
#all {
	width: 1280px; overflow: hidden;
}
&lt;/style>
&lt;/head>
&lt;body>
	&lt;section id="all" class="content">
		&lt;img src="http://fc03.deviantart.net/fs25/f/2009/250/e/5/Within_Temptation___Utopia_by_KigaMistriver.jpg" alt="">
		&lt;img src="http://images.fanpop.com/images/image_uploads/within-temptation-within-temptation-595989_1672_1417.jpg" alt="">
		&lt;img src="http://images4.alphacoders.com/247/247868.gif" alt="">
		&lt;img src="http://www.withinforever.xpg.com.br/within_temptation_wallpaper_3_1024x768.jpg" alt="">
	&lt;/section>&lt;!-- #all -->

	&lt;img src="http://3.bp.blogspot.com/-Bo2GNAVNb90/URkAlN-0V_I/AAAAAAAACfs/VHFT6oP1ZTk/s1600/Loading+-+Carregando+%252826%2529.gif" alt="" id="loading" class="content"/>


&lt;script type="text/javascript">
	hide('all');
&lt;/script>

&lt;/body>
&lt;/html>
</pre>