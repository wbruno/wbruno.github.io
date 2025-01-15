---
id: 1628
title: Trocando o title da página em navegação por query string php
date: 2011-11-25T17:48:47+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1628
permalink: /php/trocando-title-da-pagina-em-navegacao-por-query-string-php/
dsq_thread_id:
  - "2104844864"
categories:
  - PHP
---
Post complementar, deste aqui, em que eu faço um exemplo de [navegação por query string](https://wbruno.com.br/php/navegacao-querystring-php/), com php.

Outra dúvida bem recorrente no fórum.

<!--more-->

É isso ai, não tenho muito oque explicar/<del datetime="2011-11-25T19:47:59+00:00">enrolar</del>. Fiz o código bem simples.

A &#8220;manha&#8221;, para funcionar, é processar toda a requisição, antes de começar a cuspir o html para o browser. Lá em cima, antes até de abrir a tag html e o doctype do documento.

Dessa forma, consigo alterar a tag title, para cada página.

``` php
<?php
  function getGet( $key ){
    return isset( $_GET[ $key ] ) ? $_GET[ $key ] : null;
  }


  $pg = getGet('pg');
  $file = is_file( 'view/'.$pg.'.php' ) ? 'view/'.$pg.'.php' : 'view/home.php';

  switch( $pg )
  {
    case 'contato':
      $title = 'Contato - ';
      break;
    case 'gostei':
      $title = 'Gostei muito disso! - ';
      break;
    default:
      $title = '';
  }

?><html>
<head>
  <title><?php echo $title; ?>Nome Site</title>
</head>
<body>
  <a href="?pg=home">Home</a>
  <a href="?pg=contato">Contato</a>
  <a href="?pg=gostei">Gostei</a>
<?php
  include $file;
?>
</body>
</html>
```

Simples não ?
