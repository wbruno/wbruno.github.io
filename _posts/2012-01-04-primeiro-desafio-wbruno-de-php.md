---
id: 1700
title: Primeiro Desafio wbruno de PHP
date: 2012-01-04T16:33:58+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1700
permalink: /php/primeiro-desafio-wbruno-de-php/
categories:
  - PHP
---
Salve salve !!!

Vou fazer uma tentativa.. desafiozinho simples.. qndo eu tiver umas 3 respostas(certas ou não), eu divulgo a minha solução.(podem continuar enviando as suas contribuições, mesmo que eu já tenha colocado a minha).

Resolva com **2 loops**. Se conseguir, resolva com **um único loop.**

<!--more-->



O desafio, é gerar o resultado abaixo(na imagem), usando php(seu php vai gerar algum html).

[<img src="/wp-content/uploads/2012/01/Screen-shot-2012-01-04-at-4.33.25-PM-242x300.png" alt="" title="Screen shot 2012-01-04 at 4.33.25 PM" width="242" height="300" class="aligncenter size-medium wp-image-1701" srcset="/wp-content/uploads/2012/01/Screen-shot-2012-01-04-at-4.33.25-PM-242x300.png 242w, /wp-content/uploads/2012/01/Screen-shot-2012-01-04-at-4.33.25-PM.png 288w" sizes="(max-width: 242px) 100vw, 242px" />](/wp-content/uploads/2012/01/Screen-shot-2012-01-04-at-4.33.25-PM.png)

Podem me enviar o código pelo <a href="http://www.pastebin.com" target="_blank">www.pastebin.com</a>, aqui pelos comentários do blog mesmo.

é isso!

O melhor algorítmo(mais elegante) vence.

Boa Sorte!

.

.

.

.

.

.

.

.

.

.

.

.

.

## Minha solução com 2 loops encaixados:

``` php
<style type="text/css">
#grid td {
  width: 25px;
  height: 25px;
  text-align: center;
}
#grid td.diagonal {
  background: #000;
  color: #f00;
}
</style>
<table id="grid">
<?php
  for( $i=1; $i<10; $i++ )
  {
    echo '<tr>';
    for( $j=1; $j<10; $j++ )
    {
      $class = $i==$j || $i+$j==10 ? ' class="diagonal"' : '';
      $text = $i==5 || $j==5 ? '+' : '-';

      echo '<td'.$class.'>'.$text.'</td>';
    }
    echo '</tr>';
  }

?>
</table>
```
## Agora, resolvam com um único loop!

**Com 2 encaixados é fácil ne?!**

Mesma imagem, mesmas regras. **Consegue ?**

## Minha solução com apenas um único loop

``` php
<style type="text/css">
#grid td {
  width: 25px;
  height: 25px;
  text-align: center;
}
#grid td.diagonal {
  background: #000;
  color: #f00;
}
</style>
<table id="grid">
<tr>
<?php
  $j = 1;
  $k = 1;
  for( $i=0; $i<81; $i++ )
  {
    $ctrl = $i!=0 && $i%9==0;
    if( $ctrl ) echo '</tr>'.PHP_EOL.'<tr>'.PHP_EOL;

    $class = $j==$k || $j+$k==10 ? ' class="diagonal"' : '';
    $text = $j==5 || $k==5 ? '+' : '-';

    echo "\t".'<td'.$class.'>'.$text.'</td>'.PHP_EOL;

    $j = $j>=9 ? 1 : $j+1;
    $k = $j==1 ? $k+1 : $k;
  }
?>
</tr>
</table>
```
