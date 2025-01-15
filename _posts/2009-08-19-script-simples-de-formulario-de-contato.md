---
id: 10
title: Script simples de formulário de contato
date: 2009-08-19T19:34:45+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=10
permalink: /php/script-simples-de-formulario-de-contato/
dsq_thread_id:
  - "2100849254"
categories:
  - PHP
tags:
  - formulário
---
Script pra formulário de contato, enviando email com php.

Compatível com as novas diretrizes da Locaweb.

``` php
<?php
if( $_SERVER['REQUEST_METHOD']=='POST' ){
        $to                     = 'email@provedor.com'; //para quem vai o email
        $subject        = $_POST['assunto'];

                /* Mensagem */
        $message =
        '<html>
        <head>
        <title>Titulo da página</title>
        <style>
        </style>
        </head>
        <body>'.
        '<img src="" alt="" />'.'<br />'.
        '<div id="opiniao">'.
        $_POST['nome'].'<br />'.
        ' , mandou a seguinte mensagem pela seção "Fale Conosco" do site:'.
        $_POST['mensagem'].'<br />'.
        'Deixou o seguinte telefone para contato:'.$_POST['tel'].' ,'.$_POST['cel'].
        '<br />'.
        '</div>';

        $message .=
        '<div id="rodape">Obrigado pelo contato, aguardamos a sua visita.</div>'.
        '</body>
        </html>';

        $headers = "MIME-Version: 1.1".PHP_EOL;
        $headers .= "Content-type: text/html; charset=iso-8859-1".PHP_EOL;
        $headers .= "From: eu@seudominio.com".PHP_EOL; // remetente
        $headers .= "Return-Path: eu@seudominio.com".PHP_EOL; // return-path

        $headers .= "Bcc: outroemail@provedor.com".PHP_EOL; //altere ou comente essa linha, para receber uma cópia oculta

        mail($to, $subject, $message, $headers);
                $msg = 'Obrigado pelo contato, aguardamos a sua visita.';
        }
?>
                <h1>Formulário de exemplo</h1>
<?php
        if( isSet($msg) )
                echo '<span class="msg">'.$msg.'</span>';

        else { // só mostra o form se não existir a mensagem de obrigado
?>
                <form action="" method="post">
                <fieldset>
                        <label>*Nome Completo:
                                        <input type="text" name="nome" title="* Nome Completo" /></label>
                        <label>*Tel:
                                <input type="text" name="tel" onkeypress="mascara(this,mtel)" maxlength="14" size="14" title="*Telefone" /></label>
                        <label>*Cel:
                                <input type="text" name="cel" onkeypress="mascara(this,mtel)" maxlength="14" size="14" title="*Celular" /></label>
                        <label>*E-mail:
                                <input type="text" name="email" title="*E-mail" /></label>
                        <label>*Assunto:
                                <input type="text" name="assunto" title="* Assunto" /></label>
                        <label>*Mensagem:
                                <textarea name="mensagem" rows="4" cols="25" title="* Mensagem"></textarea></label>
                        <label><input type="submit" name="enviar" value="Enviar" /></label>
                </fieldset>
                </form>
<?php
        } // fecha else
?>

```
