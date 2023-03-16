---
id: 1782
title: Adicionando widget de Últimos Posts com data no WordPress
date: 2012-02-14T21:02:27+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1782
permalink: /wordpress/adicionando-widget-de-ultimos-posts-data-wordpress/
dsq_thread_id:
  - "2102625964"
categories:
  - WordPress
---
Registrando um widget do WordPress, para listar ultimos posts, com data.
  
O widget padrão, não tem essa opção, então criei um novo bem simples.

<!--more-->

<pre name="code" class="php">function ultimos_posts_display() {
  // print some HTML for the widget to display here
  echo '<div class="sidebar-box ultimos-posts"><strong>&Uacute;ltimos posts</strong>
  <ul>';

  $recent_posts = wp_get_recent_posts();
  foreach( $recent_posts as $recent ){
    echo '<li><span>'.preg_replace( '/([0-9]{4})-([0-9]{2})-([0-9]{2})([\s0-9:]+)?/', '$3-$2-$1', $recent['post_date'] ).'</span>
    <a href="' . get_permalink($recent["ID"]) . '" title="Look '.$recent["post_title"].'" >' .   $recent["post_title"].'</a></li> ';
  }

  echo '</ul></div>';
}

wp_register_sidebar_widget(
  'ultimos_posts_1',        // your unique widget id
  'Ultimos posts',          // widget name
  'ultimos_posts_display',  // callback function
  array(                  // options
    'description' => 'Widget dos ultimos posts com data'
  )
);
```