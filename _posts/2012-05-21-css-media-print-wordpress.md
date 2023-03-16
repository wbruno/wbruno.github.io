---
id: 2026
title: 'CSS media print &#8211; WordPress'
date: 2012-05-21T18:10:23+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2026
permalink: /css/css-media-print-wordpress/
dsq_thread_id:
  - "2103450567"
categories:
  - CSS
---
=)

Acabei de implementar um css específico para impressão no tema do meu blog.
  
Usando media type=&#8221;print&#8221;. 

``` css
.really_simple_share,
  .searchform,
  #related-posts-via-categories-title,
  #related-posts-via-categories-list,
  #comments,
  #wrap_footer,
  iframe,
  #header form,
  .comments,
  .post footer,
  #sidebar { display: none; }
  #wrap { padding-top: 0; }
  #header { height: 25px; }
  #content { border: none; float: none; }

  .post { padding-bottom: 10px; }
  .post_content, .post header { padding-left: 0; }
  .post h1, .post h2, .post header { padding-bottom: 0; }
  .post header { display: table; }

  .post time { position: static; width: auto; box-shadow: none; font-size: 14px; text-align: left; clear: both; height: auto; }
  .post time span { display: inline-block; margin-left: 3px; background: none; box-shadow: none; }

  .with_sidebar .post_content,
  .with_sidebar { width: auto; }
  a { text-decoration: none; }
  a:after {
    content: " - ( " attr(href) " )";
    font-size: 0.7em;
  }
```