---
id: 2210
title: 'Ler namespace xml php, usando a simplexml - content:encoded - feed WordPress'
date: 2012-08-08T07:00:39+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=2210
permalink: /wordpress/ler-namespace-xml-php-usando-a-simplexml/
dsq_thread_id:
  - "2101238834"
categories:
  - WordPress
tags:
  - xml
---
Vou falar sobre: ler namespace xml php.

## Ler feed do wordpress com php

Estamos bem acostumados a ler o **feeds do wordpress**(o famoso RSS), para reaproveitarmos a listagem de posts em outro ambiente, colocando os últimos posts na home do nosso site, ou alguma coisa desse tipo.

<!--more-->



Eu mesmo, aqui neste blog, já coloquei algumas formas de fazer isso:

-> [Ler rss do WordPress com php](https://wbruno.com.br/wordpress/ler-rss-wordpress-php/ "Ler rss do WordPress com php")

-> [Exemplo prático de Orientação a Objetos (php), diferenças e vantagens em relação à um código Estruturado](https://wbruno.com.br/php/exemplo-pratico-de-orientacao-objetos-php-diferencas-vantagens-em-relacao-a-um-codigo-estruturado/ "Exemplo prático de Orientação a Objetos (php), diferenças e vantagens em relação à um código Estruturado")

## Entender namespace xml php

Porém, eu ainda não havia falado nada sobre **ler namespace do xml, usando php**.

É necessário &#8220;registrar&#8221; aquele namespace, para que o php consiga ler corretamente. Se não, a única coisa que vai chegar será um objeto SimpleXML vazio:

``` php
object(SimpleXMLElement)#N (0) {}
```

Ou então, um nulo, não aparecendo absolutamente nada no <var>var_dump()</var> do objeto.

E isso conseguimos usando o children, em cima do objeto retornado pela simplexml\_load\_file() mesmo, desta forma aqui:

``` php
$content = $desc->children('http://purl.org/rss/1.0/modules/content/');
```

Note que a URL que passei para o children, é específica do meu namespace (&#8220;content&#8221;), se vc tiver trabalhando com outro namespace, então vc deve ir atrás da URL que registra ele.

## Featured Image

Fiz toda essa volta, para conseguir ler a &#8220;Imagem Destacada&#8221;, que podemos vincular a cada um de nossos posts, depois de setar este filtro, no functions.php do tema:

``` php
add_filter('the_content_feed', 'featured_image_feed');
```

A imagem aparece lá no feed, porém dentro da tag:

``` html
<content:encoded>..</content:encoded>
```
E por isso, eu precisava ler o namespace <var>content</var> do xml do feed do wordpress, para extrair a featured image de lá.

Sem mais, o código completo fica assim:

``` php
<?php

$rss = 'http://blog.devintegration.locaweb.com.br/feed/';


$xml = simplexml_load_file( $rss, 'SimpleXMLElement', LIBXML_NOCDATA );
$desc = $xml->children()->channel->item[0]; //->description;


$content = $desc->children('http://purl.org/rss/1.0/modules/content/');
var_dump( $content->encoded );


exit();
```

É isso galera. Comentem.

Neste caso, eu gosto de usar a simplexml, sei que com DOM fica mais robusto e tal.. porém dá uma olhada na simplicidade do meu código. =)

Usou ? comente.
