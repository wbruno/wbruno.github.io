---
id: 111
title: Criar input no onblur, e receber dados array php
date: 2011-02-04T23:28:32+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=111
permalink: /jquery/criar-input-no-onblur-e-receber-dados-array-php/
dsq_thread_id:
  - "2101432454"
categories:
  - jQuery
---
Demonstração prática do método .live() do jQuery e trabalhando com arrays no php

<pre name="code" class="html">&lt;?php
	if( $_SERVER['REQUEST_METHOD']=='POST' )
	{
		$values = Array();
		foreach( $_POST['conta'] AS $conta )
		{
			if( !empty( $conta ) )
				$values[] = "(NULL, '{$conta}')";
		}
		$sql = "INSERT INTO `table` ( `id`, `conta` ) VALUES ".implode( ', ', $values );
		echo $sql;
	}
?&gt;
&lt;html&gt;
	&lt;head&gt;
		&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js">&lt;/script>
		&lt;script type="text/javascript"&gt;
			$(document).ready(function(){
				var i = 1;
				$('#campos input').live('blur', function(){
					if( $( this ).val()!='' && $('#campos input:last').val()!='' )
					{
					if( i&lt;10 )//limitar em 10 campos
					{
						i++
						$('#campos').append( '&lt;label&gt;Conta '+i+':&lt;input type="text" name="conta[]" value="" id="'+i+'" /&gt;&lt;/label&gt;' )
							.find('input:last').focus();
						}
					}
				});
			});
		&lt;/script&gt;
	&lt;/head&gt;
	&lt;body&gt;
		&lt;form action="" method="post"&gt;
			&lt;fieldset id="campos"&gt;
				&lt;label&gt;Conta 1:&lt;input type="text" name="conta[]" /&gt;&lt;/label&gt;

			&lt;/fieldset&gt;&lt;!-- /campos --&gt;
			&lt;label&gt;&lt;input type="submit" name="ok" value="ok" /&gt;&lt;/label&gt;
		&lt;/form&gt;
	&lt;/body&gt;
&lt;/html&gt;
</pre>