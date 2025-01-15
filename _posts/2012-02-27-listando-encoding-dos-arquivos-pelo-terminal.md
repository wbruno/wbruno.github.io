---
id: 1800
title: Listando encoding dos arquivos pelo terminal
date: 2012-02-27T12:49:36+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=1800
permalink: /mac/listando-encoding-dos-arquivos-pelo-terminal/
dsq_thread_id:
  - "2102164360"
categories:
  - MAC
tags:
  - terminal
---
Um comando para listar pelo terminal, o encoding dos arquivos de determinada pasta.

``` bash
Mac-mini:lw_html5 william$ for file in *.php; do file --mime $file; done
404.php: text/x-php; charset=us-ascii
archive.php: text/x-php; charset=utf-8
comments.php: text/x-php; charset=us-ascii
footer.php: text/plain; charset=us-ascii
functions.php: text/x-php; charset=us-ascii
header.php: text/html; charset=us-ascii
index.php: text/x-php; charset=utf-8
page.php: text/x-php; charset=utf-8
search.php: text/x-php; charset=utf-8
searchform.php: text/plain; charset=us-ascii
sidebar.php: text/plain; charset=us-ascii
single.php: text/x-php; charset=utf-8
```

É isso.

=)
