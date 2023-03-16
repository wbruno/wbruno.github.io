---
id: 908
title: Cadastro de conteudo, formulário adiciona dados em tabela temporária
date: 2011-05-10T07:00:02+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=908
permalink: /javascript-puro/cadastro-de-conteudo-formulario-adiciona-dados-em-tabela-temporaria/
dsq_thread_id:
  - "2102672888"
categories:
  - Javascript
---
Salve salve!

Novamente, para termos algo, precisamos da iniciativa de começar.

Requisito:

> _&#8220;Um formulário simples, irá adicionando dados numa tabela html temporária, para depois enviar tudo de uma só vez para o banco.&#8221;_

<!--more-->



Do começo:

> _&#8220;Um formulário simples, .._

``` html
<form action="" method="post" id="form_prepare">
      <fieldset>
        <label>Nome: <input type="text" name="nome" /></label>
        <label>Telefone: <input type="text" name="email" /></label>
        <label>Email: <input type="text" name="telefone" /></label>

        <label><input type="submit" name="ok" value="Ok" /></label>
      </fieldset>
    </form><!-- /form_prepare -->
```

A outra parte:

> _&#8220;&#8230; numa tabela html temporária,&#8230;_

``` html
<table id="grid">
        <thead>
          <tr>
            <th>Nome</th>
            <th>Telefone</th>
            <th>Email</th>
          </tr>
        </thead>
        <tbody>
        </tbody>
      </table><!-- /grid -->
```

Importante isso. Começamos do início. Do HTML.

## A parte JavaScript

Agora, segundo nosso briefing, o formulário deve ir adicionando os itens nessa tabela. Aqui que entra, a responsabilidade client-side, afinal, precisamos adicionar os itens nessa tabela temporariamente, sem refresh [ e atenção, pois isso **não significa, e nem quer dizer** ajax. &#8216;Sem refresh&#8217;, [quer dizer client-side, mas não necessariamente precisamos de ajax](http://www.wbruno.com.br/2011/04/08/o-que-e-ajax-e-o-que-nao-e/).

``` html
<script type="text/javascript"> type="text/javascript">
$(document).ready(function(){
  $('#form_prepare').submit(function(){
    var $this = $( this );

    var tr = '<tr>'+
      '<td>'+$this.find("input[name='nome']").val()+'</td>'+
      '<td>'+$this.find("input[name='email']").val()+'</td>'+
      '<td>'+$this.find("input[name='telefone']").val()+'</td>'+
      '</tr>'
    $('#grid').find('tbody').append( tr );

    return false;
  });
});
</script>
```

Tranquilo até aqui, certo ?

no evento **onSubmit** do meu formulário, disparo essa function javascript, que lê o que está digitado nos inputs deste form, e faz um append lá na minha <table>

Só ficou faltando um pedaço, pois precisamos desses dados &#8216;para depois&#8217;.

A minha escolha será adicionar inputs type=&#8221;hidden&#8221;, em um <u>outro formulário</u>, e este sim, será responsável por enviar todos os dados da nossa table temporaria, para o servidor.

``` html
<form action="" method="post" id="form_insert">
      <fieldset style="display: none;"></fieldset>
      <label><input type="submit" name="cadastrar" value="Cadastrar" /></label>
    </form><!-- /form_insert -->
```

O JS desse trecho:

``` html
var hiddens = '<input type="hidden" name="nome[]" value="'+nome+'" />'+
      '<input type="hidden" name="email[]" value="'+email+'" />'+
      '<input type="hidden" name="telefone[]" value="'+telefone+'" />';

    $('#form_insert').find('fieldset').append( hiddens );
```

Prosseguindo..

## A parte PHP

Necessário nesse trecho, entendermos que trabalhar com array, simplifica todo o processo.

``` php
<?php
  if( $_SERVER['REQUEST_METHOD']=='POST' )
  {
    $sql = "INSERT INTO cliente ( id, nome, email, telefone ) VALUES ";

    $values = Array();
    for( $i=0; $i<count( $_POST['nome'] ); $i++ )
    {
      $values[] = "(NULL, '".filter( $_POST['nome'][$i] )."',
          '".filter( $_POST['email'][$i] )."',
          '".filter( $_POST['telefone'][$i] )."')";
    }
    echo $sql.implode( ',', $values );
  }
function filter( $str ){
  return addslashes( $str );//deixo demais filtros e validações por sua conta
}
?>
```

Os inputs hidden que serão adicionados, são do tipo:

``` html
<input type="hidden" name="email[]" value="valor" />```

Logo, receberemos um **array**: $\_POST\[&#8216;email&#8217;], com as posições: $\_POST[&#8216;email&#8217;\]\[0\], $_POST\[&#8216;email&#8217;\]\[1\]&#8230;

O código completo, então:

``` php
<?php
  if( $_SERVER['REQUEST_METHOD']=='POST' )
  {
    $sql = "INSERT INTO cliente ( id, nome, email, telefone ) VALUES ";

    $values = Array();
    for( $i=0; $i<count( $_POST['nome'] ); $i++ )
    {
      $values[] = "(NULL, '".filter( $_POST['nome'][$i] )."',
          '".filter( $_POST['email'][$i] )."',
          '".filter( $_POST['telefone'][$i] )."')";
    }
    echo $sql.implode( ',', $values );
  }
function filter( $str ){
  return addslashes( $str );//deixo demais filtros e validações por sua conta
}
?>
<html>
<head>
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.1/jquery.min.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $('#form_prepare').submit(function(){
    var $this = $( this );

    var nome = $this.find("input[name='nome']").val(),
      email = $this.find("input[name='email']").val(),
      telefone = $this.find("input[name='telefone']").val();

    var tr = '<tr>'+
      '<td>'+nome+'</td>'+
      '<td>'+email+'</td>'+
      '<td>'+telefone+'</td>'+
      '</tr>'
    $('#grid').find('tbody').append( tr );

    var hiddens = '<input type="hidden" name="nome[]" value="'+nome+'" />'+
      '<input type="hidden" name="email[]" value="'+email+'" />'+
      '<input type="hidden" name="telefone[]" value="'+telefone+'" />';

    $('#form_insert').find('fieldset').append( hiddens );

    return false;
  });
});
</script>
<style type="text/css">
#main {
  width: 700px; margin: 0 auto;
}
</style>
</head>
<body>
  <div id="main">
    <form action="" method="post" id="form_prepare">
      <fieldset>
        <label>Nome: <input type="text" name="nome" /></label>
        <label>Telefone: <input type="text" name="email" /></label>
        <label>Email: <input type="text" name="telefone" /></label>

        <label><input type="submit" name="ok" value="Ok" /></label>
      </fieldset>
    </form><!-- /form_prepare -->

    <table id="grid">
      <thead>
        <tr>
          <th>Nome</th>
          <th>Telefone</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
      </tbody>
    </table><!-- /grid -->
    <form action="" method="post" id="form_insert">
      <fieldset style="display: none;"></fieldset>
      <label><input type="submit" name="cadastrar" value="Cadastrar" /></label>
    </form><!-- /form_insert -->
  </div><!-- /main -->
</body>
</html>
```

Saída que obtive:

``` sql
INSERT INTO cliente ( id, nome, email, telefone ) VALUES (NULL, 'William', '(21) 1234-4567','email@teste.com.br'),(NULL, 'Bruno', '(21) 1234-1234','email@teste.com') ```

### <a href="http://www.wbruno.com.br/scripts/cadastro-formulario-table.php" target="_blank">Demonstração Online</a>

É isso =)
