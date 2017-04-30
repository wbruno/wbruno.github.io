---
id: 2554
title: Como fazer Tabela Zebrada CSS 3, javascript e php
date: 2012-08-17T07:00:20+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2554
permalink: /css/tabela-zebrada-css-3/
dsq_thread_id:
  - "2113815523"
categories:
  - CSS
tags:
  - tabela zebrada
---
Muito comum, ne?! Todos nós já tivemos um dia que fazer uma tabela zebrada. Mas você ja tinha feito tabela zebrada css 3 ?

Eu por exemplo, já fiz diversas vezes isso do lado server-side, durante a listagem de dados, calculando um contador dentro do loop de registros. Algo parecido com isso aqui:
  
<!--more-->

## Tabela Zebrada em php

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;meta charset="utf8" />
&lt;style type="text/css">
.dif { background: #ccc; }
&lt;/style>
&lt;/head>
&lt;body>
&lt;?php

	$data = Array(
			0 => Array( 'name'=> 'William Moraes', 'idade'=> '23 anos', 'alias'=> 'wbruno' ),
			1 => Array( 'name'=> 'Marco Silva', 'idade'=> '24 anos', 'alias'=> 'jorge alex' ),
			2 => Array( 'name'=> 'Marcio Hanashiro', 'idade'=> '25 anos', 'alias'=> 'japa' ),
			3 => Array( 'name'=> 'Dany Garrido', 'idade'=> 'não sei', 'alias'=> 'delicinha' ),
			4 => Array( 'name'=> 'Heric Tilly', 'idade'=> '32 anos', 'alias'=> 'tilly' ),
			5 => Array( 'name'=> 'Felipe Marx', 'idade'=> 'não sei', 'alias'=> 'marx' ),
			6 => Array( 'name'=> 'Camila Kamimura', 'idade'=> 'não sei', 'alias'=> 'japinha' ),
			7 => Array( 'name'=> 'Raquel Dalastti', 'idade'=> 'não sei', 'alias'=> 'dalastti' ),
			8 => Array( 'name'=> 'Bianca Lu', 'idade'=> 'não sei', 'alias'=> 'luttenchuijlkwypl' ),
			9 => Array( 'name'=> 'Jacqueline Pereira', 'idade'=> 'não sei', 'alias'=> 'jacque' )
		);

	echo '&lt;table id="tabela-zebrada">
		&lt;thead>
			&lt;tr>
				&lt;th>Nome&lt;/th>
				&lt;th>Idade&lt;/th>
				&lt;th>Alias&lt;/th>
			&lt;/tr>
		&lt;/thead>';

	echo '&lt;tbody>';

	$i = 0;
	foreach( $data AS $item ){
		$class = $i%2==0 ? ' class="dif"' : '';
		echo '&lt;tr'.$class.'>
			&lt;td>'.$item['name'].'&lt;/td>
			&lt;td>'.$item['idade'].'&lt;/td>
			&lt;td>'.$item['alias'].'&lt;/td>
		&lt;/tr>';

		$i++;
	}
	echo '&lt;/tbody>
	&lt;/table>';
?>

&lt;/body>
&lt;/html>
</pre>

Lógico que funciona. Mas hoje em dia, não é mais a única forma de fazer esse efeito.

Podemos por exemplo, fazer tabela zebrada com javascript:

## Tabela Zebrada em javascript

<pre name="code" class="php">&lt;script type="text/javascript">
window.onload = function(){
	var trs = id('tabela-zebrada').getElementsByTagName('tbody')[0].getElementsByTagName('tr');

	for( var i=0, max = trs.length; i&l;max; i++ ){
		if( i%2==0 ) trs[i].className = 'dif';
	}
}
var id = function( el ){
	return document.getElementById( el );
}
&lt;/script>
</pre>

Entretanto, ainda assim não é muito mais natural esses cálculos tecnicamente simples, ficarem a cargo de linguagens como esstas. Podemos usar seletores css para zebrar tabelas, selecionar primeiros ou últimos elementos, ímpares, pares.. 

## Tabela Zebrada CSS 3

Hoje em dia, podemos usar o poderoso seletor css nth-child das css 3, assim como o Marco Bruno, mostrou que é possível, [Tabela Zebrada CSS 3 – Pseudo Seletor nth-child](http://marcobruno.com.br/css3/tabela-zebrada-css-3/ "Tabela Zebrada CSS 3 – Pseudo Seletor nth-child").

<pre name="code" class="css">&lt;style type="text/css">
#tabela-zebrada tbody tr:nth-child(2n+1) { background: #ccc; }
&lt;/style></pre>

Simples, não ?
  
E muito mais intuitivo. Já que estilização é dever da linguagem css, então, o seletor nth-child veio para nos ajudar a não misturar as camadas de desenvolvimento.