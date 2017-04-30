---
id: 1152
title: Timeline Twitter com php
date: 2011-07-07T23:25:36+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1152
permalink: /php/timeline-twitter-php/
dsq_thread_id:
  - ""
categories:
  - PHP
tags:
  - twitter
---
Opa! post rápido.. apenas para registrar por aqui, uma forma de recuperar a timeline de algum usuário do Twitter. Mas dessa vez, sem usar funções como: file\_get\_contents(), fopen(), simplexml\_load\_file().. pois essas precisam de uma configuração que geralmente vem desativada em servidores compartilhados.

**Warning:** file\_get\_contents() [function.file-get-contents]: URL file-access is disabled in the server configuration in **/home/storage/blablablabla.php** on line **n**

<!--more-->

Logo, vamos usar cURL:

<pre name="code" class="php">&lt;?php
	function curl_file($url, $timeout=0){
		$ch = curl_init();
		curl_setopt( $ch, CURLOPT_URL, $url );
		//curl_setopt ($ch, CURLOPT_HEADER, 1);
		curl_setopt( $ch, CURLOPT_RETURNTRANSFER, 1 );
		curl_setopt( $ch, CURLOPT_CONNECTTIMEOUT, $timeout );
		$content = curl_exec( $ch );
		curl_close( $ch );

		return $content;
	}
	$url = 'http://twitter.com/statuses/user_timeline/tiu_uiLL.rss?count=1';
	$xml = new SimpleXMLElement( curl_file( $url ) );
	
	$item = $xml->channel->item;
	var_dump( $item );
?></pre>

=) é isso ai.