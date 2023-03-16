---
id: 111
title: Criar input no onblur, e receber dados array php
date: 2011-02-04T23:28:32+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=111
permalink: /jquery/criar-input-no-onblur-e-receber-dados-array-php/
dsq_thread_id:
  - "2101432454"
categories:
  - jQuery
---
Demonstração prática do método .live() do jQuery e trabalhando com arrays no php

``` php
<?php
  if( $_SERVER['REQUEST_METHOD']=='POST' )
  {
    $values = Array();
    foreach( $_POST['conta'] AS $conta )
    {
      if( !empty( $conta ) )
        $values[] = "(NULL, '{$conta}')";
    }
    $sql = "INSERT INTO `table` ( `id`, `conta` ) VALUES ".implode( ', ', $values );
    echo $sql;
  }
?>
<html>
  <head>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
    <script type="text/javascript">
      $(document).ready(function(){
        var i = 1;
        $('#campos input').live('blur', function(){
          if( $( this ).val()!='' && $('#campos input:last').val()!='' )
          {
          if( i<10 )//limitar em 10 campos
          {
            i++
            $('#campos').append( '<label>Conta '+i+':<input type="text" name="conta[]" value="" id="'+i+'" /></label>' )
              .find('input:last').focus();
            }
          }
        });
      });
    </script>
  </head>
  <body>
    <form action="" method="post">
      <fieldset id="campos">
        <label>Conta 1:<input type="text" name="conta[]" /></label>

      </fieldset><!-- /campos -->
      <label><input type="submit" name="ok" value="ok" /></label>
    </form>
  </body>
</html>
```