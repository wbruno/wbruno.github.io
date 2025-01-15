---
id: 2994
title: Afinal, como nomear IDs e CLASSes no CSS/HTML ?
date: 2013-05-28T07:00:45+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=2994
permalink: /css/afinal-como-nomear-ids-e-classes-no-csshtml/
dsq_thread_id:
  - "2102165768"
categories:
  - CSS
tags:
  - boas práticas
  - tableless
---
Somos incentivados a usar <var>UpperCamelCase</var> para nomear classes em OOP, usamos <var>lowerCamelCase</var> nos nomes dos métodos, não podemos usar <var>dash-case</var> em nomes de variáveis (erro de sintaxe), por isso usamos <var>underscore_case</var>.. mas saindo do mundo backend, e voltando para o frontend, afinal, **como nomear ids e classes no css/html** ?

[<img src="/wp-content/uploads/2013/05/a1.png" alt="a" width="800" height="324" class="aligncenter size-full wp-image-2995" srcset="/wp-content/uploads/2013/05/a1.png 800w, /wp-content/uploads/2013/05/a1-300x121.png 300w" sizes="(max-width: 800px) 100vw, 800px" />](/wp-content/uploads/2013/05/a1.png)

<!--more-->

## Escolha um e somente um, e use

<var>lowerCamelCase</var>, onde a primeira letra da palavra é minúscula e as inicias das demais palavras são escritas em letra maiúscula.

<var>UpperCamelCase</var>, o mesmo de cima, mas a primeira letra da palavra é escrita em maiúscula.

<var>dash-case</var>, onde as palavras são separadas por um hífen, e tudo é sempre escrito em minúsculo.

<var>underscore_case</var>, onde as palavras são separadas por underlines.

<var>AlGoMuito_louco-eEsquisito</var>, nem preciso falar nada ne?! não faça isso.

Mas o problema começa não só quando vc está nomeando uma variavel, objeto, id ou class. O problema existe quando um mesmo projeto possui estilos diferentes de codificação nele mesmo, portanto, padronize. Entre em um acordo com a sua equipe.

## SMACSS - Scalable and Modular Arquiteture fore CSS

[<img src="/wp-content/uploads/2013/05/book-covers.png" alt="book-covers" width="247" height="328" class="alignleft size-full wp-image-2996" srcset="/wp-content/uploads/2013/05/book-covers.png 247w, /wp-content/uploads/2013/05/book-covers-225x300.png 225w" sizes="(max-width: 247px) 100vw, 247px" />](/wp-content/uploads/2013/05/book-covers.png) O <a href="http://smacss.com/" rel="nofollow">http://smacss.com/</a> não é um framework css, é um guia de estilo.

Toda a teoria dele é muito interessante e eu recomendo a leitura. O foco deste post é apenas como eu venho nomeando meus ids e classes.

### dash-case

Considero esse estilo mais próximo da linguagem css e html, do que os outros. As próprias propriedades css já são escritas em dash-case: <var>text-decoration</var>, <var>data-*</var>.. e assim por diante.

### in english

Afinal não podemos mesmo usar acentos, algumas palavras são menores e queremos que qualquer pessoa possa dar manutenção em nosso código. É o caso, por exemplo de plugins, frameworks e snippets open source. As linguagens já são em inglês, então se o nosso código também for fica mais natural ler.

## Pense em módulos

É comum quando estamos recortando layouts tableless, nos depararmos com partes da página que estarão presentes em mais de uma página. Por exemplo um box de depoimentos que pode existe na home e na página de preços de um produto.

O ideal é escrevermos um código html/css que possa ser copiado/movido de um lugar para o outro, sem que nada se perca e continue funcionando.

``` html
<ul id="comments">
    <li class="comment">
        <q class="comment-text">"lorem ipsum dolor sit amet..."</q>
        <cite class="comment-author">Desconhecido</cite>
    </li><!-- .comment -->
    <li class="comment">
        <q class="comment-text">"lorem ipsum dolor sit amet..."</q>
        <cite class="comment-author">Desconhecido</cite>
    </li><!-- .comment -->
</ul><!-- #comments -->
```

Só possuo um bloco de comentários por document, então uso ID para identificar esse bloco.

Cada LI é um <var>.comment</var>, e os filhos desse comentário, como o texto e o autor carregam o nome do pai neles: <var>.comment-text</var> e <var>.comment-author</var>.

### Namespaces isolados

Ao batermos o olho no nosso css:

