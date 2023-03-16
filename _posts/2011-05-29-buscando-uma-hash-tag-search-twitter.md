---
id: 1060
title: Buscando uma hash tag no search do Twitter
date: 2011-05-29T07:00:56+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1060
permalink: /php/buscando-uma-hash-tag-search-twitter/
dsq_thread_id:
  - "2102952726"
categories:
  - PHP
tags:
  - twitter
---
Não tem muito oque explicar.

vou fazer um search no Twitter, procurando por determinada hash tag **#wbruno**, e então devolver um HTML simples para inserirmos no nosso site.

<!--more-->



Usei aqui, algumas funções nativas do php, como **file\_get\_contents()**, **var_dump()**, e **json_decode()**.

O link para mais esclarecimentos do search é: <a href="http://dev.twitter.com/doc/get/search" target="_blank">http://dev.twitter.com/doc/get/search</a>

``` php
<?php
  header('Content-type: text/html; charset=utf-8');


  $hash = '%23wbruno';//apenas para ficar claro oque é
  $search = 'http://search.twitter.com/search.json?q='.$hash.'&rpp=10';

  $json = file_get_contents( $search );
  /*
    "{"results":[
      {
        "from_user_id_str":"18765280",
        "profile_image_url":"http://a3.twimg.com/profile_images/1318748377/0863ff06d8563514ab26e03e0fad1fa6_normal.jpg",
      ...
  */
  $data = json_decode( $json );
  /*
  object(stdClass)#1 (10) {
    ["results"]=>
    array(6) {
    [0]=>
    object(stdClass)#2 (14) {
      ["from_user_id_str"]=>
      string(8) "18765280"
      ["profile_image_url"]=>
      string(89) "http://a3.twimg.com/profile_images/1318748377/0863ff06d8563514ab26e03e0fad1fa6_normal.jpg"
      ["created_at"]=>
      string(31) "Sat, 28 May 2011 13:35:21 +0000"
      ["from_user"]=>
      string(8) "tiu_uiLL"
      ["id_str"]=>
      string(17) "74468805430087680"
      ["metadata"]=>
      object(stdClass)#3 (1) {
      ["result_type"]=>
      string(6) "recent"
      }
      ["to_user_id"]=>
      NULL
      ["text"]=>
      string(113) "Novo Post: FormulÃ¡rio de busca com filtro dinÃ¢mico em MySQL e php http://www.wbruno.com.br/?p=1058 #wbruno"
      ["id"]=>
      float(7.4468805430088E+16)
      ["from_user_id"]=>
      int(18765280)
      ["geo"]=>
      NULL
      ["iso_language_code"]=>
      string(2) "pt"
      ["to_user_id_str"]=>
      NULL
      ["source"]=>
      string(97) "<a href="http://www.wbruno.com.br" rel="nofollow">wbruno</a>"
    }
  */


  $li = '<ul>'.PHP_EOL;
  foreach( $data->results AS $post ){
    $li .= "\t".'<li><img src="'.$post->profile_image_url.'" alt="'.$post->from_user.'" title="'.$post->from_user.'" />
      '.$post->text.'</li>'.PHP_EOL;
  }
  echo $li,'</ul>';

```

com isso, a minha saída no instante em que rodei, foi:

``` html
<ul>
  <li><img src="http://a3.twimg.com/profile_images/1318748377/0863ff06d8563514ab26e03e0fad1fa6_normal.jpg" alt="tiu_uiLL" title="tiu_uiLL" />
      Novo Post: Formulário de busca com filtro dinâmico em MySQL e php http://www.wbruno.com.br/?p=1058 #wbruno</li>
  <li><img src="http://a3.twimg.com/profile_images/1318748377/0863ff06d8563514ab26e03e0fad1fa6_normal.jpg" alt="tiu_uiLL" title="tiu_uiLL" />
      Acessar função de um iframe, apatir do documento pai http://t.co/MqrYpuf #wbruno</li>
  <li><img src="http://a3.twimg.com/profile_images/1318748377/0863ff06d8563514ab26e03e0fad1fa6_normal.jpg" alt="tiu_uiLL" title="tiu_uiLL" />
      Post Editado: Criando um plugin jQuery - parte 3 - Otimizando http://www.wbruno.com.br/?p=343 #wbruno</li>
  <li><img src="http://a3.twimg.com/profile_images/1318748377/0863ff06d8563514ab26e03e0fad1fa6_normal.jpg" alt="tiu_uiLL" title="tiu_uiLL" />

      Novo Post: Navegação sem refresh – carregando conteúdo com ajax em div 2 http://www.wbruno.com.br/?p=1038 #wbruno</li>
  <li><img src="http://a3.twimg.com/profile_images/1318748377/0863ff06d8563514ab26e03e0fad1fa6_normal.jpg" alt="tiu_uiLL" title="tiu_uiLL" />
      Novo Post: Validando inputs com Expressão Regular com jQuery http://www.wbruno.com.br/?p=1034 #wbruno</li>
  <li><img src="http://a3.twimg.com/profile_images/1318748377/0863ff06d8563514ab26e03e0fad1fa6_normal.jpg" alt="tiu_uiLL" title="tiu_uiLL" />
      Novo Post: Só carregar scripts js, se houver suporte a js http://www.wbruno.com.br/?p=1031 #wbruno</li>
</ul>
```

## <a href="http://wbruno.com.br/scripts/search_hash_twitter.php" target="_blank">Demonstração Online</a>

Deixei um parâmetro, caso vc queria fazer um teste:

<a href="http://wbruno.com.br/scripts/search_hash_twitter.php?hash=locaweb" target="_blank">http://wbruno.com.br/scripts/search_hash_twitter.php?hash=locaweb</a>

## Versão com cURL

``` php
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
```
