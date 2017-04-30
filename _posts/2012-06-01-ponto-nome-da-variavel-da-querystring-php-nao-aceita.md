---
id: 2030
title: 'Ponto no nome da variável da querystring &#8211; O php não aceita'
date: 2012-06-01T13:29:09+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2030
permalink: /php/ponto-nome-da-variavel-da-querystring-php-nao-aceita/
dsq_thread_id:
  - "2102292530"
categories:
  - PHP
---
Precisei usar parâmetros na querystring, com ponto no nome deles:

**?login.sys=wbruno**

Só que o ponto no php é uma estrutura da linguagem. Variaveis com ponto no nome não são válidas.
  
Isso me impossibilitou de receber o GET, da forma convencional:

<pre name="code" class="php">echo $_GET['login.sys'];//</pre>

Com um var_dump(), percebi que neste caso, o php faz a troca automaticamente, do ponto por um underline:

<pre name="code" class="php">echo $_GET['login_sys'];//wbruno</pre>

Rascunhei rapidamente o seguinte script para &#8220;desfazer&#8221; essa troca do php, e então usar no restante do projeto, o array $_GET, exatamente como está lá na URL.

<pre name="code" class="php">&lt;?php
        //var_dump( $_GET, $_GET['login.sys'], $_GET['login_sys'] );//array(1) { ["login_sys"]=> string(6) "wbruno" } NULL string(6) "wbruno" 


        var_dump( $_GET['login.sys'] );//NULL 


        $newGet = Array();
        foreach( $_GET AS $key=>$value )
        {
                $newGet[ str_replace( '_', '.', $key ) ] = $value;
        }


        $_GET = $newGet;

        echo '&lt;hr />';
        var_dump( $_GET['login.sys'] );//string(6) "wbruno" 
</pre>

E ai ? você já passou por isso ?
  
Como resolveu ?

@João Batista Neto, resolveu com htaccess:
  
https://www.facebook.com/neto.joaobatista/posts/470926322933918

<pre name="code" class="php">RewriteEngine On

RewriteCond %{QUERY_STRING} ^(.*)\.(.*)\=(.*)$
RewriteRule .* index.php?%1[%2]=%3 [QSA]
</pre>

Isso vai fazer:

Então: index.php?user.name=Teste
  
Virar: index.php?user[name]=Teste

E no PHP, acessamos:

<pre name="code" class="php">&lt;?php
echo $_GET['user']['name'];</pre>