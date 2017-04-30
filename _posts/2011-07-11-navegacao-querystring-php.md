---
id: 1167
title: 'Navegação com QueryString &#8211; php'
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

<pre name="code" class="php">&lt;?php
                function getGet( $key ){
                        return isset( $_GET[ $key ] ) ? $_GET[ $key ] : null;
                }
                        $pg = getGet('pg');
                        if( is_file( 'view/'.$pg.'.php' ) )
                                include 'view/'.$pg.'.php';
                        else
                                include 'view/home.php';
        ?>
</pre>

tecnicamente, substituimos a tag <iframe> por esse código.
  
No meio do nosso arquivo **index.php**, fica esse controler, para ser uma espécie de FrontController.

O menu então fica assim:

<pre name="code" class="html">&lt;a href="?pg=home">Home&lt;/a>
&lt;a href="?pg=contato">Contato&lt;/a>
&lt;a href="?pg=gostei">Gostei&lt;/a>
</pre>

sendo os arquivos <u>view/home.php</u>, <u>view/contato.php</u> e <u>view/gostei.php</u>. 

Ele vê oque tem na URL, testa se existe aquele arquivo, na pasta view. Se existir ele inclui. Se não, ele manda para a home.
  
Podemos incrementar o tratamento, colocando uma opção de verdade para páginas que realmente não existem 404.

porém, por enqnto só quero deixar aqui esse resumido simples.