---
id: 2630
title: 'Outros maus cheiros em código css - Como sentir'
date: 2012-08-22T07:00:43+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2630
permalink: /css/como-sentir-mau-cheiro-em-codigo-css/
categories:
  - CSS
tags:
  - boas práticas
---
Eu já havia dado algumas dicas de [como sentir mau cheiro em código css](https://wbruno.com.br/css/mau-cheiro-em-codigo-css-como-sentir/ "Mau cheiro em código css - Como sentir"). Veja mais alguns outros pontos importantes em que vc deve ficar de olho.

[<img src="/wp-content/uploads/2012/08/css.jpg" alt="Linguagem CSS" title="css" width="600" height="346" class="aligncenter size-full wp-image-2638" srcset="/wp-content/uploads/2012/08/css.jpg 600w, /wp-content/uploads/2012/08/css-300x173.jpg 300w" sizes="(max-width: 600px) 100vw, 600px" />](/wp-content/uploads/2012/08/css.jpg)

<!--more-->

## Mau cheiro em código css

Interprete esses &#8220;maus cheiros&#8221; como algo que pode(provavelmente) estar errado. Que potencialmente irá lhe causar uma incompatibilidade entre os browsers.

Não são regras, e nem sempre lhe causarão problemas. Mesmo assim, vale a pena prestar atenção nas situações que vou expor.

## Não economize declaração de seletores

As vezes uma preguiça de colocar mais uma classe num elemento ou até mesmo um ID se for o caso, pode nos levar a usar erradamente seletores descendentes.

Na maioria das vezes, é melhor declarar uma class extra, do que usar:

``` css
#content h3 {}
```

por exemplo.

Basta imaginar que agora o que era um h3, será alterado para um h2, com o mesmo estilo.

Ou então que eu tenha algum outro h3 que deva receber uma estilização diferente dos demais.

Essa excessão terá que sobrescrever diversas propriedades herdadas desnecessariamente da regra anterior.

[<img src="/wp-content/uploads/2012/08/css-300x300.png" alt="" title="css" width="300" height="300" class="alignright size-medium wp-image-2652" srcset="/wp-content/uploads/2012/08/css-300x300.png 300w, /wp-content/uploads/2012/08/css-150x150.png 150w, /wp-content/uploads/2012/08/css.png 400w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2012/08/css.png)

## Como usar float

A propriedade <var>float</var>, flutua elementos para um dos lados(left|right), retirando este elemento do fluxo do documento, e fazendo com que o próximo na marcação html, ocupe o lugar que ele deixou vazio.

Dessa forma, esvaziando o container. É um erro comum declarar um float: left; para o elemento pai. Assim, &#8220;visualmente&#8221; ele volta a ganhar a altura que havia perdido por ter os seus filhos todos com float.

Note que isso é um grave erro. Pois se a propriedade existe para jogar um elemento para um lado, e assim colocar alguma outra coisa do outro lado, então que sentido faz flutuar um elemento que ocupa 100% da largura ? Pois é, nenhum. Não faça isso.

Um <var>display: table</var> ou uma altura fixa no container, ou até mesmo um elemento vazio logo antes do fechamento dele, com um <var>clear: both;</var> são as maneiras corretas, de lidar com este efeito colateral do float.

## De quem é a margem?

Margens em css são &#8220;espaçamentos&#8221; externos aos elementos. Tente enxergar dessa forma.

Que elemento está empurrando quem ? Geralmente é o da esquerda. Então este é quem deve ter uma <var>margin-right</var> para que o elemento da direita se afaste dele.

Se forem apenas 2 colunas, mais fácil colocar float: left em um, e float: right no outro, do que usar left nos 2, e usar margin-right no primeiro.

## O que é padding?

Os paddings são espaçamentos internos ao elemento.

Uma boa dica, é quando todo um conjunto de elementos de um box precisar se afastar uma mesma medida da borda do seu container. Ai temos um caso para usar padding e não margin.

## Valores gigantes?

Se você tem uma área útil de 960px de largura, e algum elemento com 300px ou mais de margin ou padding laterais, ou um left dessa magnitude&#8230; tome cuidado.

Pense bem.. se você desloca um bloco 300px para a esquerda, então ele está na verdade, na direita?

Logo, não era mais simples colocar ele na direita com um float: right; ou right: 0; do que ficar empurrando até chegar lá ?

Pense nisso. Revise suas implementações.

## Tome cuidado com seletores genéricos

<acronym title="Cascate Style Sheet">CSS</acronym> é o acronimo para Cascate Style Sheet. Mas nem sempre nos damos conta do que realmente é a cascata.

Um seletor do tipo: <var>p{}</var>, é genérico por demais.

Tome cuidado com declarações do tipo:

``` css
p {
    line-height: 16px;
    font-size: 12px;
}
```

Ai se você tiver algum parágrafo com font-size maior ou menor que <var>12px</var>, logicamente esse valor de line-height não ficará bacana.

Nessa situação em específico, eu indico usar na unidade <var>em</var>.

``` css
p {
    line-height: 1.3em;
    font-size: 12px;
}
```

O mais problemático na verdade, são propriedades css declaradas em seletores genéricos(de baixa especificidade) que acabam engessando e travando a sua implementação.

Estas são algumas das coisas que vemos todos dias, e podemos nos acostumar com observar elas. Sentir um mau cheiro no código css, te fará economizar tempo de implementação.
