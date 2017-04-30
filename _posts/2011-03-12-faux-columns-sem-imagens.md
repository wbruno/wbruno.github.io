---
id: 186
title: Faux Columns sem imagens
date: 2011-03-12T00:01:07+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=186
permalink: /css/faux-columns-sem-imagens/
dsq_thread_id:
  - "2100746429"
categories:
  - CSS
---
Achei <a href="http://www.positioniseverything.net/articles/onetruelayout/equalheight" target="_blank">este artigo</a>, que resolve o problema de **ter que se ter** colunas com mesma altura, **mas sem usar imagens**, como na [solução tradicional](http://forum.imasters.uol.com.br/index.php?showtopic=225319).
  
A renderização sem nenhuma técnica, para 3 colunas com diferentes alturas, é esta:
  
<a href="http://wbruno.com.br/scripts/semFauxColumns.html" target="_blank">http://wbruno.com.br/scripts/semFauxColumns.html</a>

E agora, aplicando a técnica de faux-columns, mas sem imagens, sugerida no artigo acima:
  
<a href="http://wbruno.com.br/scripts/comFauxColumns.html" target="_blank">http://wbruno.com.br/scripts/comFauxColumns.html</a>

A grande &#8220;chave&#8221; para essa técnica, é atribuir &#8220;overflow: hidden&#8221; para o container, e colocar margins e paddings gigantes para as colunas:

<pre name="code" class="css">#colunaUm {
	background-color: #ff0;
	padding-bottom: 1000em;
	margin-bottom: -999.5em;
}</pre>

você pode verificar o código completo nos links que postei para exemplo, e vizualização.

Usei para esse exemplo, um [gerador de Lorem Ipsum](http://lipsum.com)

Testado:
  
Opera 9.5 Beta
  
FireFox 3
  
Internet Explorer 7
  
Internet Explorer 6
  
Internet Explorer 8 (Beta)
  
Google Chrome Beta
  
Safari 3.1.2 (Windows)
  
Iceweasel 3.0.6 (Linux)
  
Web Epiphany 2.22.3 (Linux)

Postado originalmente <a href="http://forum.imasters.uol.com.br/index.php?/topic/309442-solucao-para-faux-columns-sem-usar-imagens/" target="_blank">aqui</a>

source:

<pre name="code" class="html">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
	"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml" xml:lang="pt-br" lang="pt-br"&gt;
&lt;head&gt;
	&lt;style type="text/css"&gt;
	* { margin: 0; padding: 0; }
	#container { width: 600px; margin: 0 auto; overflow: hidden; }
	#colunaUm,
	#colunaDois,
	#colunaTres {
		width: 200px;
		float: left;
		padding-bottom: 1000em;
		margin-bottom: -999.5em;
	}
	#colunaUm {
		background: #ff0;
	}
	#colunaDois {
		background: #f0f;
	}
	#colunaTres{
		background: #0ff;
	}
	&lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;

	&lt;div id="container"&gt;
		&lt;div id="colunaUm"&gt;
			&lt;/p&gt;Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed mi tortor, fringilla nec imperdiet id,
			mollis vitae justo. Quisque in urna odio. Cras in dignissim orci. Quisque pellentesque &lt;/p&gt;
		&lt;/div&gt;&lt;!-- /coluna1 --&gt;

		&lt;div id="colunaDois"&gt;
			&lt;/p&gt;Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed mi tortor, fringilla nec imperdiet id,
			mollis vitae justo. Quisque in urna odio. Cras in dignissim orci. Quisque pellentesque justo varius
			quam rhoncus imperdiet. Sed eleifend molestie nisi, ultricies interdum turpis ultrices sit amet.
			Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Nulla &lt;/p&gt;
		&lt;/div&gt;&lt;!-- /coluna2 --&gt;
		&lt;div id="colunaTres"&gt;
			&lt;/p&gt;Lorem ipsum &lt;/p&gt;
		&lt;/div&gt;&lt;!-- /coluna3 --&gt;
	&lt;/div&gt;&lt;!-- /container --&gt;

&lt;/body&gt;
&lt;/html&gt;</pre>