---
id: 280
title: Validar e enviar formulário com ajax, usando jquery.validate
date: 2011-03-21T15:35:10+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=280
permalink: /jquery/validar-enviar-formulario-ajax-usando-jquery-validate/
dsq_thread_id:
  - "2100739386"
categories:
  - jQuery
tags:
  - plugin
---
Bom, o motivo deste post, é para tentar acabar com os franksteins que tenho visto.

O cara vê jQuery, acha legal. Resolve começar a usar.

Tudo bem até aqui, se ele não tivesse feito essa escolha, antes de aprender a programar, o mínimo de Javascript Puro e Básico primeiro.

<!--more-->



Ai ele descobre os plugins, e como todo bom iniciante, fica maravilhado com oque falam sobre ajax.

Resolve então juntar um plugin de validação com o envio do form em ajax. Acontece que ele não pesquisou e nem foi instruído sobre a melhor forma de fazer isso.

Daí começam os problemas, erros, bugs.. e rondando blogs e mais blogs.. quase frustado, começam as gambiarras.

Basta usar o metodo do plugin, o **submitHandler**, não se esquecendo de mandar um return false; para impedir que o comportamento HTML do formulário seja seguido.

``` html
<html>
<head>
  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
  <script type="text/javascript" src="http://ajax.microsoft.com/ajax/jquery.validate/1.7/jquery.validate.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){
    $('#ajax_form').validate({
      rules: {
        nome: { required: true, minlength: 2 },
        email: { required: true, email: true },
        telefone: { required: true }
      },
      messages: {
        nome: { required: 'Preencha o campo nome', minlength: 'No mínimo 2 letras' },
        email: { required: 'Informe o seu email', email: 'Ops, informe um email válido' },
        telefone: { required: 'Nos diga seu telefone' }

      },
      submitHandler: function( form ){
        var dados = $( form ).serialize();

        $.ajax({
          type: "POST",
          url: "processa.php",
          data: dados,
          success: function( data )
          {
            alert( data );
          }
        });

        return false;
      }
    });
  });
  </script>
</head>
<body>
  <form method="post" action="" id="ajax_form">
    <label><input type="hidden" name="id" value="" /></label>
    <label>Nome: <input type="text" name="nome" value="" /></label>
    <label>Email: <input type="text" name="email" value="" /></label>
    <label>Telefone: <input type="text" name="telefone" value="" /></label>

    <label><input type="submit" name="enviar" value="Enviar" /></label>
  </form>
</body>
</html>
```

**processa.php**

``` php
<?php
  ini_set('display_errors', true);
  error_reporting(E_ALL);

  if( $_SERVER['REQUEST_METHOD']=='POST' )
  {
    if( !getPost('id') )
    {
      //significa um INSERT
      $sql = "INSERT INTO `tabela` (`id`, `nome`, `email`, `telefone`)
        VALUES
        (NULL, '".getPost('nome')."', '".getPost('email')."', '".getPost('telefone')."')";

    }
    else
    {
      //significa um UPDATE
      $sql = "UPDATE `tabela` SET `nome` = '".getPost('nome')."',
        `email` = '".getPost('email')."',
        `telefone` = '".getPost('telefone')."'
        WHERE `id` = ".getPost('id');
    }
    echo $sql;//executar a query

  }
  function getPost( $key ){
    return isset( $_POST[ $key ] ) ? filter( $_POST[ $key ] ) : null;
  }
  function filter( $var ){
    return $var;//faça o tratamento
  }
?>
```

O interessante, agora é notar que se for um UPDATE, os campos estarão preenchidos:

``` html
<label><input type="hidden" name="id" value="15" /></label>
    <label>Nome: <input type="text" name="nome" value="Bruno" /></label>
    <label>Email: <input type="text" name="email" value="email@provedor.com" /></label>
    <label>Telefone: <input type="text" name="telefone" value="(11) 1234-5678" /></label>
```

E então nesse caso, a resposta será:

``` sql
UPDATE `tabela` SET `nome` = 'Bruno',
        `email` = 'email@provedor.com',
        `telefone` = '(11) 1234-5678'
        WHERE `id` = 15
```
