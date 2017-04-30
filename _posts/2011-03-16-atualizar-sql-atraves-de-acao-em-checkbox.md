---
id: 241
title: Atualizar SQL através de ação em checkbox
date: 2011-03-16T00:12:46+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=241
permalink: /jquery/atualizar-sql-atraves-de-acao-em-checkbox/
categories:
  - jQuery
---
Boas Galera !

Exemplo rápido, o &#8216;dificil&#8217; aqui, seria apenas descobrir o ID do registro, mas isso resolvi com um **.next()**, pois guardei num hidden ali, o id do registro.

é a idéia de GRID que vamos reproduzir. Desmarca o checkbox, atualiza para 0 um campo da tabela, referente aquele ID, marca o checkbox, atualiza para 1.

<!--more-->

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js">&lt;/script>
	&lt;script type="text/javascript">
	$(document).ready(function(){
		$("input[name='status[]']").click(function(){
			var $this = $( this );//guardando o ponteiro em uma variavel, por performance


			var status = $this.attr('checked') ? 1 : 0;
			var id = $this.next('input').val();


			$.ajax({
				url: 'action.php',
				type: 'GET',
				data: 'status='+status+'&id='+id,
				success: function( data ){
					alert( data );
				}
			});
		});
	});
	&lt;/script>
&lt;/head>
&lt;body>
	&lt;form action="" method="post">
		&lt;table>
			&lt;thead>
				&lt;tr>
					&lt;th>ID&lt;/th>
					&lt;th>Nome&lt;/th>
					&lt;th>Status&lt;/th>
				&lt;/tr>
			&lt;/thead>
			&lt;tbody>
				&lt;tr>
					&lt;td>15&lt;/td>
					&lt;td>Resident Evil&lt;/td>
					&lt;td>&lt;input type="checkbox" name="status[]" value="1" />
						&lt;input type="hidden" name="id" value="15" />&lt;/td>
				&lt;/tr>
				&lt;tr>
					&lt;td>17&lt;/td>
					&lt;td>Tomb Raider&lt;/td>
					&lt;td>&lt;input type="checkbox" name="status[]" value="1" />
						&lt;input type="hidden" name="id" value="17" />&lt;/td>
				&lt;/tr>
				&lt;tr>
					&lt;td>21&lt;/td>
					&lt;td>Prince of Persia&lt;/td>
					&lt;td>&lt;input type="checkbox" name="status[]" value="1" />
						&lt;input type="hidden" name="id" value="21" />&lt;/td>
				&lt;/tr>
			&lt;/tbody>
		&lt;/table>
	&lt;/form>
&lt;/body>
&lt;/html>
</pre>

**action.php**

<pre name="code" class="php">&lt;?php
	ini_set('display_errors', true);
	error_reporting(E_ALL);

	if( isset( $_GET['status'] ) )
	{
		$id = (int)getGet('id');
		$sql = 'UPDATE `jogo` SET `status` = '.getGet('status').' WHERE `id` = '.$id;

		echo $sql;//aqui vc deve executar a query
	}
	function getGet( $key ){
		return isset( $_GET[ $key ] ) ? filter( $_GET[ $key ] ) : null;
	}
	function filter( $str ){
		return $str;//deixo a implementação desta por conta de vcs.
	}
</pre>

<a href="http://www.wbruno.com.br/scripts/atualiza-checkbox.php" target="_blank">Demonstração</a>.