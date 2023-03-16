---
id: 35
title: Combobox dinâmico com cadastro AJAX
date: 2010-04-07T07:54:58+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=35
permalink: /ajax/combobox-dinamico-com-cadastro-ajax/
categories:
  - AJAX
---
Cara, não é &#8216;algo comum&#8217;, mas achei interessante essa dúvida, e resolvi montar.
  
Em funcionamento:
  
<http://www.wbruno.com.br/scripts/form-cidade.php>

**config.inc.php**

``` php
<?php

        header("Content-Type: text/html; charset=ISO-8859-1");

        //Evitando cache de arquivo
        header('Expires: Mon, 26 Jul 1997 05:00:00 GMT');
        header('Last Modified: '. gmdate('D, d M Y H:i:s') .' GMT');
        header('Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0');
        header('Pragma: no-cache');
        header('Expires: 0');


        session_start();



///*
        define('SERVIDOR', 'localhost');
        define('USUARIO', 'root');
        define('SENHA', '123');
        define('BANCO', 'ajax');
//*/
```

**init.inc.php**

``` php
<?php
        define('BASE_PATH', realpath(dirname(__FILE__)).'/');

        if( !file_exists(BASE_PATH.'config.inc.php') )
                exit('Erro config.php nao encontrado');
        else
                require_once BASE_PATH.'config.inc.php';

        class Db
        {
                private static $instancia;

                private function __construct(){}
                private static function conecta()
                {
                        return new mysqli( SERVIDOR, USUARIO, SENHA, BANCO );
                }
                public static function pegaConexao()
                {
                        if ( self::$instancia == null )
                                self::$instancia = self::conecta();
                        return self::$instancia;
                }
        }
        function queryCidade( $where=null )
        {
                $mysqli = Db::pegaConexao();//pegando uma instância da conexão
                $sql = "SELECT `id` AS `value`, `nome` AS `label` FROM `cidade` {$where}";

                return $mysqli->query( $sql );
        }
        function comboCidade( $where=null )
        {
                $query = queryCidade( $where );

                return montaSelect( $query );
        }
        function montaSelect( $query )
        {
                if( $query->num_rows )
                        while( $dados = $query->fetch_object() )
                                $opt .= '<option value="'.$dados->value.'">'.$dados->label.'</option>'."\n";
                else
                        $opt = '<option value="0">Nenhum registro</option>';

                return $opt;
        }
        function cadastraCidade( $nome )
        {
                $nome = utf8_decode( $nome );
                $mysqli = Db::pegaConexao();//pegando uma instância da conexão
                $sql = "INSERT INTO `cidade`
                        (`id`, `nome`)
                        VALUES (NULL, '{$nome}')";

                return $mysqli->query( $sql );
        }
        function isPost()
        {
                if( $_SERVER['REQUEST_METHOD'] == 'POST' )
                        return true;
        }
        function getPost( $campo )
        {
                return isset( $_POST[$campo] ) ? filter( $_POST[$campo] ) : '';
        }
        function getGet( $campo )
        {
                return isset( $_GET[$campo] ) ? filter( $_GET[$campo] ) : '';
        }
        function filter( $var ){
                if( !get_magic_quotes_gpc() )
                        //$str = mysql_real_escape_string( $var );
                        $str = addslashes( $var );
                else
                        $str = $var;
                $str = str_replace( '#', '\#', $str );
                return $str;
        }
        function jsonCidade( $id=null )
        {
                $where = ( $id ) ? " WHERE `id` = {$id} " : '';

                $where .= ' ORDER BY `nome`';
                $query = queryCidade( $where );

                $json = ' [';
                if( $query->num_rows > 0 )
                        while( $dados = $query->fetch_object() )
                                $json .= '{"nome":"'.$dados->label.'","id":"'.$dados->value.'"}, ';
                else
                        $json .= '{"nome": "Não Encontrado"}';

                $json .= ']';

                return $json;
        }
        function existeCidade( $cidade )
        {
                $city = utf8_decode( $cidade );
                $query = queryCidade( " WHERE nome = '{$city}'" );
                if( $query->num_rows )
                        return $city.' já existe!';
                else
                        return cadastraCidade( $cidade );
        }
```

**retorno.php**

``` php
<?php
        include 'init.inc.php';

        if( isset($_GET['param']) )
        {
                echo jsonCidade( getGet('param') );
        }
        if( getPost('cidade') )
        {
                echo existeCidade( getPost('cidade') );
        }
```

**form-cidade.php**

