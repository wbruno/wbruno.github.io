---
id: 475
title: Adicionar inputs, com opção de removê-los
date: 2011-04-01T07:00:13+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=475
permalink: /jquery/adicionar-inputs-opcao-de-remove-los/
dsq_thread_id:
  - "2104496516"
categories:
  - jQuery
tags:
  - framework
---
Post rápido hoje.
  
Script melhorado de uma dúvida que surgiu no iMasters.
  
Sobre esse mesmo assunto, eu já tinha feito [esse post aqui meu](http://www.wbruno.com.br/2011/02/04/criar-input-no-onblur-e-receber-dados-array-php/), porém como o fluxo de interação do usuário é diferente, valeu a pena postar &#8216;de novo&#8217;.

<!--more-->

``` html
<html>
<head>
<script type="text/javascript" src="http://code.jquery.com/jquery-1.5.1.min.js"></script>
<script type="text/javascript">
$(document).ready(function(){

  var input = '<label>Nome: <input type="text" name="foto[]" /> <a href="#" class="remove">X</a></label>';

  $("input[name='add']").click(function( e ){
    $('#inputs_adicionais').append( input );
  });

  $('#inputs_adicionais').delegate('a','click',function( e ){
    e.preventDefault();
    $( this ).parent('label').remove();
  });

});
</script>
<style type="text/css">
fieldset { border: none; }
label { display: block; }
.remove { color:black;font-weight:bold;text-decoration:none; }
</style>
</head>
<body>

  <form action="" method="post">
    <label><input type="button" name="add" value="Add" /></label>
      <label>Nome: <input type="text" name="foto[]" /></label>

    <fieldset id="inputs_adicionais">
    </fieldset>
  </form>
</body>
</html>
```

Alguns pontos importantes
  
-> Uso o .delegate() no lugar do [.live()](http://www.wbruno.com.br/2011/03/18/metodo-live-jquery/)
  
-> indentei corretamente o script
  
-> sempre uso aspas duplas para delimitar os valores dos atributos HTML
  
-> não desperdiço IDs, e uso bem os seletores da lib
  
-> semântica na marcação do formulário

É isso ai. Se tiverem alguma sugestão de script, podem me encaminhar.