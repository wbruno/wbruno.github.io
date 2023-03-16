---
id: 328
title: Upload de arquivo via FTP com php
date: 2011-03-24T16:00:16+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=328
permalink: /php/upload-de-arquivo-ftp-php/
dsq_thread_id:
  - "2100803045"
categories:
  - PHP
---
Formulário HTML, enviando arquivo via FTP com php.
  
Apenas o mínimo necessário para fazer o upload.

<!--more-->

Outro script que estava <a href="http://forum.imasters.com.br/topic/391792-upload-de-um-dominio-para-outro-ftp/page__view__findpost__p__1528296" target="_blank">esquecido e perdido</a> pelo iMasters.

``` php
<?php
if( $_SERVER['REQUEST_METHOD']=='POST' )
{
        var_dump( $_FILES );//apenas para debug


        $servidor = 'host';
        $caminho_absoluto = '/httpdocs/uploads/';
        $arquivo = $_FILES['arquivo'];

        $con_id = ftp_connect($servidor) or die( 'Não conectou em: '.$servidor );
        ftp_login( $con_id, 'usuario', 'senha' );

        ftp_put( $con_id, $caminho_absoluto.$arquivo['name'], $arquivo['tmp_name'], FTP_BINARY );
}
?>
        <form action="" method="post" enctype="multipart/form-data">
                <input type="file" name="arquivo" />
                <input type="submit" name="enviar" value="Enviar" />
        </form>
```