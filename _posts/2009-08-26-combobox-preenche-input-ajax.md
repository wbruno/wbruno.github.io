---
id: 12
title: Combobox preenche input AJAX
date: 2009-08-26T19:45:40+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=12
permalink: /ajax/combobox-preenche-input-ajax/
dsq_thread_id:
  - "2101374968"
categories:
  - AJAX
tags:
  - formulário
---
Eu tô estudando AJAX com jQuery.. dá uma olhada.. você vai precisar do jQuery:

script corrijido para versões jquery 1.4.2

index.php

``` html
<html>
<head>
  <script type="text/javascript" src="jquery-1.4.2.min.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){
    $("select[name='nome']").change(function(){
      var endereco = $("input[name='endereco']");
      var telefone = $("input[name='telefone']");

      $( endereco ).val('Carregando...');
      $( telefone ).val('Carregando...');

        $.getJSON(
          'function.php',
          { idCliente: $( this ).val() },
          function( json )
          {
            $( endereco ).val( json.endereco );
            $( telefone ).val( json.telefone );
          }
        );
    });
  });
  </script>
</head>
<body>
  <form action="" method="post">
    <label>Nome: <select name="nome">
      <option value="">--</option>
<?php
  include 'function.php';
  echo montaSelect();
?>
    </select></label>
    <label>Endereço: <input name="endereco" type="text" disabled="disabled" value="" /></label>
    <label>Telefone: <input type="text" name="telefone" value="" /></label>
  </form>


  <div id="test"></div>
</body>
</html>
```

**function.php**

``` php
<?php
  $con = mysql_connect('localhost', 'root', '123');
  mysql_select_db('test', $con);

  /**
   * função que retorna o select
   */
  function montaSelect()
  {
    $sql = "SELECT `idCliente`, `nome` FROM `cliente` ";
    $query = mysql_query( $sql );

    if( mysql_num_rows( $query ) > 0 )
    {
      while( $dados = mysql_fetch_assoc( $query ) )
      {
        $opt .= '<option value="'.$dados['idCliente'].'">'.$dados['nome'].'</option>';
      }
    }
    else
      $opt = '<option value="0">Nenhum cliente cadastrado</option>';

    return $opt;
  }

  /**
   * função que devolve em formato JSON os dados do cliente
   */
  function retorna( $id )
  {
    $id = (int)$id;

    $sql = "SELECT `idCliente`, `nome`, `telefone`, `endereco`
      FROM `cliente` WHERE `idCliente` = {$id} ";
    $query = mysql_query( $sql );


    $arr = Array();
    if( mysql_num_rows( $query ) )
    {
      while( $dados = mysql_fetch_object( $query ) )
      {
        $arr['endereco'] = $dados->endereco;
        $arr['telefone'] = $dados->telefone;
      }
    }
    else
      $arr[] = 'endereco: não encontrado';

    return json_encode( $arr );
  }

/* só se for enviado o parâmetro, que devolve o combo */
if( isset($_GET['idCliente']) )
{
  echo retorna( $_GET['idCliente'] );
}


```

Usei php, e banco de dados MySQL.

Mas você conseguindo gerar o objeto JSON com a tua linguagem server-side, o script jquery que postei, se encarrega do resto do trabalho.

Em funcionamento:

<http://www.wbruno.com.br/scripts/combo-preenche-input.php>
