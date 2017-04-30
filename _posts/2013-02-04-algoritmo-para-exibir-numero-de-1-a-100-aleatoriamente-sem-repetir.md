---
id: 2899
title: Algoritmo para exibir número de 1 a 100 aleatoriamente, sem repetir
date: 2013-02-04T02:40:14+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2899
permalink: /php/algoritmo-para-exibir-numero-de-1-a-100-aleatoriamente-sem-repetir/
dsq_thread_id:
  - "2103098517"
categories:
  - PHP
---
Acabei de ver um cara perguntando isso no fórum.imasters.

Ele queria saber como exibir aleatoriamente números de 1 a 100, sem repeti-los.
  
Bom, primeiro precisamos dos tais números de 1 a 100

<pre name="code" class="php">$arr = range(1,100);
</pre>

Ok, então preciso exibir cada um desses números aleatoriamente, sem repeti-los.
  
O primeiro código que me veio na cabeça, foi o seguinte:

<pre name="code" class="php">&lt;?php

$arr = range(1,100);

while( sizeof( $arr )>0 )
{
	shuffle( $arr );
	echo $arr[0], '&lt;br />';
	unset( $arr[0] );
}</pre>

Não é o &#8220;melhor&#8221; código, nem o mais performático. Mas não é isso que me fez escrevê-lo.
  
Fiz apenas para &#8220;ver se resolvia&#8221;. Worse is better.

Ok, vamos lá. O loop ali, anda no array até ele &#8220;acabar&#8221;, pois conforme vou exibindo a primeira posição do array, eu removo este item dele. 

Funciona. Mas note o shuffle ali dentro do loop. A cada volta ele é feito desnecessariamente.
  
Se desordenei o array uma vez, não preciso ficar fazendo isso a cada elemento que for exibir. Os próximos elementos já estarão &#8220;em ordem aleatória&#8221;.

Então, esse &#8220;incomodo&#8221; que estava atrapalhando a performance, e tornava o algoritmo mais complicado do que preciso, podemos jogar para fora do loop, e apenas exibir o array:

<pre name="code" class="php">&lt;?php

$arr = range(1,100);

shuffle( $arr );
foreach( $arr AS $each )
{
	echo $each, '&lt;br />';
}</pre>

Bem melhor.
  
Mas o importante foi a iniciativa de começar. Precisei de cerca de 4 minutos para ler o problema, formular o código ruim, e depois chegar a solução final.

O importante é não travar, não ficar só pensando, só especulando.. sem rascunhar, sem tentar.
  
Tente, comece fazendo um código ruim, desde que depois vc o melhore.