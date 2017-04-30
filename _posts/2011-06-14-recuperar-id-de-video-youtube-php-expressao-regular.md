---
id: 1086
title: 'Recuperar ID de vídeo do Youtube &#8211; php Expressão Regular'
date: 2011-06-14T03:00:26+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1086
permalink: /php/recuperar-id-de-video-youtube-php-expressao-regular/
dsq_thread_id:
  - "2102873270"
categories:
  - PHP
tags:
  - youtube
---
Não raramente fazemos sistemas em que precisamos embedar vídeos do youtube no site de nossos clientes.
  
<!--more-->

Até para deixar registrado aqui, nesse meu repositório, esta foi a ER que utilizei recentemente:

<pre name="code" class="php">&lt;?php

		preg_match( '/(v=)([^&]+)/', 'http://www.youtube.com/watch?v=K0e1DbvE0bg&feature=topvideos_music', $matches ); 
		
		var_dump( $matches[2] );
		return $matches;
</pre>

é isso, post rápido.