---
id: 265
title: Selecionar todos checkbox ao clicar em um, e selecionar check ao clicar em linha
date: 2011-03-20T12:45:14+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=265
permalink: /jquery/selecionar-todos-checkb-ao-clicar-em-um-selecionar-check-ao-clicar-em-linha/
dsq_thread_id:
  - "2101234424"
categories:
  - jQuery
tags:
  - framework
---
Boas galera!!

script bem batido e massacrado já, mas com uns adicionais, que nunca vi por ai. Fazer a primeira parte é super simples, e tô cansado de ver gente postando como selecionar grupo de checkbox, ao marcar um. Então, para não fugir do costume, posto algo melhor:

<!--more-->


  
<a href="http://www.wbruno.com.br/scripts/seleciona-todos-checkbox.html" target="_blank">Demostração</a>

<pre name="code" class="html">&lt;html>
&lt;head>
	&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js">&lt;/script>
	&lt;script type="text/javascript">
	$(document).ready(function(){
		/* ao clicar no todos, seleciona todos e altera a class de todas as linhas */
		$("input[name='todos']").click(function(){
			var ckd = $( this ).attr('checked');

			$("#grid input[type='checkbox']").attr({checked: ckd});
			toogle_class( ckd, $('#grid tbody tr') );
		});
		/* ao clicar no checkbox, altera a class da linha */
		$("input[name='status[]']").click(function(){
			toogle_class( $( this ).attr('checked'), $( this ).parents('tr') );
		});
		$("#grid tr").click(function( e ){
			if( e.target.tagName!='INPUT' )
			{
				var checkbox = $( this ).find("input[type='checkbox']");
				var ckd = !checkbox.attr('checked');

				checkbox.attr('checked', ckd);
				toogle_class( ckd, $( this ) );
			}
		});
	});
	function toogle_class( ckd, el ){
		if( ckd==true )
			el.addClass('selecionado');
		else
			el.removeClass('selecionado');
	}
	&lt;/script>
	&lt;style type="text/css">
	.selecionado { background: #f0f; }
	&lt;/style>
&lt;/head>
&lt;body>
	&lt;form action="" method="post">
		&lt;table id="grid">
			&lt;thead>
				&lt;tr>
					&lt;th>ID&lt;/th>
					&lt;th>Nome&lt;/th>
					&lt;th>Status&lt;/th>
				&lt;/tr>
			&lt;/thead>
			&lt;tbody>
				&lt;tr>
					&lt;td>&lt;/td>
					&lt;td>&lt;/td>
					&lt;td>&lt;input type="checkbox" name="todos" value="todos" />&lt;/td>
				&lt;/tr>
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
				&lt;tr>
					&lt;td>18&lt;/td>
					&lt;td>Soul Reaver&lt;/td>
					&lt;td>&lt;input type="checkbox" name="status[]" value="1" />
						&lt;input type="hidden" name="id" value="18" />&lt;/td>
				&lt;/tr>
			&lt;/tbody>
		&lt;/table>
	&lt;/form>
&lt;/body>
&lt;/html>
</pre>