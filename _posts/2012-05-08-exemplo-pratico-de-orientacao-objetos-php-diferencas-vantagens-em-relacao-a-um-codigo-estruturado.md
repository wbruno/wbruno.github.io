---
id: 1974
title: Exemplo prático de Orientação a Objetos (php), diferenças e vantagens em relação à um código Estruturado
date: 2012-05-08T11:25:50+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1974
permalink: /php/exemplo-pratico-de-orientacao-objetos-php-diferencas-vantagens-em-relacao-a-um-codigo-estruturado/
dsq_thread_id:
  - "2100720553"
categories:
  - PHP
tags:
  - oo
---
#SouDev, focado em #FrontEnd &#8220;atualmente&#8221;.

Já trabalhei com backend também, desde a modelagem das Entidades, até as interfaces e controllers com ajax.

Uma das minhas maiores dificuldades enquanto estava estudando sobre **Orientação a Objetos**, era entender de fato o que é _um objeto_.

E o que a palavra _orientação_ tem a ver com eles. [Afinal, o que é Orientação a Objetos?](https://wbruno.com.br/opiniao/afinal-e-orientacao-objetos/ "Afinal, o que é Orientação a Objetos?")

<!--more-->



Não basta sair criando classes, instanciando coisas, ou colocando todo o nosso código estruturado dentro de métodos <var>public function foo()</var>!

Isso não é Orientação a Objetos.

Precisamos ter em mente <a href="https://wbruno.com.br/php/boas-praticas-de-programacao-filosofias-de-desenvolvimento/" target="_blank">diversos conceitos de programação</a>, e entender que a granulidade de nossos objetos(SRP), nos guiará a um código melhor, enxuto e menos custoso.

## Exemplo Prático

Precisei recentemente, ler diversos feeds de redes sociais, e mostrar os 4~5~7 últimas atividades da timeline/posts/vídeos/fotos&#8230;

Eu já tinha cada código isolado mais ou menos pronto:

-> <a href="https://wbruno.com.br/wordpress/ler-rss-wordpress-php/" target="_blank">Ler rss do WordPress com php</a>

-> <a href="https://wbruno.com.br/php/timeline-twitter-php/" target="_blank">Timeline Twitter com php</a>

..

Ainda precisava ler do Flickr, do Facebook, e do Youtube.

Simplesmente, pegar cada rotina dessa e jogar na aplicação, me levaria a ter um código macarrônico/redundante:

[<img src="/wp-content/uploads/2012/05/LeitorRss2-571x1024.jpg" alt="" title="LeitorRss2" width="571" height="1024" class="aligncenter size-large wp-image-1980" srcset="/wp-content/uploads/2012/05/LeitorRss2-571x1024.jpg 571w, /wp-content/uploads/2012/05/LeitorRss2-167x300.jpg 167w, /wp-content/uploads/2012/05/LeitorRss2.jpg 1009w" sizes="(max-width: 571px) 100vw, 571px" />](/wp-content/uploads/2012/05/LeitorRss2.jpg)

Ok, a classe acima &#8220;faz&#8221; oque eu precisava, mas está incorreta. De uma forma visual e bem simples, note as áreas que circulei.

Uma &#8220;god class&#8221;, precisa ser urgentemente refatorada!

E ainda faltam o Facebook, o Flickr, o Youtube&#8230;

## Refatorando

As repetições e inconsistências estão concentradas no loop que itera o objeto, e nas rotinas de testar se já existe ou criar um novo arquivo de cache.

``` php
<?php

/**
 * @file View.class.php
 * @date 2012-05-04
 * @author William Moraes
 */
class View
{


  public function draw( iSource $source, $limit=5 )
  {
    $data = $source->getData();

    $i = 0;
    $html = '';
    foreach( $data AS $item ){
      if( $i==$limit ) break;


      if( $source->criteria( $item ) ){
        $html .= $source->html( $item );
        $i++;
      }
    }
    return $html;
  }

}//View
```

E o cache, que também não deveria ser responsabilidade de cada &#8220;método&#8221; twitter(), wordpress()..

``` php
<?php

/**
 * @file Cache.class.php
 * @date 2012-05-04
 * @author William Moraes
 */
class Cache
{
  private $path = '../cache/';
  private $view;

  public function setPath( $path )
  {
    $this->path = $path;
  }

  public function __construct( iSource $source, View $view )
  {
    $this->source = $source;
    $this->view = $view;
  }

  public function isCached( $url, $file, $limit=5 )
  {
    $this->source->setURL( $url );
    $cached_file = $this->path.$file;


    if( is_file( $cached_file ) )
      return file_get_contents( $cached_file );

    $contents = $this->view->draw( $this->source, $limit );

    file_put_contents( $cached_file, trim( $contents ) );
    return $contents;
  }


}//Cache
```

Note que para &#8220;dar certo&#8221; e fazer sentido, eu criei um contrato: <a href="https://wbruno.com.br/php/afinal-e-interface-oop/" target="_blank">A interface</a> iSource:

``` php
<?php

/**
 * @file iSource.class.php
 * @date 2012-05-04
 * @author William Moraes
 */
interface iSource
{
  public function setURL( $url );
  public function html( $data );

  public function getData();
  public function criteria( $item );
}
```

E então agora, cada &#8220;objeto&#8221;, afinal Twitter é uma coisa, Facebook é uma outra, e Flickr é outra ainda completamente diferente. Logo, **objetos** diferentes, podem implementar esse contrato, e garantir compatibilidade com as classes Cache e View.

## Timeline do Twitter

``` php
<?php

include_once 'iSource.class.php';
/**
 * @file Twitter.class.php
 * @date 2012-05-04
 * @author William Moraes
 * @usage

  $twitter = new Twitter( $reader );
  $twitter->setURL( 'http://twitter.com/statuses/user_timeline/locaweb.json?count=5' );
  echo $view->draw( $twitter );

 */
class Twitter implements iSource
{

  private $reader;
  private $url;

  public function __construct( Reader $reader )
  {
    $this->reader = $reader;
  }

  public function setURL( $url )
  {
    $this->url = $url;
  }


  /**
   * @function html
   */
  public function html( $item )
  {
    $html = "\t".'<li><img src="'.$item->user->profile_image_url.'" alt="'.$item->user->screen_name.'" title="'.$item->user->screen_name.'" /> ';

    $html .= $this->makeLinks( $item->text );
    $html .= '</li>'.PHP_EOL;


    return $html;
  }


  /**
   * @function getData
   */
  public function getData()
  {
    return $this->reader->getJSON( $this->url );
  }


  /**
   * @function criteria
   */
  public function criteria( $item )
  {
    return true;
  }


  /**
   * @function makeLinks
   */
  private function makeLinks( $text )
  {
    return preg_replace(
      Array(
        '/(http:\/\/[\w\.\/]+)/',
        '/[^\w]@([\w]+)/',
        '/(#[\w]+)/'
      ),
      Array(
        '<a href="$1" title="$1" rel="external">$1</a>',
        '<a href="http://twitter.com/#!/$1" title="$1" rel="external">@$1</a>',
        '<a href="http://twitter.com/#!/search/$1" title="$1" rel="external">$1</a>'
      ),
      $text
    );
  }


}//Twitter
```

Note a simplicidade do método Twitter:html();

Diferente do método LeitorRss:twitter(), agora só oque &#8220;realmente&#8221; interessa está ali. Afinal, oque mudava entre: LeitorRss:twitter() e LeitorRss:wordpress(), era a forma com que eu montava cada LI, e não o loop em si.

## Timeline do Facebook

É simples também agora, plugar a class Facebook para ler a timeline:

``` php
<?php

include_once 'iSource.class.php';
/**
 * @file Facebook.class.php
 * @date 2012-05-04
 * @author William Moraes
 * @usage

   $facebook = new Facebook( $reader );
  $facebook->setURL( 'https://graph.facebook.com/locaweb/posts&access_token=SEU_ACCESS_TOKEN&method=get' );
  echo $view->draw( $facebook );

 */
class Facebook implements iSource
{

  private $reader;
  private $url;

  public function __construct( Reader $reader )
  {
    $this->reader = $reader;
  }

  public function setURL( $url )
  {
    $this->url = $url;
  }


  /**
   * @function html
   */
  public function html( $item )
  {

    $ts = strtotime( $item->created_time );
    $date = date( 'd/m/Y à\s H:m', $ts );
    $pieces = explode('_', $item->id );



    return '<li>'.substr( $item->message, 0, 140 ).'..
      postado dia <a href="https://www.facebook.com/locaweb/posts/'.$pieces[1].'" rel="external">'.$date.'</a></li>';
  }


  /**
   * @function getData
   */
  public function getData()
  {
    $data = $this->reader->getJSON( $this->url );
    return $data->data;
  }


  /**
   * @function criteria
   */
  public function criteria( $item )
  {
    return isset( $item->message );
  }

}//Facebook
```

Usando:

``` php
<?php
  header ('Content-type: text/html; charset=utf-8');

  date_default_timezone_set('America/Sao_Paulo');

  include 'class/Reader.class.php';

  include 'class/Twitter.class.php';
  include 'class/Facebook.class.php';
  include 'class/Wordpress.class.php';
  include 'class/Statusblog.class.php';
  include 'class/Flickr.class.php';
  include 'class/View.class.php';
  include 'class/Cache.class.php';


  $reader = new Reader();
  $view = new View();


  $twitter = new Twitter( $reader );
  $cache = new Cache( $twitter, $view );
  echo $cache->isCached( 'http://twitter.com/statuses/user_timeline/locaweb.json?count=10', 'twitter-timeline.txt' );


  $facebook = new Facebook( $reader );
  $cache = new Cache( $facebook, $view );
  echo $cache->isCached( 'https://graph.facebook.com/locaweb/posts&access_token=XXX&method=get', 'facebook-timeline.txt' );


  $wordpress = new WordPress( $reader );
  $cache = new Cache( $wordpress, $view );
  echo $cache->isCached( 'http://feeds.feedburner.com/bloglocaweb', 'rss_blog.txt' );


  /* cache status blog */
  $statusblog = new Statusblog( $reader );
  $cache = new Cache( $statusblog, $view );
  echo $cache->isCached( 'http://statusblog.locaweb.com.br/feed', 'rss_statusblog.txt', 7 );
```

E enfim, o último participante:

### Class Reader

Eu não vi sentido em colocar o cURL, o json\_decode(), o file\_get_contents()&#8230; dentro de cada uma das classes que representam as Mídias Sociais.

Por esse motivo, criei um outro objeto, especializado em &#8220;ler&#8221;, seja da forma que for, e retornar dados em forma de StandardClass.

``` php
<?php

/**
 * @file Reader.class.php
 * @date 2012-05-04
 * @author William Moraes
 */
class Reader
{


  public function getXML( $url )
  {
    $file = $this->curlFile( $url );
    return simplexml_load_string( $file, 'SimpleXMLElement', LIBXML_NOCDATA );
  }
  public function getJSON( $url )
  {
    $result = $this->curlFile( $url );
    return json_decode( $result );
  }

  private function getContents( $url )
  {
    return file_get_contents( $url );
  }

  private function curlFile($url, $timeout=0)
  {
    $ch = curl_init();
    curl_setopt( $ch, CURLOPT_URL, $url );
    //curl_setopt ($ch, CURLOPT_HEADER, 1);
    curl_setopt( $ch, CURLOPT_RETURNTRANSFER, 1 );
    curl_setopt( $ch, CURLOPT_CONNECTTIMEOUT, $timeout );
    $content = curl_exec( $ch );
    curl_close( $ch );

    return $content;
  }
}//Reader
```

### Eu disse não à herança

Geralmente, temos uma certa tendência a querer colocar esses métodos em uma class Abstrata, e então Twitter, Facebook, WordPress, extenderem essa class.

Porém, do ponto de vista da Orientação a Objetos, isso não é bacana. Afinal, nossos objetos **usam** pq precisam os métodos curlFile, getJSON, mas **não são** isso.

O objeto Twitter não deve ter a responsabilidade de ir buscar o jSON, nem de fazer o cache, nem de interar um loop.

Apenas deve saber oque fazer com os dados já mastigados, e assim por diante.

#### Vantagem

Uma vantagem, é que essa class Reader pode ser utilizada em outro projeto, sozinha. Desacoplei o código dela do restante da aplicação.

### Extends pode e deve ser usado, mas na hora correta

Dentro deste mesmo projeto, eu precisava retornar dados, de mais de um blog WordPress. E para cada blog, havia um html diferente. Digamos que uma &#8220;especialização&#8221; do que a class WordPress fazia. Logo, **aqui sim**, coube usar herança:

``` php
<?php

include_once 'iSource.class.php';
/**
 * @file Statusblog.class.php
 * @date 2012-05-04
 * @author William Moraes
 * @usage

   $Statusblog = new Statusblog( $reader );
  $Statusblog->setURL( 'http://feeds.feedburner.com/BlogLocaweb14elwSalvador' );
  echo $view->draw( $Statusblog );


 */
class Statusblog extends WordPress
{

  /**
   * @overwrite parent::html()
   * @function html
   */
  public function html( $item )
  {
    return '<li>
      <a href="'.$item->link.'">'.$item->title.'</a>
      <div class="category">Categoria: '.$item->category.'</div>
      </li>'.PHP_EOL;
  }

}//Facebook
```

## Concluindo

Agora sim, eu tenho um projeto Orientado a Objetos. Um objeto conversando com outro, poucas dependências sólidas e bem resolvidas.

É isso. O que acham ?

criticas? sugestões? dúvidas?
