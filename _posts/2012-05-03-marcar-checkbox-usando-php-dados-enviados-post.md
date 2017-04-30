---
id: 1971
title: Marcar checkbox usando PHP, com dados enviados via POST
date: 2012-05-03T11:13:06+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1971
permalink: /php/marcar-checkbox-usando-php-dados-enviados-post/
dsq_thread_id:
  - "2100757509"
categories:
  - PHP
---
Para deixar registrado por aqui.

Colocando o atributo checked=&#8221;checked&#8221; em uma lista de checkboxs, dependendo do que foi marcado e enviado via POST.
  
Para usar algum outro array, como um vindo do banco, basta trocar o getPost(&#8216;arr&#8217;), pelo teu array.

<pre name="code" class="php">&lt;?php

$_POST['var'][0] = 'r';
$_POST['var'][1] = 'tx';


function getPost( $key ){
	return isset( $_POST[ $key ] ) ? $_POST[ $key ] : null;
}
function is_checked( $value, $arr ){
	if( in_array( $value, $arr ) ) echo 'checked="checked"';
}
?>
&lt;input type="checkbox" value="r" name="var[]" &lt;?php is_checked( 'r', getPost('var') ); ?>/>Precipitação&lt;br/>
&lt;input type="checkbox" value="tn" name="var[]" &lt;?php is_checked( 'tn', getPost('var') ); ?>/> Temperatura Mínima&lt;br/>
&lt;input type="checkbox" value="tx" name="var[]" &lt;?php is_checked( 'tx', getPost('var') ); ?>/> Temperatura Máxima
</pre>