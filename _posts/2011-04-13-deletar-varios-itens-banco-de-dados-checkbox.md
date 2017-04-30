---
id: 742
title: Deletar vários itens do banco de dados, com checkbox
date: 2011-04-13T13:00:25+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=742
permalink: /php/deletar-varios-itens-banco-de-dados-checkbox/
dsq_thread_id:
  - "2100810985"
categories:
  - PHP
---
Dúvida recorrente no fórum.

Funcionamento parecido com os webmails.
  
Você possui uma lista de registros. Em cada um desses registros, há um checkbox.

Deseja-se, [selecionar vários checkboxs](http://www.wbruno.com.br/2011/03/20/selecionar-todos-checkb-ao-clicar-em-um-selecionar-check-ao-clicar-em-linha/), e então com um só botão, proceder com a exclusão de todos os itens selecionados.
  
<!--more-->

<pre name="code" class="php">&lt;?php
	if( $_SERVER['REQUEST_METHOD']=='POST' ){
		$arr = filter( $_POST['excluir'] );

		$sql = 'DELETE FROM registro WHERE id IN('.implode( ',', $arr ).')';
		echo $sql;
	}
	function filter( $dados ){
		$arr = Array();
		foreach( $dados AS $dado ) $arr[] = (int)$dado;
		return $arr;
	}
?>


&lt;form action="" method="post">
	&lt;table>
		&lt;tr>
			&lt;td>&lt;input type="checkbox" name="excluir[]" value="13" />&lt;/td>
			&lt;td>Registro 13&lt;/td>
		&lt;/tr>
		&lt;tr>
			&lt;td>&lt;input type="checkbox" name="excluir[]" value="9" />&lt;/td>
			&lt;td>Registro 9&lt;/td>
		&lt;/tr>
		&lt;tr>
			&lt;td>&lt;input type="checkbox" name="excluir[]" value="26" />&lt;/td>
			&lt;td>Registro 26&lt;/td>
		&lt;/tr>
		&lt;tr>
			&lt;td>&lt;input type="checkbox" name="excluir[]" value="14" />&lt;/td>
			&lt;td>Registro 14&lt;/td>
		&lt;/tr>
	&lt;/table>
	&lt;input type="submit" name="submit" value="Excluir Selecionados" />
&lt;/form>
</pre>

Bom, é isso. Simples, prático e direto.

@2011-04-18 Adicionei a função **filter()**, para fazer o casting de tipo, antes de mandar para a string SQL. Dessa forma evitamos o injection mencionado pelos nossos colegas nos comentários deste post.