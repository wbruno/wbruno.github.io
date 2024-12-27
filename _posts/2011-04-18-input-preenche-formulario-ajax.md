---
id: 817
title: Input preenche formulário com ajax
date: 2011-04-18T23:59:45+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=817
permalink: /ajax/input-preenche-formulario-ajax/
dsq_thread_id:
  - "2101198903"
categories:
  - AJAX
tags:
  - formulário
---
Boas galera!

Este aqui, é complementar do <a href="https://wbruno.com.br/ajax/combobox-preenche-input-ajax" target="_blank">Combobox preenche input ajax</a>.

Muita gente já perguntou, e já vi muitos outros usando esse meu script por ai. Para facilitar, fica aqui o script modificado, para que no lugar do <var><select></var>, seja um <var><input></var>, que no evento **onblur**, vai preencher o restante do formulário.

<!--more-->



Para deixar simples, e análogo ao outro, estou usando o &#8216;nome&#8217; como campo a ser pesquisado. Porém, convém lembrar, que o ideal, é trabalharmos com algo mais consistente, para esse tipo de consulta, como o CPF, ou RG.

**index.html**

``` html
<html>
<head>
  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.2/jquery.min.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){
    $("input[name='nome']").blur(function(){
      var $endereco = $("input[name='endereco']");
      var $telefone = $("input[name='telefone']");

      $endereco.val('Carregando...');
      $telefone.val('Carregando...');

        $.getJSON(
          'function.php',
          { nome: $( this ).val() },
          function( json )
          {
            $endereco.val( json.endereco );
            $telefone.val( json.telefone );
          }
        );
    });
  });
  </script>
</head>
<body>
  <form action="" method="post">
    <label>Nome: <input type="text" name="nome" /></label>
    <label>Endereço: <input name="endereco" type="text" disabled="disabled" value="" /></label>
    <label>Telefone: <input type="text" name="telefone" value="" /></label>
  </form>
</body>
</html>
```

**function.php**

``` php
<?php
  /**
   * função que devolve em formato JSON os dados do cliente
   */
  function retorna( $nome, $db )
  {
    $sql = "SELECT `id`, `nome`, `telefone`, `endereco`
      FROM `cliente` WHERE `nome` = '{$nome}' ";

    $query = $db->query( $sql );

    $arr = Array();
    if( $query->num_rows )
    {
      while( $dados = $query->fetch_object() )
      {
        $arr['endereco'] = $dados->endereco;
        $arr['telefone'] = $dados->telefone;
      }
    }
    else
      $arr['endereco'] = 'não encontrado';

    return json_encode( $arr );
  }

/* só se for enviado o parâmetro, que devolve os dados */
if( isset($_GET['nome']) )
{
  $db = new mysqli('localhost', 'root', '123', 'test');
  echo retorna( filter ( $_GET['nome'] ), $db );
}

function filter( $var ){
  return $var;//a implementação desta, fica a cargo do leitor
}
```

**dump.sql**

``` sql
--
-- Estrutura da tabela `cliente`
--

CREATE TABLE IF NOT EXISTS `cliente` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nome` varchar(50) NOT NULL,
  `telefone` varchar(14) NOT NULL,
  `endereco` varchar(70) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=3 ;

--
-- Extraindo dados da tabela `cliente`
--

INSERT INTO `cliente` (`id`, `nome`, `telefone`, `endereco`) VALUES
(1, 'Bruno', '(11) 1234-5678', 'Rua dos Bobos, 0'),
(2, 'William', '(22) 2345-6789', 'Avenida blablabla, 14');
```

Prontinho.
