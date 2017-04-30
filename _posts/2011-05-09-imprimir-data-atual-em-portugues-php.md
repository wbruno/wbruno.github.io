---
id: 906
title: Imprimir data atual em português com php
date: 2011-05-09T18:58:21+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=906
permalink: /php/imprimir-data-atual-em-portugues-php/
dsq_thread_id:
  - "2100730325"
categories:
  - PHP
---
É simples retornar a data atual em português, sem precisar usar malabarismos com arrays, ifs/elses, switch/case..

O php tem muitas funções, mas nem sempre lembramos de dar uma olhada|pesquisada no manual, antes de tentarmos reinventar a roda.
  
<!--more-->


  
Em php:

<pre name="code" class="php">&lt;?php
	setlocale(LC_ALL, "pt_BR", "pt_BR.iso-8859-1", "pt_BR.utf-8", "portuguese");
	date_default_timezone_set('America/Sao_Paulo');

	$date = '2011-05-08';
	echo strftime("%A, %d de %B de %Y", strtotime( $date ));
</pre>

<a href="http://br2.php.net/manual/pt_BR/function.date-default-timezone-set.php" target="_blank">http://br2.php.net/manual/pt_BR/function.date-default-timezone-set.php</a>

E no SQL: [bem lembrado pelo <a href="http://forum.imasters.com.br/topic/432495-transformar-data-do-banco-de-dados-para-outro-formato/page__view__findpost__p__1707238" target="_blank">@Victor Cometti </a> ]

<pre name="code" class="sql">SET lc_time_names = 'pt_BR';
SELECT DATE_FORMAT(CURDATE(), '%d %b %Y') AS data;</pre>

<a href="http://dev.mysql.com/doc/refman/4.1/pt/date-and-time-functions.html" target="_blank">http://dev.mysql.com/doc/refman/4.1/pt/date-and-time-functions.html</a>

> _&#8220;As restrições impostas por uma dada linguagem de programação ou o conhecimento incompleto das suas potencialidades pode conduzir a raciocínios (e conseqüentes projetos) relativamente limitados.&#8221;_