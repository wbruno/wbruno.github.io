---
id: 908
title: Cadastro de conteudo, formulário adiciona dados em tabela temporária
date: 2011-05-10T07:00:02+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=908
permalink: /javascript-puro/cadastro-de-conteudo-formulario-adiciona-dados-em-tabela-temporaria/
dsq_thread_id:
  - "2102672888"
categories:
  - Javascript
---
Salve salve!

Novamente, para termos algo, precisamos da iniciativa de começar.
  
Requisito:

> _&#8220;Um formulário simples, irá adicionando dados numa tabela html temporária, para depois enviar tudo de uma só vez para o banco.&#8221;_

<!--more-->


  
Do começo:

> _&#8220;Um formulário simples, .._

<pre name="code" class="html:firstLine[56]">&lt;form action="" method="post" id="form_prepare">
			&lt;fieldset>
				&lt;label>Nome: &lt;input type="text" name="nome" />&lt;/label>
				&lt;label>Telefone: &lt;input type="text" name="email" />&lt;/label>
				&lt;label>Email: &lt;input type="text" name="telefone" />&lt;/label>

				&lt;label>&lt;input type="submit" name="ok" value="Ok" />&lt;/label>
			&lt;/fieldset>
		&lt;/form>&lt;!-- /form_prepare -->
</pre>

A outra parte:

> _&#8220;&#8230; numa tabela html temporária,&#8230;_

<pre name="code" class="html:firstLine[66]">&lt;table id="grid">
				&lt;thead>
					&lt;tr>
						&lt;th>Nome&lt;/th>
						&lt;th>Telefone&lt;/th>
						&lt;th>Email&lt;/th>
					&lt;/tr>
				&lt;/thead>
				&lt;tbody>
				&lt;/tbody>
			&lt;/table>&lt;!-- /grid -->
</pre>

Importante isso. Começamos do início. Do HTML.

## A parte JavaScript

Agora, segundo nosso briefing, o formulário deve ir adicionando os itens nessa tabela. Aqui que entra, a responsabilidade client-side, afinal, precisamos adicionar os itens nessa tabela temporariamente, sem refresh [ e atenção, pois isso **não significa, e nem quer dizer** ajax. &#8216;Sem refresh&#8217;, [quer dizer client-side, mas não necessariamente precisamos de ajax](http://www.wbruno.com.br/2011/04/08/o-que-e-ajax-e-o-que-nao-e/).

<pre name="code" class="javascript">&lt;script type="text/javascript">
$(document).ready(function(){
	$('#form_prepare').submit(function(){
		var $this = $( this );

		var tr = '&lt;tr>'+
			'&lt;td>'+$this.find("input[name='nome']").val()+'&lt;/td>'+
			'&lt;td>'+$this.find("input[name='email']").val()+'&lt;/td>'+
			'&lt;td>'+$this.find("input[name='telefone']").val()+'&lt;/td>'+
			'&lt;/tr>'
		$('#grid').find('tbody').append( tr );

		return false;
	});
});
&lt;/script>
</pre>

Tranquilo até aqui, certo ?
  
no evento **onSubmit** do meu formulário, disparo essa function javascript, que lê o que está digitado nos inputs deste form, e faz um append lá na minha <table>

Só ficou faltando um pedaço, pois precisamos desses dados &#8216;para depois&#8217;.
  
A minha escolha será adicionar inputs type=&#8221;hidden&#8221;, em um <u>outro formulário</u>, e este sim, será responsável por enviar todos os dados da nossa table temporaria, para o servidor.

<pre name="code" class="html:firstLine[75]">&lt;form action="" method="post" id="form_insert">
			&lt;fieldset style="display: none;">&lt;/fieldset>
			&lt;label>&lt;input type="submit" name="cadastrar" value="Cadastrar" />&lt;/label>
		&lt;/form><!-- /form_insert -->
</pre>

O JS desse trecho:

<pre name="code" class="html:firstLine[36]">var hiddens = '&lt;input type="hidden" name="nome[]" value="'+nome+'" />'+
			'&lt;input type="hidden" name="email[]" value="'+email+'" />'+
			'&lt;input type="hidden" name="telefone[]" value="'+telefone+'" />';

		$('#form_insert').find('fieldset').append( hiddens );
</pre>

Prosseguindo..

## A parte PHP

Necessário nesse trecho, entendermos que trabalhar com array, simplifica todo o processo.

<pre name="code" class="php">&lt;?php
	if( $_SERVER['REQUEST_METHOD']=='POST' )
	{
		$sql = "INSERT INTO cliente ( id, nome, email, telefone ) VALUES ";

		$values = Array();
		for( $i=0; $i&lt;count( $_POST['nome'] ); $i++ )
		{
			$values[] = "(NULL, '".filter( $_POST['nome'][$i] )."',
					'".filter( $_POST['email'][$i] )."',
					'".filter( $_POST['telefone'][$i] )."')";
		}
		echo $sql.implode( ',', $values );
	}