``` css
.comment {}
.comment-text {}
.comment-author {}
```

Sabemos rapida e exatamente quais classes se referem a esse módulo de comentários. O mesmo não seria possível se tivéssemos nomeado assim:

``` css
.comment {}
.text {}
.author {}
```

Afinal, podemos gerar um conflito de namespaces, pois se for uma página com CDs, a classe text poderia também estar identificando qualquer texto na página, e o author poderia ser o compositor.

### Não estilize por filhos

Uma alternativa seria usar classes filhas:

``` css
.comment {}
.comment .text {}
.comment .author {}
```

O problema dessa abordagem é que estamos aumentando a especificidade do seletor, e se precisamos sobrescrever alguma propriedade, tudo começa a ficar muito verboso:

``` css
body.home .comment .author {}
body.price .comment .author {}
```

Além do que, se o .author for uma classe com poucas responsabilidades, podemos usá-la em diversos contextos, apenas somando classes:

``` html
<cite class="comment-author author"></cite>
<p class="music-author author"></p>
```

### Não estilize pelo nome da tag

É comum termos preguiça de declarar classes no HTML, e sair fazendo coisas assim:

``` css
#comments li {}
#comments p {}
#comments cite {}
```

ou então:

``` css
.comment {}
.comment p {}
.comment cite {}
```

O grande problema, é que estamos vinculando o nosso css a um único html, e quando fazermos isso, estamos travando a implementação, o que é ruim, já que se formos apresentar um único comentário, não vamos usar uma LISTA para isso, mas sim uma DIV ou algo do tipo. Além de lento, pois devemos lembrar que os browsers lêem os seletores da direita para a esquerda.

Pense nos layouts que vc já implementou. Tudo começa a ficar mais complexo conforme o site cresce e mais módulos são adicionados, mais áreas precisam ser transpostas de um lugar para outro.. Dei um exemplo simples para ilustrar o conceito.

## Quando usar ID e CLASS

Identifique um elemento com ID quando ele for único em uma página, e não existir nenhuma possibilidade de ter outro igual a ele, como por exemplo o #header e o #footer do site.

Identifique um ou mais elementos com CLASSes quando estiver pensando em módulos reaproveitáveis, em estilos que podem ser somados, como por exemplo:

``` html
<a href="" class="btn btn-hire btn-big">Contratar</a>
```
Estou somando classes para compor o meu elemento. Se eu precisar desse botão em um tamanho menor, apenas troco uma classe no html, ou se eu quiser ele em outra cor, eu apenas adiciono outra class <var>class=&#8221;btn btn-submit btn-medium&#8221;</var>.

## Nomeie pela função

Não escolha nomes que estejam vinculados aos estilos de um seletor. Estilos mudam, assim que layouts se alteram. Escolha nomes que representem o que aquele seletor é na página, ou o que ele faz.

### O que faz ?

Por exemplo, <var>.btn-green</var> e <var>.btn-orange</var> são nomes ruins, pois carregam cores que podem ser alteradas. Melhor seria se esses nomes de classes descrevessem o que aquilo faz, como: <var>.btn-hire</var> e <var>.btn-submit</var>. Assim sabemos que possuimos uma classe que cuida de todos os botões de contratar do site e outra para cuidar dos botões de enviar formulários.

Dessa forma, podemos altera a vontade os estilos sem que o nome do seletor deixe de fazer sentido.

Vale a pena dar uma lida sobre a teoria **OOCSS**.

### O que é ?

Outra má prática, é nomear de acordo com a posição do elemento na página: <var>#column-left</var>, se algum dia essa coluna deixar de ser coluna ou mudar de lado, além de alterarmos alguns estilos no css, teríamos também que alterar no html, pois não faria sentido esse nome.

Nomeie pelo o que o elemento é. Esqueça coisas como posição, cor e tamanho. Se é uma coluna adicional ao conteúdo, não importa onde ela está, é uma #sidebar, #aside.. algo do gênero.

Devemos conseguir distinguir o que um elemento é, sem ler ou ver o conteúdo dele. Apenas batendo o olho na tag e no seletor que ele possui.

## Google Style Guide

Uma indicação de leitura complementar:

[CSS Style Rules](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml#CSS_Style_Rules)

## Conclusão

Para ter um código mais fácil de ler, mais simples de dar manutenção, com seletores mais rápidos, desenvolvido em módulos encaixáveis em qualquer página e independente da marcação html, é que eu nomeio os meus IDs e classes desta maneira.

E ai ? gostou desse estilo ?
