---
id: 241
title: Atualizar SQL através de ação em checkbox
date: 2011-03-16T00:12:46+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=241
permalink: /jquery/atualizar-sql-atraves-de-acao-em-checkbox/
categories:
  - jQuery
---
Boas Galera !

Exemplo rápido, o &#8216;dificil&#8217; aqui, seria apenas descobrir o ID do registro, mas isso resolvi com um **.next()**, pois guardei num hidden ali, o id do registro.

é a idéia de GRID que vamos reproduzir. Desmarca o checkbox, atualiza para 0 um campo da tabela, referente aquele ID, marca o checkbox, atualiza para 1.

<!--more-->

``` html
<html>
<head>
  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){
    $("input[name='status[]']").click(function(){
      var $this = $( this );//guardando o ponteiro em uma variavel, por performance


      var status = $this.attr('checked') ? 1 : 0;
      var id = $this.next('input').val();


      $.ajax({
        url: 'action.php',
        type: 'GET',
        data: 'status='+status+'&id='+id,
        success: function( data ){
          alert( data );
        }
      });
    });
  });
  </script>
</head>
<body>
  <form action="" method="post">
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Nome</th>
          <th>Status</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>15</td>
          <td>Resident Evil</td>
          <td><input type="checkbox" name="status[]" value="1" />
            <input type="hidden" name="id" value="15" /></td>
        </tr>
        <tr>
          <td>17</td>
          <td>Tomb Raider</td>
          <td><input type="checkbox" name="status[]" value="1" />
            <input type="hidden" name="id" value="17" /></td>
        </tr>
        <tr>
          <td>21</td>
          <td>Prince of Persia</td>
          <td><input type="checkbox" name="status[]" value="1" />
            <input type="hidden" name="id" value="21" /></td>
        </tr>
      </tbody>
    </table>
  </form>
</body>
</html>
```

**action.php**

``` php
<?php
  ini_set('display_errors', true);
  error_reporting(E_ALL);

  if( isset( $_GET['status'] ) )
  {
    $id = (int)getGet('id');
    $sql = 'UPDATE `jogo` SET `status` = '.getGet('status').' WHERE `id` = '.$id;

    echo $sql;//aqui vc deve executar a query
  }
  function getGet( $key ){
    return isset( $_GET[ $key ] ) ? filter( $_GET[ $key ] ) : null;
  }
  function filter( $str ){
    return $str;//deixo a implementação desta por conta de vcs.
  }
```

<a href="http://www.wbruno.com.br/scripts/atualiza-checkbox.php" target="_blank">Demonstração</a>.
