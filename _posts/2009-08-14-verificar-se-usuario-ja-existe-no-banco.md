---
id: 830
title: Verificar se usuário já existe no banco
date: 2009-08-14T01:32:41+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=3
permalink: /ajax/verificar-se-usuario-ja-existe-no-banco/
dsq_thread_id:
  - "2100716820"
categories:
  - AJAX
---
E aee!

Primeiro post, e primeiro script em AJAX desse tipo&#8230; vamos lá..

Criando um pequeno e simples script em AJAX com jQuery, para verificar a existência de um usuário num banco de dados MySQL.

**dump.sql**

``` sql
--
-- Estrutura da tabela `usuario`
--
CREATE TABLE IF NOT EXISTS `usuario` (
  `idUsuario` int(10) NOT NULL AUTO_INCREMENT,
  `nomeUsuario` varchar(200) NOT NULL,
  PRIMARY KEY (`idUsuario`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=3 ;
--
-- Extraindo dados da tabela `usuario`
--
INSERT INTO `usuario` (`idUsuario`, `nomeUsuario`) VALUES
(1, 'William'),
(2, 'Bruno');
```

Arquivo **usuario.php**

``` php
<?php
  //envio o charset para evitar problemas com acentos
  header("Content-Type: text/html; charset=UTF-8");


  $mysqli = new mysqli('localhost', 'root', '', 'artigos');

  $user = filter_input(INPUT_GET, 'nomeUsuario');
  $sql = "SELECT * FROM `usuario` WHERE `nomeUsuario` = '{$user}'"; //monto a query


  $query = $mysqli->query( $sql ); //executo a query

  if( $query->num_rows > 0 ) {//se retornar algum resultado
    echo 'Já existe!';
  } else {
    echo 'Não existe ainda!';
  }
```

**index.php**

``` php
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Document</title>
</head>
<body>

<form action="usuario.php" method="GET">
  <label>Nome Usuário: <input type="text" name="nomeUsuario" /></label>
  <input type="button" name="verificar" id="verificar" value="verificar" />
</form>

<div id="resultado"></div>


<script type="text/javascript" src="http://code.jquery.com/jquery-1.11.3.min.js"></script>
<script type="text/javascript">
$(function(){ // declaro o início do jquery
  $("input[name='verificar']").on('click', function(){//botão para disparar a ação
    var nomeUsuario = $("input[name='nomeUsuario']").val();
    //console.log(nomeUsuario);
    $.get('usuario.php?nomeUsuario=' + nomeUsuario,function(data){
      $('#resultado').html(data);//onde vou escrever o resultado
    });
  });
});// fim do jquery
</script>

</body>
</html>
```

Basta fazer download do <a title="Link externo" rel="nofollow external" href="http://jquery.com/download/">jQuery</a>.

Criar a base com a tabela que postei a estrutura, e rodar os códigos. 

<h2>
  Validando usuário ao sair do input, sem clicar no botão
</h2>

<p>
  Para fazer essa verificação apenas ao &#8220;sair do campo&#8221;, sem precisar apertar o botão, use o evento onblur:
</p>

``` js
$("input[name='nomeUsuario']").on('blur', function(){
  var nomeUsuario = $(this).val();
  $.get('usuario.php?nomeUsuario=' + nomeUsuario, function(data){
    $('#resultado').html(data);
  });
});
```

<h2>
  Código no Github
</h2>

<p>
  <a href="https://github.com/wbruno/examples/tree/gh-pages/verify-user-on-db/">verify user on db</a>
</p>