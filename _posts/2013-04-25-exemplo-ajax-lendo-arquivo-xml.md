---
id: 2948
title: Exemplo ajax lendo arquivo xml
date: 2013-04-25T11:54:50+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2948
permalink: /ajax/exemplo-ajax-lendo-arquivo-xml/
dsq_thread_id:
  - "2102693168"
categories:
  - AJAX
tags:
  - xml
---
Ler arquivo xml com ajax.. bem simples. Vamos lá

<pre class="xml">&lt;?xml version="1.0" encoding="UTF-8"?>
&lt;text>
	&lt;p>Lorem ipsum dolor sit amet&lt;/p>
	&lt;p>Nihil cumque vero&lt;/p>
	&lt;p>Impedit quibusdam fuga&lt;/p>
	&lt;p>Magnam ad maiores omnis&lt;/p>
	&lt;p>Aliqua omnis laborum&lt;/p>
&lt;/text>
</pre>

<!--more-->


  
E o código ajax necessário para abrir esse xml, e mostrar a segunda tag <p> dele

<pre class="javascript">&lt;script type="text/javascript">
var ajax = new XMLHttpRequest();

ajax.open("GET","test.xml",true);
ajax.send();

ajax.onreadystatechange = function(){
	if (ajax.readyState == 4){
		var xml = ajax.responseXML;

		console.log(xml.getElementsByTagName('p')[1].innerHTML);
	}
}
&lt;/script>
</pre>