``` php
<?php include 'init.inc.php'; ?>
<html>
<head>
        <title>Formulário de Cadastro</title>
        <meta name="author" content="William Bruno" />

        <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />

        <script type="text/javascript" src="jquery-1.4.2.min.js"></script>
        <script type="text/javascript">
        $(document).ready(function(){
                $("a[rel*='popup']").click(function( e ){
                        e.preventDefault();
                        var param = $(this).attr('rel').split(';');

                        window.open( $(this).attr('href'), $(this).attr('href'), param[1] );
                });
        });
        function carregarCombo( param, combo )
        {
                $("img[src='ico-loading.gif']").show();
                $.getJSON(
                        'retorno.php',
                        {param: param},
                        function(data){
                                var option = new Array();

                                resetaCombo( combo );
                                $.each(data, function(i, obj){

                                        option[i] = document.createElement('option');
                                        $( option[i] ).attr( {value : obj.id} );
                                        $( option[i] ).append( obj.nome );

                                        $("select[name='"+combo+"']").append( option[i] );
                        });
                        $("img[src='ico-loading.gif']").hide();
                });
        }
        function resetaCombo( el )
        {
                $("select[name='"+el+"']").empty();
                var option = document.createElement('option');
                $( option ).attr( {value : '0'} );
                $( option ).append( '' );
                $("select[name='"+el+"']").append( option );
        }
        </script>
</head>
<body>
        <form action="" method="post">
                <label>Cidade: <select name="cidade">
                        <option value=""></option>
<?php echo comboCidade(); ?>
                </select></label>
                <a href="cadastrar-cidade.php" rel="popup; width=300px, height=150px, top=150px, left=300px;">Cadastrar Cidade</a>

                <img src="ico-loading.gif" alt="" style="display: none;" />
        </form>
</body>
</html>
```

**cadastrar-cidade.php**

``` php
<?php
        include 'init.inc.php';
        $msg = null;
        if( isPost() )
                $msg = existeCidade( getPost('cidade') ) ? 'Cadastro efetuado' : 'Ocorreu um erro';
?>
<html>
<head>
        <title>Formulário de Cadastro</title>
        <meta name="author" content="William Bruno" />

        <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />

        <script type="text/javascript" src="jquery-1.4.2.min.js"></script>
        <script type="text/javascript">
        $(document).ready(function(){
                $("a.voltar").hide();
                $("input[name='fechar']").click(function(){
                        fechar_pop();
                });
                $("input[name='enviar']").click(function(){
                        $("img[src='ico-loading.gif']").show();
                        $( this ).attr({ disabled: 'disabled'});
                        $("input[name='cidade']").attr({ disabled: 'disabled'});
                        $.ajax({
                                type: 'POST',
                                url: 'retorno.php',
                                data: 'cidade='+$("input[name='cidade']").val(),
                                success: function( data ){
                                        if( data!=1 )
                                        {
                                                $("input[name='enviar'], input[name='cidade']").attr({ disabled: ''});
                                                $("input[name='cidade']").val('');
                                                $("input[name='cidade']").focus();

                                                $('#retorno').html( data );
                                        }
                                        else
                                                fechar_pop();
                                },
                                complete: function( xhr, status ){
                                        $("img[src='ico-loading.gif']").hide();
                                }
                        });
                        return false;
                });
        });
        function fechar_pop()
        {
                window.close();
                if ( window.opener && !window.opener.closed )
                        window.opener.carregarCombo( '', 'cidade' );
        }
        window.onbeforeunload = fechar_pop;
        </script>
</head>
<body>
<?php if( !$msg ){ ?>
        <form action="" method="post">
                <label>Cidade: <input type="text" name="cidade" /></label>
                <label><input type="submit" name="enviar" value="Enviar" /></label>
                <img src="ico-loading.gif" alt="" style="display: none;" />
                <p id="retorno"></p>
        </form>
<?php } else echo $msg; ?>
        <a href="form-cidade.php" class="voltar">voltar</a>
</body>
</html>
```

**ico-loading.gif**
  
![Imagem Loading](http://www.wbruno.com.br/scripts/ico-loading.gif)
  
<a title="Link externo" rel="nofollow external" href="http://www.wbruno.com.br/scripts/ico-loading.gif">http://www.wbruno.com.br/scripts/ico-loading.gif</a>

**jquery-1.4.2.min.js**
  
<a title="Link externo" rel="nofollow external" href="http://code.jquery.com/jquery-1.4.2.min.js">http://code.jquery.c&#8230;ry-1.4.2.min.js</a>

Os códigos estão ai e funcionam.