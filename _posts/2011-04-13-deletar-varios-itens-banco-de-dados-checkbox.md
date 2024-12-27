---
id: 742
title: Deletar vários itens do banco de dados, com checkbox
date: 2011-04-13T13:00:25+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=742
permalink: /php/deletar-varios-itens-banco-de-dados-checkbox/
dsq_thread_id:
  - "2100810985"
categories:
  - PHP
---
Dúvida recorrente no fórum.

Funcionamento parecido com os webmails.

Você possui uma lista de registros. Em cada um desses registros, há um checkbox.

Deseja-se, [selecionar vários checkboxs](https://wbruno.com.br/jquery/selecionar-todos-checkb-ao-clicar-em-um-selecionar-check-ao-clicar-em-linha/), e então com um só botão, proceder com a exclusão de todos os itens selecionados.

<!--more-->

``` php
<?php
  if( $_SERVER['REQUEST_METHOD']=='POST' ){
    $arr = filter( $_POST['excluir'] );

    $sql = 'DELETE FROM registro WHERE id IN('.implode( ',', $arr ).')';
    echo $sql;
  }
  function filter( $dados ){
    $arr = Array();
    foreach( $dados AS $dado ) $arr[] = (int)$dado;
    return $arr;
  }
?>


<form action="" method="post">
  <table>
    <tr>
      <td><input type="checkbox" name="excluir[]" value="13" /></td>
      <td>Registro 13</td>
    </tr>
    <tr>
      <td><input type="checkbox" name="excluir[]" value="9" /></td>
      <td>Registro 9</td>
    </tr>
    <tr>
      <td><input type="checkbox" name="excluir[]" value="26" /></td>
      <td>Registro 26</td>
    </tr>
    <tr>
      <td><input type="checkbox" name="excluir[]" value="14" /></td>
      <td>Registro 14</td>
    </tr>
  </table>
  <input type="submit" name="submit" value="Excluir Selecionados" />
</form>
```

Bom, é isso. Simples, prático e direto.

@2011-04-18 Adicionei a função **filter()**, para fazer o casting de tipo, antes de mandar para a string SQL. Dessa forma evitamos o injection mencionado pelos nossos colegas nos comentários deste post.
