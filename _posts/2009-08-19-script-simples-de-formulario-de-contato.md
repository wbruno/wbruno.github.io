---
id: 10
title: Script simples de formulário de contato
date: 2009-08-19T19:34:45+00:00
author: William Bruno
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

<pre name="code" class="php">&lt;?php
if( $_SERVER['REQUEST_METHOD']=='POST' ){
        $to                     = 'email@provedor.com'; //para quem vai o email
        $subject        = $_POST['assunto'];

                /* Mensagem */
        $message =
        '&lt;html>
        &lt;head>
        &lt;title>Titulo da página&lt;/title>
        &lt;style>
        &lt;/style>
        &lt;/head>
        &lt;body>'.
        '&lt;img src="" alt="" />'.'<br />'.
        '&lt;div id="opiniao">'.
        $_POST['nome'].'<br />'.
        ' , mandou a seguinte mensagem pela seção "Fale Conosco" do site:'.
        $_POST['mensagem'].'<br />'.
        'Deixou o seguinte telefone para contato:'.$_POST['tel'].' ,'.$_POST['cel'].
        '&lt;br />'.
        '&lt;/div>';

        $message .=
        '&lt;div id="rodape">Obrigado pelo contato, aguardamos a sua visita.&lt;/div>'.
        '&lt;/body>
        &lt;/html>';

        $headers = "MIME-Version: 1.1".PHP_EOL;
        $headers .= "Content-type: text/html; charset=iso-8859-1".PHP_EOL;
        $headers .= "From: eu@seudominio.com".PHP_EOL; // remetente
        $headers .= "Return-Path: eu@seudominio.com".PHP_EOL; // return-path

        $headers .= "Bcc: outroemail@provedor.com".PHP_EOL; //altere ou comente essa linha, para receber uma cópia oculta

        mail($to, $subject, $message, $headers);
                $msg = 'Obrigado pelo contato, aguardamos a sua visita.';
        }
?>
                &lt;h1>Formulário de exemplo&lt;/h1>
&lt;?php
        if( isSet($msg) )
                echo '&lt;span class="msg">'.$msg.'&lt;/span>';

        else { // só mostra o form se não existir a mensagem de obrigado
?>
                &lt;form action="" method="post">
                &lt;fieldset>
                        &lt;label>*Nome Completo:
                                        &lt;input type="text" name="nome" title="* Nome Completo" />&lt;/label>
                        &lt;label>*Tel:
                                &lt;input type="text" name="tel" onkeypress="mascara(this,mtel)" maxlength="14" size="14" title="*Telefone" />&lt;/label>
                        &lt;label>*Cel:
                                &lt;input type="text" name="cel" onkeypress="mascara(this,mtel)" maxlength="14" size="14" title="*Celular" />&lt;/label>
                        &lt;label>*E-mail:
                                &lt;input type="text" name="email" title="*E-mail" />&lt;/label>
                        &lt;label>*Assunto:
                                &lt;input type="text" name="assunto" title="* Assunto" />&lt;/label>
                        &lt;label>*Mensagem:
                                &lt;textarea name="mensagem" rows="4" cols="25" title="* Mensagem">&lt;/textarea>&lt;/label>
                        &lt;label>&lt;input type="submit" name="enviar" value="Enviar" />&lt;/label>
                &lt;/fieldset>
                &lt;/form>
&lt;?php
        } // fecha else
?>

</pre>