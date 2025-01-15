---
id: 1058
title: Formulário de busca com filtro dinâmico em MySQL e php
date: 2011-05-28T10:35:20+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=1058
permalink: /php/formulario-de-busca-filtro-dinamico-em-mysql-php/
dsq_thread_id:
  - "2100758040"
categories:
  - PHP
---
Boas galerinha ^^

Post rápido pra ajudar um amigo aqui no msn.

A proposta é fazer aqueles formulários em que temos 2~3 ou mais inputs, que servirão de filtro para a consulta que faremos na base de dados.

Porém, o usuário pode querer preencher apenas um desses campos, 2 deles, ou todos.. e a nossa query, deve se adequar a esta realidade, mandando pro servidor apenas a consulta correta.

<!--more-->

Abaixo está a &#8216;minha solução&#8217; para o problema.

Usando 1 array, e alguns ifs, fica tudo bem prático.

``` php
<?php
  if( $_SERVER['REQUEST_METHOD']=='POST' )
  {
    $where = Array();

    $nome = getPost('n');
    $cidade = getPost('c');
    $bairro = getPost('b');


    if( $nome ){ $where[] = " `nome` = '{$nome}'"; }
    if( $cidade ){ $where[] = " `cidade` = '{$cidade}'"; }
    if( $bairro ){ $where[] = " `bairro` = '{$bairro}'"; }

    $sql = "SELECT nome, cidade, bairro FROM local ";
    if( sizeof( $where ) )
      $sql .= ' WHERE '.implode( ' AND ',$where );

    echo $sql;//execute a query aqui
  }
  //a cargo do leitor melhorar o filtro anti injection
  function filter( $str ){
    return addslashes( $str );
  }
  function getPost( $key ){
    return isset( $_POST[ $key ] ) ? filter( $_POST[ $key ] ) : null;
  }
?>
<style type="text/css">
label { display: block; }
</style>
<form action="" method="post">
  <label>Nome: <input type="text" name="n" /></label>
  <label>Cidade: <input type="text" name="c" /></label>
  <label>Bairro: <input type="text" name="b" /></label>


  <label><input type="submit" name="ok" value="Ok" /></label>
</form>
```
