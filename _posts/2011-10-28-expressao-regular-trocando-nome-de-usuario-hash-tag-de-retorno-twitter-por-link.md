---
id: 1588
title: Expressão Regular, trocando nome de usuário e hash tag de retorno do Twitter, por link
date: 2011-10-28T19:45:36+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1588
permalink: /php/expressao-regular-trocando-nome-de-usuario-hash-tag-de-retorno-twitter-por-link/
categories:
  - PHP
tags:
  - twitter
---
É.. o título ficou bem extenso..

mas não tinha como resumir. Somente isso, eu já tinha mostrado <a href="http://wbruno.com.br/2011/05/29/buscando-uma-hash-tag-search-twitter/" target="_blank">como buscar uma hashtag no twitter usando php</a>, agora, apenas para ficar registrado, 2 ERs aqui, para colocar link nos usuários e nas hashtags retornadas.

<!--more-->



As ERs são bem simples:

``` php
Array(
            '/@([\w]+)/',
            '/(#[\w]+)/'
          ),
```

Então, lá vai o source completo:

``` php
<?php
    header('Content-type: text/html; charset=utf-8');

    $hash = '%23locaweb';//apenas para ficar claro oque é

  $search = 'http://search.twitter.com/search.json?q='.$hash.'&rpp=10';
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

  $json = curl_file( $search );
  $data = json_decode( $json );

    $li = '<ul>'.PHP_EOL;
    foreach( $data->results AS $post ){
        $li .= "\t".'<li><img src="'.$post->profile_image_url.'" alt="'.$post->from_user.'" title="'.$post->from_user.'" /> ';


        $li .= preg_replace(
          Array(
            '/@([\w]+)/',
            '/(#[\w]+)/'
          ),
          Array(
            '<a href="http://twitter.com/#!/$1" title="$1">@$1</a>',
            '<a href="http://twitter.com/#!/search/$1" title="$1">$1</a>'
          ),
          $post->text
        );


        $li .= '</li>'.PHP_EOL;
    }
    echo $li,'</ul>';
```

é isso ai.

Se vc usar, ou ler este post, não deixe de comentar! Me ajuda a produzir mais conteúdos relevantes e interessantes.

**E aproveitando a deixa do Twitter, me siga!** <a href="http://twitter.com/#!/tiu_uiLL" target="_blank">@tiu_uiLL</a>

## <a href="http://www.wbruno.com.br/scripts/search_hash_twitter_com_links.php" target="_blank">Demonstração Online</a>

é isso ai, vlw!
