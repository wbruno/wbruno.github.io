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

Este aqui, é complementar do <a href="http://www.wbruno.com.br/2009/08/26/combobox-preenche-input-ajax/" target="_blank">Combobox preenche input ajax</a>.

Muita gente já perguntou, e já vi muitos outros usando esse meu script por ai. Para facilitar, fica aqui o script modificado, para que no lugar do <var><select></var>, seja um <var><input></var>, que no evento **onblur**, vai preencher o restante do formulário.
  
<!--more-->


  
Para deixar simples, e análogo ao outro, estou usando o &#8216;nome&#8217; como campo a ser pesquisado. Porém, convém lembrar, que o ideal, é trabalharmos com algo mais consistente, para esse tipo de consulta, como o CPF, ou RG.

**index.html**

<pre class="html">&lt;html&gt;
&lt;head&gt;
  &lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.2/jquery.min.js"&gt;&lt;/script&gt;
  &lt;script type="text/javascript"&gt;
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
  &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;form action="" method="post"&gt;
    &lt;label&gt;Nome: &lt;input type="text" name="nome" /&gt;&lt;/label&gt;
    &lt;label&gt;Endereço: &lt;input name="endereco" type="text" disabled="disabled" value="" /&gt;&lt;/label&gt;
    &lt;label&gt;Telefone: &lt;input type="text" name="telefone" value="" /&gt;&lt;/label&gt;
  &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>

**function.php**

<pre class="php">&lt;?php
  /**
   * função que devolve em formato JSON os dados do cliente
   */
  function retorna( $nome, $db )
  {
    $sql = "SELECT `id`, `nome`, `telefone`, `endereco`
      FROM `cliente` WHERE `nome` = '{$nome}' ";

    $query = $db-&gt;query( $sql );

    $arr = Array();
    if( $query-&gt;num_rows )
    {
      while( $dados = $query-&gt;fetch_object() )
      {
        $arr['endereco'] = $dados-&gt;endereco;
        $arr['telefone'] = $dados-&gt;telefone;
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
}</pre>

**dump.sql**

<pre class="sql">--
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
(2, 'William', '(22) 2345-6789', 'Avenida blablabla, 14');</pre>

Prontinho.