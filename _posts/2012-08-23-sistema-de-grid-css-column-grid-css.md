---
id: 2615
title: 'Sistema de GRID CSS 960 &#8211; Classes CSS com mais significado'
date: 2012-08-23T07:00:57+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2615
permalink: /css/sistema-de-grid-css-column-grid-css/
dsq_thread_id:
  - "2104976286"
categories:
  - CSS
---
O conceito de **grid css** é ótimo! E para realmente ser implementado, precisa vir desde o wireframe.

Os designers da equipe já precisam usar a base com as linhas guia, se você quiser conseguir aplicar um sistema de grid css nos teus projetos.

[<img src="/wp-content/uploads/2012/08/Captura-de-Tela-2012-08-21-às-09.25.19.jpg" alt="grid css 960gs" title="Captura-de-Tela-2012-08-21-às-09.25.19" width="600" height="218" class="aligncenter size-full wp-image-2688" srcset="/wp-content/uploads/2012/08/Captura-de-Tela-2012-08-21-às-09.25.19.jpg 600w, /wp-content/uploads/2012/08/Captura-de-Tela-2012-08-21-às-09.25.19-300x109.jpg 300w" sizes="(max-width: 600px) 100vw, 600px" />](/wp-content/uploads/2012/08/Captura-de-Tela-2012-08-21-às-09.25.19.jpg)

<!--more-->

## Bom para os designers

Pois eles perdem menos tempo definindo larguras. Medindo alinhamentos.

Basta seguir as guias, colocando 2 colunas, 3 colunas..

## Bom para os DEVs

Pois conseguiremos num projeto grande, manter um padrão de estrutura entre diversos desenvolvedores.

## GRID CSS com 960gs

Só não sou muito fãn, pois me incomoda esse tipo de coisa:

<pre name="code" class="html">&lt;div class="container_12">..
    &lt;div class="grid_xx">..
        &lt;div class="grid_x push_x">
</pre>

Tenho a impressão que criaram o <a href="http://960.gs/" rel="external" title="Sistema de GRID CSS - 906gs">960gs</a> para que desenvolvedores _&#8220;Não FrontEnds&#8221;_ pudessem utilizar. Ok, existe um mérito nisso.. mas eu sou frontend, e exatamente por isso, me incomoda posicionar colunas com paddings? e position..

Não faz sentido. A propriedade <var>padding</var> existe para definirmos espaçamentos internos a um elemento.

E <var>position: relative</var>, existe para deslocarmos em alguma direção apartir do ponto inicial em que o elemento se encontrava.

## GRID CSS com 1140 css grid

Eu havia pensado da mesma forma que os criadores do projeto <a href="http://cssgrid.net/" rel="extenral">1140 css grid</a>, nomeando as classes pela quantidade de colunas que elas &#8220;pegam&#8221; de um total de 12. Por exemplo, se eu tiver 3 colunas iguais, cada coluna seria: <var>.fourcol</var>.

Porém, é esquisito pensar assim.

## Minha sugestão para GRID CSS

Sei que existem diversos sistemas de grid css por ai, alguns até já preparados para serem responsivos. Porém ainda nenhum me convenceu.

Tenho implementado da seguinte forma:

<pre name="code" class="css">.column-full { width: 940px; }
.column-half { width: 460px; }
.column-third { width: 300px; }
	.column-two-thirds { width: 620px; }
.column-quarter { width: 220px; }
	.column-three-quarters { width: 700px; }
.column-sixth { width: 140px; }

.space-left { margin-left: 20px; }
.space-right { margin-right: 20px; }</pre>

ou seja, nomeio os meus elementos de acordo com a fração que eles ocupam no documento.

Se eu tiver 2 colunas iguais, então tenho:

<pre name="code" class="html">&lt;div class="column-half fleft">&lt;/div>
&lt;div class="column-half fright">&lt;/div></pre>

E o respiro entre elas eu &#8220;ganho&#8221; de graça, ao jogar uma para a esquerda e outra para a direita.

Se forem 3 colunas:

<pre name="code" class="html">&lt;div class="column-third space-right fleft">&lt;/div>
&lt;div class="column-third space-right fleft">&lt;/div>
&lt;div class="column-third fright">&lt;/div></pre>

E pronto! resolvido!

## .fleft e .fright

Estas classes foram declaradas no meu [css reset](http://wbruno.com.br/2012/03/06/meu-css-minimo-comum-todos-os-projetos-desenvolvo/).

## Porque &#8220;mais um&#8221; grid css?

Muito menos código do que os &#8220;concorrentes&#8221;, e mais liberdade para o desenvolvedor FrontEnd que utilizar.

Nomenclaturas mais intuitivas, sem gorduras estruturais.

Ainda não pensei em um &#8220;nome&#8221; para esse sistema de grid. Talvez algo como: **column css grid system**. 😉 sei lá..

O que achou ?

Você usa algum ? Por que ?

## Acompanhe as atualizações desse projeto no github

[Column.Gs](https://github.com/wbruno/column.gs)
