---
id: 1088
title: Diferenciar refresh (f5) de post(submit)
date: 2011-06-15T05:38:05+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1088
permalink: /php/diferenciar-refresh-f5-de-postsubmit/
dsq_thread_id:
  - "2100719164"
categories:
  - PHP
---
Salve salve!

Este é um problema que assombra diversos desenvolvedores.
  
Temos um formulário, que será submetido para **mesma página**, em que ele se encontra:
  
<!--more-->

``` html
<form action="" method="post">
    <input type="text" name="ae" value="ae" />
    <input type="submit" name="enviar" value="enviar" />
  </form>
```

Até ai tudo bem. Se pudessemos redirecionar o usuário para outra página, não teríamos o &#8216;problema do F5&#8217;.
  
Mas se não pudermos fazer isso, o form está na **index.php**, essa mesma processa os dados enviados, e ela mesma vai mostrar o sucesso ou falha da requisição.

Logo, precisamos notar que <u>não adianta</u> apenas tentar apagar o post enviado:

<pre name="code" class="php">unset( $_POST );
```

O unset(), apenas vai liberar memória do servidor, pois quando o usuário apertar F5, quem vai enviar o POST novamente, é o navegador.

Poderíamos ter uma SESSION simples, do tipo: $\_SESSION[&#8216;ja\_enviado&#8217;];
  
Se ela tivesse com o valor &#8216;true&#8217;, poderíamos desconsiderar a requisição.

Mas, numa situação em que o usuário pode querer realmente enviar novamente o formulário(via submit), essa &#8216;ja_enviou&#8217; não resolve a questão. Não existe nenhuma diferença nos cabeçalhos da requisição, entre um submit via form, e um refresh que reenvia um submit.

Então, precisamos criar essa diferença, ou seja, distinguir, se a requisição atual, é a mesma da vez passada ou não.

``` php
<?php
  session_start();
  
  if( $_SERVER['REQUEST_METHOD']=='POST' )
  {
    $request = md5( implode( $_POST ) );
    
    if( isset( $_SESSION['last_request'] ) && $_SESSION['last_request']== $request )
    {
      echo 'refresh';
    }
    else
    {
      $_SESSION['last_request']  = $request;
      echo 'post';
    }
  }
?>
  <form action="" method="post">
    <input type="text" name="ae" value="ae" />
    <input type="submit" name="enviar" value="enviar" />
  </form>
```

=) Feito.
  
Nossa string guardada na session, vai impedir também que requisições iguais sejam enviadas(mesmo que ambas via submit).
  
O que não chega a ser ruim pois, se o cara já enviou uma vez, e sei lá, gravamos no banco, não tem sentido reescrevermos o mesmo dado de novo no banco, sendo que ele já está lá.

É isso galera.
  
A referência que pesquisei qndo precisei resolver essa situação está aqui:
  
<a href="http://pt.w3support.net/index.php?db=so&#038;id=456841" target="_blank">http://pt.w3support.net/index.php?db=so&id=456841</a>

Afinal, muito dificilmente seremos os primeiros a nos deparar com uma _&#8216;situação problema&#8217;_. E já que é assim, provavelmente alguém já o tenha solucionado. Fica a dica: pesquisem! =)