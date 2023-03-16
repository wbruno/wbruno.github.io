---
id: 2862
title: 'Remover o termo &#8220;Comentário por&#8221; de cada comentário no seu blog WordPress'
date: 2012-11-26T07:00:06+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2862
permalink: /wordpress/remover-o-termo-comentario-por-de-cada-comentario-no-seu-blog-wordpress/
categories:
  - WordPress
---
Comentário por, Comentário por, Comentário por..

<!--more-->



Eu ainda não tinha me dado conta disso, dessa &#8220;falha&#8221; do WordPress, até ver um dado muito esquisito no meu WebMaster Tools.

[<img src="/wp-content/uploads/2012/11/Captura-de-Tela-2012-11-22-às-21.48.48.png" alt="" title="Captura de Tela 2012-11-22 às 21.48.48" width="589" height="271" class="aligncenter size-full wp-image-2868" srcset="/wp-content/uploads/2012/11/Captura-de-Tela-2012-11-22-às-21.48.48.png 589w, /wp-content/uploads/2012/11/Captura-de-Tela-2012-11-22-às-21.48.48-300x138.png 300w" sizes="(max-width: 589px) 100vw, 589px" />](/wp-content/uploads/2012/11/Captura-de-Tela-2012-11-22-às-21.48.48.png)

## Segunda palavra mais relevante

Caraca.. lógico que não quero ser encontrado por esse termo..

Mas ele aparece repetidas vezes no meu blog, por causa do sistema de comentários do wordpress.

[<img src="/wp-content/uploads/2012/11/Captura-de-Tela-2012-11-22-às-21.46.20.png" alt="" title="Captura de Tela 2012-11-22 às 21.46.20" width="318" height="673" class="aligncenter size-full wp-image-2865" />](/wp-content/uploads/2012/11/Captura-de-Tela-2012-11-22-às-21.46.20.png)

Provavelmente, você vai encontrar no arquivo **comments.php**, ou no **functions.php** do seu tema, a declaração desse &#8220;Comentário por&#8221;.

Parecido com isso aqui:

``` php
<?php comment_type(_x('Coment&aacute;rio', 'noun'), __('Trackback'), __('Pingback')); ?>
<?php _e('por'); ?>
<?php comment_author_link() ?>
```

Sugiro remover.. hehe =)

``` php
<?php _e('por'); ?>
<?php comment_author_link() ?>
```

E ai ? ainda tinha isso no teu blog ? corre lá e tira. =)