function filter( $str ){
	return addslashes( $str );//deixo demais filtros e validações por sua conta
}
?>
</pre>

Os inputs hidden que serão adicionados, são do tipo:

<pre name="code" class="html:firstLine[37]">&lt;input type="hidden" name="email[]" value="valor" /></pre>

Logo, receberemos um **array**: $\_POST\[&#8216;email&#8217;], com as posições: $\_POST[&#8216;email&#8217;\]\[0\], $_POST\[&#8216;email&#8217;\]\[1\]&#8230;

O código completo, então:

<pre name="code" class="html">&lt;?php
	if( $_SERVER['REQUEST_METHOD']=='POST' )
	{
		$sql = "INSERT INTO cliente ( id, nome, email, telefone ) VALUES ";

		$values = Array();
		for( $i=0; $i&lt;count( $_POST['nome'] ); $i++ )
		{
			$values[] = "(NULL, '".filter( $_POST['nome'][$i] )."',
					'".filter( $_POST['email'][$i] )."',
					'".filter( $_POST['telefone'][$i] )."')";
		}
		echo $sql.implode( ',', $values );
	}
function filter( $str ){
	return addslashes( $str );//deixo demais filtros e validações por sua conta
}
?>
&lt;html>
&lt;head>
&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
$(document).ready(function(){
	$('#form_prepare').submit(function(){
		var $this = $( this );

		var nome = $this.find("input[name='nome']").val(),
			email = $this.find("input[name='email']").val(),
			telefone = $this.find("input[name='telefone']").val();

		var tr = '&lt;tr>'+
			'&lt;td>'+nome+'&lt;/td>'+
			'&lt;td>'+email+'&lt;/td>'+
			'&lt;td>'+telefone+'&lt;/td>'+
			'&lt;/tr>'
		$('#grid').find('tbody').append( tr );

		var hiddens = '&lt;input type="hidden" name="nome[]" value="'+nome+'" />'+
			'&lt;input type="hidden" name="email[]" value="'+email+'" />'+
			'&lt;input type="hidden" name="telefone[]" value="'+telefone+'" />';

		$('#form_insert').find('fieldset').append( hiddens );

		return false;
	});
});
&lt;/script>
&lt;style type="text/css">
#main {
	width: 700px; margin: 0 auto;
}
&lt;/style>
&lt;/head>
&lt;body>
	&lt;div id="main">
		&lt;form action="" method="post" id="form_prepare">
			&lt;fieldset>
				&lt;label>Nome: &lt;input type="text" name="nome" />&lt;/label>
				&lt;label>Telefone: &lt;input type="text" name="email" />&lt;/label>
				&lt;label>Email: &lt;input type="text" name="telefone" />&lt;/label>

				&lt;label>&lt;input type="submit" name="ok" value="Ok" />&lt;/label>
			&lt;/fieldset>
		&lt;/form>&lt;!-- /form_prepare -->

		&lt;table id="grid">
			&lt;thead>
				&lt;tr>
					&lt;th>Nome&lt;/th>
					&lt;th>Telefone&lt;/th>
					&lt;th>Email&lt;/th>
				&lt;/tr>
			&lt;/thead>
			&lt;tbody>
			&lt;/tbody>
		&lt;/table>&lt;!-- /grid -->
		&lt;form action="" method="post" id="form_insert">
			&lt;fieldset style="display: none;">&lt;/fieldset>
			&lt;label>&lt;input type="submit" name="cadastrar" value="Cadastrar" />&lt;/label>
		&lt;/form>&lt;!-- /form_insert -->
	&lt;/div>&lt;!-- /main -->
&lt;/body>
&lt;/html>
</pre>

Saída que obtive:

<pre name="code" class="sql">INSERT INTO cliente ( id, nome, email, telefone ) VALUES (NULL, 'William', '(21) 1234-4567','email@teste.com.br'),(NULL, 'Bruno', '(21) 1234-1234','email@teste.com') </pre>

### <a href="http://www.wbruno.com.br/scripts/cadastro-formulario-table.php" target="_blank">Demonstração Online</a>

É isso =)