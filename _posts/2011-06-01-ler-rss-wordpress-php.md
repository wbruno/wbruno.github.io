---
id: 1062
title: Ler rss do WordPress com php
date: 2011-06-01T07:00:23+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1062
permalink: /wordpress/ler-rss-wordpress-php/
categories:
  - WordPress
tags:
  - xml
---
Vou usar a lib **simplexml\_load\_file()**, para resgatar o RSS da categoria php do meu blog WordPress.

Para ler o conteudo dentro de CDATA(conteudo do post, categorias&#8230;), preciso passar um parâmetro adicional para a classe **LIBXML_NOCDATA**
  
<a href="http://br.php.net/manual/en/libxml.constants.php" target="_blank">http://br.php.net/manual/en/libxml.constants.php</a>

<!--more-->

``` php
<?php

  $rss = 'http://www.wbruno.com.br/category/php/feed/';

  $xml = simplexml_load_file( $rss, 'SimpleXMLElement', LIBXML_NOCDATA );

  $li = '<ul>'.PHP_EOL;
  $i = 0;
  foreach( $xml->channel->item AS $item )
  {
    if( $i==7 ) break; //limitando a 7 posts

    $li .= "\t".'<li><h3><a href="'.$item->link.'">'.$item->title.'</a></h3>
      <p>'.substr( strip_tags( $item->description ), 5, 100 ).'...</p></li>'.PHP_EOL;
    $i++;
  }
  /*
    object(SimpleXMLElement)#3 (7) {
      ["title"]=>
      string(56) "Formulário de busca com filtro dinâmico em MySQL e php"
      ["link"]=>
      string(90) "http://www.wbruno.com.br/2011/05/28/formulario-de-busca-filtro-dinamico-em-mysql-php/"
      ["comments"]=>
      string(99) "http://www.wbruno.com.br/2011/05/28/formulario-de-busca-filtro-dinamico-em-mysql-php/#comments"
      ["pubDate"]=>
      string(31) "Sat, 28 May 2011 13:35:20 +0000"
      ["category"]=>
      array(3) {
      [0]=>
      object(SimpleXMLElement)#5 (0) {
      }
      [1]=>
      object(SimpleXMLElement)#6 (0) {
      }
      [2]=>
      object(SimpleXMLElement)#7 (0) {
      }
      }
      ["guid"]=>
      string(37) "http://www.wbruno.com.br/?p=1058"
      ["description"]=>
      object(SimpleXMLElement)#8 (0) {
      }
    }
  */

  echo $li,'</ul>';
```