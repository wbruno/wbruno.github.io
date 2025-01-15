---
id: 24
title: 'Suggest AJAX - jQuery - php/Mysql'
date: 2010-01-08T23:32:31+00:00
author: wbruno
excerpt: Resolvi brincar um pouquinho aqui..
layout: post
guid: http://www.wbruno.com.br/blog/?p=24
permalink: /ajax/suggest-ajax-jquery-phpmysql/
dsq_thread_id:
  - "2101473987"
categories:
  - AJAX
---
Resolvi brincar um pouquinho aqui..

``` html
<html>
<head>
<title>Suggest</title>
<style type="text/css">
* {
        margin: ;
        padding: ;
        list-style: none;
        border: none;
}
form {
        width: 400px;
        margin:  auto;
}
form label {
        display: block;
}
form label input {
        margin: 2px;
        padding: 2px;
        border: 1px solid #000;
}
.suggest {
        position: relative;
}
.suggest input {
        width: 250px;
}
#suggest {
        position: absolute;
        top: 22px;
        right: 64px;
        background-color: #fff;
        width: 248px;
        text-align: left;
        border: 1px solid #000;
}
#suggest li {
        margin: 2px;
}
#suggest a {
        display: block;
        color: #000;
        text-decoration: none;
}
#suggest a:hover {
        background: #eee;
        text-decoration: underline;
        color: #f00;
}

</style>
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript">
        $(document).ready(function(){
                $("input[name='suggest']").keyup(function(){
                        createList('.suggest');
                        $.ajax({
                                type: "GET",//apenas pra ficar mais fácil de debugar, pode mudar para POST depois
                                url: "function.php",
                                data: "parte="+$(this).val(),
                                success: function( data ){
                                        $("#suggest").html( data );
                                }
                        });
                });

                $("#suggest a").live('click', function( e ){
                        e.preventDefault();
                        var href = $(this).attr('href');
                        var id = href.split('=');

                        $("input[name='id']").val( id[1] );
                        $("input[name='nome']").val( $(this).text() );

                        $("#suggest").remove();
                });
                $("#suggest").mouseout(function(){
                        $("#suggest").remove();
                });
        });
        function createList( el )
        {
                $("#suggest").remove();

                var list = document.createElement('ul');
                list.id = 'suggest';
                $( el ).append( list );
        }
</script>
</head>
<body>
        <form action="" method="post">
                <fieldset>
                        <label class="suggest">Vá digitando: <input type="text" name="suggest" /></label>

                        <label>ID: <input type="text" name="id" /></label>
                        <label>Nome: <input type="text" name="nome" /></label>
                </fieldset>
        </form>
        <p>Procure por: William, B, J..</p>
</body>
</html>
```

e o sql disso:

``` sql
--
-- Banco de Dados: `ajax`
--

-- --------------------------------------------------------

--
-- Estrutura da tabela `cliente`
--

CREATE TABLE IF NOT EXISTS `cliente` (
  `id` int(11) unsigned NOT NULL AUTO_INCREMENT,
  `nome` varchar(50) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `cliente_indexnome` (`nome`)
) ENGINE=MyISAM  DEFAULT CHARSET=latin1 PACK_KEYS= AUTO_INCREMENT=7 ;

--
-- Extraindo dados da tabela `cliente`
--

INSERT INTO `cliente` (`id`, `nome`) VALUES
(1, 'Jeovane Reges'),
(2, 'Felipe Gonçalves'),
(3, 'William'),
(4, 'William Bruno'),
(5, 'Bruno'),
(6, 'Bruno Rocha');
```

<strong style="font-style: normal; font-weight: bold !important;">function.php</strong>

``` php
<?php
        header("Content-Type: text/html; charset=ISO-8859-1");

        echo suggest( getGet('parte') );

function suggest( $palavra )
{
        $sql = "SELECT `id`, `nome` FROM `cliente` ";
        if( !empty($palavra) )
                $sql .= "WHERE `nome` LIKE '{$palavra}%'";

        $mysqli = new mysqli( 'localhost','root','123','ajax' );
        $query = $mysqli->query( $sql );
        if( $query->num_rows> )
        {
                $li='';
                while( $dados = $query->fetch_object() )
                        $li .= '<li><a href="?id='.$dados->id.'">'.$dados->nome.'</a></li>';
        }
        else
                $li = 'Nenhum cadastro encontrado!';

        return $li;
}
function getGet( $campo ){
        return ( isset($_GET[ $campo ]) ) ? filter( $_GET[ $campo ] ) : null;
}
function filter( $var )
{
        if( !get_magic_quotes_gpc() )
                $str = mysql_real_escape_string( $var );
        else
                $str = $var;
        $str = str_replace( '#', '\#', $str );
        return $str;
}
```

<img style="vertical-align: middle; border: 0px initial initial;" src="http://forum.imasters.uol.com.br/public/style_emoticons/default/happy.gif" alt="^_^" />

<img style="vertical-align: middle; border: 0px initial initial;" src="http://forum.imasters.uol.com.br/public/style_emoticons/default/natal_happy.gif" alt=":natal_happy:" />

em asp:

<http://forum.imasters.com.br/index.php?/topic/403150-autocomplete-do-banco-de-dados>
