---
id: 3002
title: Importar emails dos comentários do WordPress para CSV
date: 2013-05-30T07:00:37+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3002
permalink: /wordpress/importar-emails-dos-comentarios-do-wordpress-para-csv/
categories:
  - WordPress
---
<img src="http://wbruno.com.br/wp-content/uploads/2013/05/wp.png" alt="wp" width="504" height="279" class="aligncenter size-full wp-image-3003" srcset="http://wbruno.com.br/wp-content/uploads/2013/05/wp.png 504w, http://wbruno.com.br/wp-content/uploads/2013/05/wp-300x166.png 300w" sizes="(max-width: 504px) 100vw, 504px" />
  
<!--more-->

Depois de [capturar a lista dos emails de quem comentou no teu wordpress](http://wbruno.com.br/wordpress/capturar-lista-de-email-dos-comentarios-seu-wordpress-outras-queries-uteis/), chega a hora de disparar um email para essa gente toda.

Como o meu servidor é compartilhado, a sintaxe para <a href="http://fiorix.wordpress.com/2008/04/17/importando-e-exportando-csv-no-mysql/" rel="nofollow">importar csv direto no sql</a>, não funcionou. Pois o meu usuário do banco não tem acesso a esse tipo de operação.

Caso o seu tenha, use o comando abaixo:

## Direto no SQL

<pre class="sql">SELECT comment_author_email, comment_author
FROM  `wp_comments` 
WHERE comment_author_email &lt;>  ''
GROUP BY comment_author_email
ORDER BY (
comment_author_email )
INTO OUTFILE '/tmp/meuarquivo.csv'
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\n';
</pre>

E se quiser apenas os comentários após uma certa data:

<pre>SELECT comment_author_email, comment_author FROM  `wp_comments`  WHERE comment_author_email &lt;>  '' AND comment_date > '2013-04-13' GROUP BY comment_author_email ORDER BY ( comment_author_email ) INTO OUTFILE '/tmp/comments-2013-04-13.csv' FIELDS TERMINATED BY ';' LINES TERMINATED BY '\n';</pre>

No meu caso, eu tive que conectar no banco e gerar o .csv com programação server-side.

## Usando PHP

<pre class="php">&lt;?php

$db = new mysqli('host', 'user', 'pass', 'bd');

$sql = "SELECT comment_author_email, comment_author
	FROM  `wp_comments` 
	WHERE comment_author_email &lt;>  ''
	GROUP BY comment_author_email
	ORDER BY (
		comment_author_email
	)";

$query = $db->query( $sql );
while( $dados = $query->fetch_object() ){
	$arr[] = "\"{$dados->comment_author}\", \"{$dados->comment_author_email}\"";
}

echo implode($arr, "\n");
</pre>

Prontinho! feito. Dai foi só disparar um email para todo mundo, logicamente com o link de remover.
  
Se você frequenta meu blog, ou já comentou por aqui, provavelmente você recebeu também.