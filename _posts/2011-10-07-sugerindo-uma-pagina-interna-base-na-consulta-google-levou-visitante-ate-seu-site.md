---
id: 1466
title: Sugerindo uma página interna com base na consulta do google que levou o visitante até o seu site
date: 2011-10-07T07:00:43+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1466
permalink: /php/sugerindo-uma-pagina-interna-base-na-consulta-google-levou-visitante-ate-seu-site/
categories:
  - PHP
---
Foi uma idéia que tive, dando uma olhada nas palavras chaves que trazem pessoas até a home do meu site/blog.

Nem sempre o meu melhor conteudo para aquela busca está na página que o google entregou ao visitante. Por esse motivo, tive essa idéia de customizar um pedaço da home, respondendo com um conteudo mais adequado àquela pesquisa.

<!--more-->



O único trabalho manual aqui, é cadastrar este array:

``` php
$redirects = Array(
        'marietta' => '/freelas/marietta/',
        'carousel' => '/blog/2011/04/15/carousel-jquery-usando-cycle/'
      );
```

Note que na chave de cada item do array, deixo a **palavra chave** que pode levar o visitante até a minha página, e o valor correspondente é a URL que quero sugerir como mais adequada para aquela busca.

``` php
<?php
  /**
   * @author William Bruno
   * @url http://wbruno.com.br
   * @date 2011-10-05
   */

  if( isset( $_SERVER['HTTP_REFERER'] ) )
  {
    $referer = $_SERVER['HTTP_REFERER'];

    if( stripos( $referer, 'google' ) )
    {
      $url = parse_url( $referer );
      parse_str( $url['query'], $qs );

      $redirects = Array(
        'marietta' => '/freelas/marietta/',
        'dci' => '/freelas/dci/',
      );
      $keys = array_keys( $redirects );

      $search = Array();
      foreach( $keys AS $key ){
        if( stripos( $qs['q'], $key ) )
        {
          $search['key'] =  $key;
          $search['redirect'] =  $redirects[ $key ];
          break;
        }
      }

      if( !empty( $search['redirect'] ) )
        echo '<p>Você estava procurando por: <a href="'.$search['redirect'].'">'.$search['key'].'</a> ?</p>';
    }
  }
```

É isso, qualquer dúvida comentem!
