---
id: 1167
title: 'Navegação com QueryString - php'
date: 2011-07-11T20:31:38+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1167
permalink: /php/navegacao-querystring-php/
dsq_thread_id:
  - "2105261691"
categories:
  - PHP
---
Só passando para registar um código que deixei no fórum

<!--more-->

``` php
<?php
                function getGet( $key ){
                        return isset( $_GET[ $key ] ) ? $_GET[ $key ] : null;
                }
                        $pg = getGet('pg');
                        if( is_file( 'view/'.$pg.'.php' ) )
                                include 'view/'.$pg.'.php';
                        else
                                include 'view/home.php';
        ?>
```

tecnicamente, substituimos a tag <iframe> por esse código.

No meio do nosso arquivo **index.php**, fica esse controler, para ser uma espécie de FrontController.

O menu então fica assim:

``` html
<a href="?pg=home">Home</a>
<a href="?pg=contato">Contato</a>
<a href="?pg=gostei">Gostei</a>
```

sendo os arquivos <u>view/home.php</u>, <u>view/contato.php</u> e <u>view/gostei.php</u>.

Ele vê oque tem na URL, testa se existe aquele arquivo, na pasta view. Se existir ele inclui. Se não, ele manda para a home.

Podemos incrementar o tratamento, colocando uma opção de verdade para páginas que realmente não existem 404.

porém, por enqnto só quero deixar aqui esse resumido simples.
