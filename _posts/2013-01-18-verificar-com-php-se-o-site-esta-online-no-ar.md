---
id: 2893
title: Verificar com php se o site está online (no ar)
date: 2013-01-18T11:59:14+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2893
permalink: /php/verificar-com-php-se-o-site-esta-online-no-ar/
dsq_thread_id:
  - "2102655931"
categories:
  - PHP
---
Vi dois caras no fórum perguntando sobre isso, então resolvi fazer um post.

Um simples código com a lib cURL do php, para verificar se um site está ou não no ar.

``` php
<?php

  function curl_info($url){
    $ch = curl_init();
    curl_setopt( $ch, CURLOPT_URL, $url );
    curl_setopt( $ch, CURLOPT_HEADER, 1);
    curl_setopt( $ch, CURLOPT_RETURNTRANSFER, 1 );
    curl_setopt( $ch, CURLOPT_CONNECTTIMEOUT, $timeout );
    curl_setopt( $ch, CURLOPT_FOLLOWLOCATION, 1 );
        
    $content = curl_exec( $ch );
    $info = curl_getinfo( $ch );

    return $info;
  }

  $site = 'http://www.locaweb.com.br';
  $info = curl_info( $site );
  if( $info['http_code']==200 ) {
    echo '<u>'.$site . '</u> - <strong>está no ar!!</strong><br />';
  } else {
    echo '<u>'.$site . '</u> - está fora do ar<br />';
  }


  $site = 'http://www.locaweba.com.br';
  $info = curl_info( $site );
  if( $info['http_code']==200 ) {
    echo '<u>'.$site . '</u> - <strong>está no ar!!</strong><br />';
  } else {
    echo '<u>'.$site . '</u> - está fora do ar<br />';
  }

```

Capturo os cabeçalhos da requisição e verifico se o http_status é igual a 200.
  
Caso seja, significa que o site está sim no ar.

Note que deixei a entrada:
  
`curl_setopt( $ch, CURLOPT_FOLLOWLOCATION, 1 );`
  
para caso o site possua algum redirecionamento, como é o caso da locaweb, que redireciona a home para o /default.html

É isso galera, comentem caso usem. =)