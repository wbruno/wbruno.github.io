---
id: 1159
title: Procurando link(url) com Expressão Regular php
date: 2011-07-08T15:45:10+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1159
permalink: /expressao-regular/procurando-linkurl-expressao-regular-php/
dsq_thread_id:
  - "2102320217"
categories:
  - Expressão Regular
---
Fiz uma ER rápida aqui. Procuro uma url dentro de um texto, e então substituo pelo HTML da âncora.

``` php
$description = preg_replace( '/(http:\/\/[\w\.\/-]+)/', '<a href="$1" rel="external">$1</a>', $li->description );
```

<!--more-->

## Entrada

``` html
locaweb_intl: New blog post: How Cloud Computing Can Help Your Business - http://tinyurl.com/how-cloud-computing-can-help
```

## Saída

``` html
locaweb_intl: New blog post: How Cloud Computing Can Help Your Business - <a rel="external" href="http://tinyurl.com/how-cloud-computing-can-help">http://tinyurl.com/how-cloud-computing-can-help</a>
```

=)
