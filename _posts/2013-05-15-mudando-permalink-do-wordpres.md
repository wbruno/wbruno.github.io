---
id: 2964
title: Mudando permalink do wordpress
date: 2013-05-15T17:39:52+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2964
permalink: /wordpress/mudando-permalink-do-wordpres/
categories:
  - WordPress
---
É.. eu não sabia que o wordpress faz automaticamente..

Mas se por um acaso não fizer ou vc precisar fazer manualmente, o script abaixo lê todos os posts publicados, e escreve a regra htaccess para redicionar do formato <var>year/day/month/post_name</var> para <var>category/post_name</var>

<!--more-->

Chega de enrolação, e lá vai o código:

``` php
<?php
ini_set('display_errors', 1);

$mysqli = new mysqli('localhost', 'usuario', 'senha', 'banco');

$sql = "SELECT ID, post_name, DATE_FORMAT(post_date, '%Y/%m/%d') AS data FROM wp_posts
    WHERE
       post_type = 'post' AND
       post_status = 'publish'
    ";

$query = $mysqli->query($sql);


while( $dados = $query->fetch_object() ) {

  $sql = "SELECT * FROM `wp_term_taxonomy`
      JOIN wp_terms
        ON wp_terms.term_id = `wp_term_taxonomy`.term_taxonomy_id
      WHERE term_taxonomy_id
        IN (
          SELECT term_taxonomy_id
          FROM  `wp_term_relationships`
          WHERE object_id = {$dados->ID}
          )
        AND taxonomy = 'category'
      ORDER BY name ASC
      LIMIT 1";

  $query_cat = $mysqli->query( $sql );
  $dados_cat = $query_cat->fetch_object();


  $url = $dados->data.'/'.$dados->post_name.'/';
  $to = $dados_cat->slug.'/'.$dados->post_name.'/';


  echo 'RewriteRule ^'.$url.'$', ' ', $to ,' [NC,R=301,L]<br />';
}
```

A saída é neste formato:

``` bash
RewriteRule ^2009/08/14/verificar-se-usuario-ja-existe-no-banco/$ ajax/verificar-se-usuario-ja-existe-no-banco/ [NC,R=301,L]
```
