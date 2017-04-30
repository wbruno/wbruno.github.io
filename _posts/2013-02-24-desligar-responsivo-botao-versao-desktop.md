---
id: 2916
title: 'Desligar responsivo &#8211; botão versão desktop'
date: 2013-02-24T14:22:20+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2916
permalink: /javascript-puro/desligar-responsivo-botao-versao-desktop/
categories:
  - Javascript
tags:
  - design
---
Esses dias eu li 4 críticas aos layouts responsivos.
  
O cara dizia que o visitante pode &#8220;gostar&#8221; da versão full, e em sites responsivos não existe o botão &#8220;[voltar a versão desktop](http://www.themarketingagents.com/responsive-design-problems)&#8220;.

Bom, por mais que seja discutível esse ponto de vista do cara, eu pensei e há sim uma forma de fazer o botão &#8220;voltar a versão desktop&#8221;, mesmo quando estamos usando media queries, para fazer nosso layout responsivo.

Basta atacar a base dessa técnica, a primeira coisa que a faz funcionar. A meta tag viewport.

Criei um elemento, que no click dele, altera o valor da minha meta viewport.

<pre name="code" class="javascript">d.getElementById('no-responsive').onclick = function(){
			var vps = d.querySelectorAll("meta[name='viewport']");
			vps[0].content = 'width=960px,initial-scale=0.3,user-scalable=yes';
		}
</pre>

Prontinho, feito o botão para ver a versão full. Derrubando o argumento do cara.

**&#8212; update 2013-05-29 &#8212;**

## onOrientationChange

E segue uma versão completa do código, que identifica se o visitante está em landscape ou portrait.

Tem uma chamada ao .innerHTML do elemento #t apenas para debug. Remova quando for usar em produção.

<pre class="html">&lt;!doctype html>
&lt;html lang="en">
&lt;head>
	&lt;meta charset="UTF-8">
	&lt;title>Desligar Responsivo&lt;/title>

	&lt;meta name="viewport" content="width=device-width,initial-scale=1,user-scalable=yes" />
&lt;style>
body { margin: 0; padding: 0; }
&lt;/style>
&lt;/head>
&lt;body>

	&lt;main id="main">
		&lt;h1>Desligar responsivo&lt;/h1>

		&lt;span id="no-responsive">desligar&lt;/span>
		&lt;p id="t">&lt;/p>

	&lt;/main>&lt;!-- #main -->
&lt;script>
(function(w, d, undefined) {
	var viewport = {
		meta : d.querySelectorAll("meta[name='viewport']")[0],
		landscape : function() {
			viewport.meta.content = 'width=960px,initial-scale=1,user-scalable=yes';
			alert('landscape');
		},
		portrait : function() {
			viewport.meta.content = 'width=960px,initial-scale=1,user-scalable=yes';
			alert('portrait');
		},
		orientation : function() {
			if(Math.abs(window.orientation) === 90) {
				viewport.landscape();
			} else {
				viewport.portrait();
			}
			d.getElementById('t').innerHTML = '&lt;strong>viewport:&lt;/strong> ' + viewport.meta.content;
			d.getElementById('t').innerHTML += '&lt;br/>&lt;strong>body.offsetWidth:&lt;/strong> ' + d.querySelector('body').offsetWidth;
		}
	};


	w.onorientationchange = viewport.orientation;
	d.getElementById('no-responsive').onclick = viewport.orientation;


}(window, document));
&lt;/script>
&lt;/body>
&lt;/html>
</pre>