---
id: 1451
title: Mostrar .html na URL mas, servir páginas .php
date: 2011-10-06T07:00:52+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1451
permalink: /php/mostrar-html-na-url-mas-servir-paginas-php/
dsq_thread_id:
  - "2114720294"
categories:
  - PHP
tags:
  - htaccess
---
Post rápido.

## Situação:

Temos um projeto desenvolvido em php. Porém queremos que na URL a extensão a ser mostrada para o visitante seja **.html**.

Uma forma de fazer isto, seria adicionando a extensão .html para ser interpretada pelo servidor como um script dinâmico, e assim todo e qualquer arquivo .html passaria pelo interpretador, a procura de código php.

``` html
AddType application/x-httpd-php html ```

Uma outra forma, consiste em somente reescrever a URL, mascarando a extensão .php, e fazendo o servidor devolver a requisição, para o respectivo arquivo .php.

Dessa forma aqui:

``` html
RewriteEngine On
RewriteRule ^([a-z]+)\.html$ $1.php [L]
```

## Note:

Acessando a URL: <u>http://localhost/index.html</u>, o arquivo que a ser chamado será o **index.php**.
  
E assim por diante, pois o nosso grupo ali, casa tudo o que for letras de a até z, em qualquer quantidade.

O que as RewriteRules fazem na verdade, é &#8216;traduzirem&#8217; para o servidor as requisições enviadas.
  
Na regra acima, pedi o arquivo: **index.html** e a regra no htacces traduziu para **index.php**.

## Um problema

Se realmente tivermos um arquivo: **teste.html**, com apenas a regra acima, o servidor vai ignorar a existência desse arquivo, e irá redirecionar a requisição para um **teste.php**.
  
Para corrigir isso, precisamos dizer para ele, que se existir o tal arquivo, deixa o mesmo responder oque foi pedido.

``` html
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^([a-z]+)\.html$ $1.php [L]```

ou seja, só vai aplicar a Regra, a condição for satisfeita:

``` html
RewriteCond %{REQUEST_FILENAME} !-f```

E ela diz que o nome requisitado **não** pode ser um arquivo.