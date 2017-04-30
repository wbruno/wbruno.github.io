---
id: 6
title: 'Div 100% redimensionável, com coluna fixa!'
date: 2009-08-16T02:38:21+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=6
permalink: /css/div-100-redimensionavel-com-coluna-fixa/
dsq_thread_id:
  - "2100998987"
categories:
  - CSS
---
Boa galeraa!!!

Vendo mais uma dúvida no fórum iMasters, resolvi criar uma solução simples e crossbrowser aqui.
  
Totalmente em CSS, e com uma marcação xHTML simples.

Vamos lá!

&#8220;O problema&#8221;:

Criar uma DIV com width 100%, sendo que ela deve ter uma coluna com width fixo

<pre>&lt;!DOCTYPE html>
&lt;html lang="en">
&lt;head>
  &lt;meta charset="UTF-8">
  &lt;title>Document&lt;/title>
&lt;head>
&lt;title>100% com coluna&lt;/title>
&lt;style type="text/css">
* {
  margin: 0;
  padding: 0;
}
p {
  margin-bottom: 15px;
}
#tudo {
  background: #ff0;
}
#coluna {
  float: right;
  width: 160px;
  background: #f0f;
  padding: 20px;
}
#conteudo {
  padding: 20px 220px 20px 20px; /* o right, é a soma do width da coluna com o padding desejado */
  text-align: justify;
}
&lt;/style>
&lt;/head>
&lt;body>
&lt;div id="tudo">
  &lt;div id="coluna">
    &lt;h1>Coluna&lt;/h1>
    &lt;p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque sodales ultricies venenatis. Duis eleifend tortor eget
    metus malesuada in dictum urna elementum. Mauris eleifend sapien ac magna auctor interdum condimentum tellus feugiat. Curabitur
    at hendrerit lacus. Phasellus augue tellus, euismod at tincidunt vel, feugiat auctor tellus. Fusce eu lectus erat, nec hendrerit
    velit. Fusce massa elit, hendrerit non convallis id, viverra vitae massa. Duis et leo sem, a ullamcorper justo.&lt;/p>
  &lt;/div>&lt;!-- /coluna -->
  &lt;div id="conteudo">
    &lt;h1>Conteúdo&lt;/h1>
    &lt;p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque sodales ultricies venenatis. Duis eleifend tortor eget
    metus malesuada in dictum urna elementum. Mauris eleifend sapien ac magna auctor interdum condimentum tellus feugiat. Curabitur
    at hendrerit lacus. Phasellus augue tellus, euismod at tincidunt vel, feugiat auctor tellus. Fusce eu lectus erat, nec hendrerit
    velit. Fusce massa elit, hendrerit non convallis id, viverra vitae massa. Duis et leo sem, a ullamcorper justo. Integer tempor,
    nunc a tempus consectetur, est ipsum tincidunt est, a vehicula mi ante ut lacus. Proin est massa, vulputate non lacinia ut,
    scelerisque a justo. Aliquam dapibus ipsum venenatis nisl ullamcorper quis imperdiet mi molestie. Nam rutrum sagittis feugiat.
    Sed pellentesque dictum mi sit amet tempor. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce sed consectetur arcu.
    Vivamus eget tellus tellus. Sed ultrices accumsan turpis sed ultricies. Fusce quis urna nec nunc auctor ullamcorper vel non risus.
    Pellentesque vehicula nisi ut lacus consequat nec laoreet mauris ultrices. Donec augue mauris, rhoncus in porta id, vehicula vel nulla.&lt;/p>
    &lt;p>Morbi auctor condimentum mauris ut vulputate. Cras molestie consequat imperdiet. Donec aliquet pellentesque dictum. Aenean blandit
    eleifend sem quis accumsan. Nulla sit amet turpis justo. In tempus elit eu erat auctor ut tincidunt tellus adipiscing. In sagittis
    ornare metus in volutpat. Proin sagittis diam eget nisl commodo dictum. In ornare nisi eu libero auctor malesuada eu quis diam.
    Cras vitae nisl non tellus rhoncus auctor. Morbi nec nibh magna. Maecenas elementum placerat lobortis. Nunc ornare feugiat ipsum,
    malesuada tristique metus consectetur eu. Cras lacus nisi, tincidunt non tristique at, pharetra vel urna. Aliquam at laoreet lorem.
    Etiam vestibulum metus quis ligula adipiscing laoreet vestibulum lacus lobortis. In odio metus, suscipit et dignissim vel, egestas
    sed nunc. Cras dignissim turpis eu justo sodales rutrum. Nulla facilisi.&lt;/p>
  &lt;/div>&lt;!-- /conteudo -->
&lt;/div>&lt;!-- /tudo -->
&lt;/body>
&lt;/html>
</pre>

Bom, não sei se tem muito oque explicar.. o código é este.
  
Qualquer coisa postem, que explico.

## Demonstração

<a href="http://wbruno.github.io/examples/100-with-fixed-width-column" target="_blank">100% com coluna</a>

## Código no github

<a href="https://github.com/wbruno/examples/blob/gh-pages/100-with-fixed-width-column/index.html" target="_blank">100% com coluna</a>
  
!