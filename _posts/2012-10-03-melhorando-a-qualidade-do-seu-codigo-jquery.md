---
id: 2791
title: Melhorando a qualidade do seu código jQuery
date: 2012-10-03T11:12:42+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2791
permalink: /jquery/melhorando-a-qualidade-do-seu-codigo-jquery/
dsq_thread_id:
  - "2100963315"
categories:
  - jQuery
tags:
  - boas práticas
---
jQuery é bacana. Escreva menos, faça mais.

<p style="text-align: center;">
  <a href="/wp-content/uploads/2012/10/OQAAAI1PPrJY0nBALB7mkvju3mkQXqLmzMhxEjeb4gp8aujEUQcLfLyy-Sn4gZdkAas6-k8eYbQlGDE-GCjKfF5gIrUA15jOjFfLRv77VBd5t-WfZURdP9V3PdmT.preview.png"><img class="size-full wp-image-2799 aligncenter" title="OQAAAI1PPrJY0nBALB7mkvju3mkQXqLmzMhxEjeb4gp8aujEUQcLfLyy-Sn4gZdkAas6-k8eYbQlGDE-GCjKfF5gIrUA15jOjFfLRv77VBd5t-WfZURdP9V3PdmT.preview" alt="" src="/wp-content/uploads/2012/10/OQAAAI1PPrJY0nBALB7mkvju3mkQXqLmzMhxEjeb4gp8aujEUQcLfLyy-Sn4gZdkAas6-k8eYbQlGDE-GCjKfF5gIrUA15jOjFfLRv77VBd5t-WfZURdP9V3PdmT.preview.png" width="700" height="172" srcset="/wp-content/uploads/2012/10/OQAAAI1PPrJY0nBALB7mkvju3mkQXqLmzMhxEjeb4gp8aujEUQcLfLyy-Sn4gZdkAas6-k8eYbQlGDE-GCjKfF5gIrUA15jOjFfLRv77VBd5t-WfZURdP9V3PdmT.preview.png 700w, /wp-content/uploads/2012/10/OQAAAI1PPrJY0nBALB7mkvju3mkQXqLmzMhxEjeb4gp8aujEUQcLfLyy-Sn4gZdkAas6-k8eYbQlGDE-GCjKfF5gIrUA15jOjFfLRv77VBd5t-WfZURdP9V3PdmT.preview-300x73.png 300w" sizes="(max-width: 700px) 100vw, 700px" /></a>
</p>

&nbsp;

Porém muitos dos desenvolvedores de hoje em dia, não levaram a sério a parte do _&#8220;escreva menos&#8221;_, e continuam escrevendo **muito** e de forma desordenada.

Tudo bem, então aqui vai algumas dicas para melhorar a qualidade dos códigos jQuery.

<!--more-->

## jsHint

jQuery é apenas uma lib javascript. Logo, todas as boas práticas que existem para javascript, também existem para jQuery. Começe passando o teu código pelo jsHint:

<a href="http://www.jshint.com/" rel="external">http://www.jshint.com/</a>

Dentre outras coisas, o jshint, vai verificar se vc usou um switch na hora errada, se declarou uma variavel que não está sendo usada..

## Outras coisas, que nem o jshint conseguiria te dizer

Agora começa o meu post de verdade.

## Prefira sempre usar jQuery no lugar de $

Eu pessoalmente, considero mais legível. Mas além disso, também estamos evitando de uma maneira muito simples aquele velho problema do conflito com outras libs que usam o apelido $.

Seria:

<pre class="javascript">jQuery(document).ready(function() {});
```

no lugar de

<pre class="javascript">$(document).ready(function() {});
```

## Não procure um mesmo elemento várias vezes no DOM

Coisas como:

<pre class="javascript">jQuery(this).parent('dl').find('dd').eq(0).addClass('active');
jQuery(this).parent('dl').find('dt').text('Ativo');
```

Poderiam ser simplificadas para:

<pre class="javascript">var $this = jQuery(this),
$dl = $this.parent('dl');

$dl.find('dd').eq(0).addClass('active');
$dl.find('dt').text('Ativo');
```

Note que se formos usar o DD e esse DT outras vezes nesse escopo, então vale apena guardar uma variavel que aponte para eles também.

Isso também vai melhorar a performance do teu script.

## Convencione os nomes das variaveis

É bacana olhar para uma variavel e entender logo de cara de onde ela veio, e qual o valor dela.

Eu estou adotando usar $ antes de começar uma variavel que aponte para um objeto jQuery. Assim como o **$this**. E deixo para as variaveis &#8220;normais&#8221;(arrays, inteiros e strings), uma notação sem o símbolo $.

Dessa forma, qndo bato o olho no meu código jQuery, sei que todas as variaveis com $ no nome, são objetos jQuery.

<pre class="javascript">var $this = jQuery(this),
$dl = $this.parent('dl'),
i = 0,
str = '';
```

## Faça bom uso dos arrays e objetos

Uma cadeia de if/elses ou switchs podem ser evitados se vc souber usar arrays e objetos javascript corretamente.

Como por exemplo essa lista de valores:

<pre class="javascript">var values = [];

  values[1] = { '1': '1,90', '6': '1,41', '12': '1,01' };
  values[2] = { '1': '2,90', '6': '2,91', '12': '2,01' };
  values[3] = { '1': '3,90', '6': '3,41', '12': '3,01' };
  values[4] = { '1': '4,90', '6': '4,40', '12': '4,01' };
```

Tenho 4 &#8220;planos&#8221; cada um com 3 opções de valores: planos mensais, semestrais e anuais. Se eu fosse fazer isso com if ou switch, o código bem ruim.

## Separe comportamentos

Essa é uma coisa básica de programação. Divida um procedimento em várias rotinas menores, e escreva pequenas funções que resolvam uma parte pequena do problema. Juntando todas, vc terá resolvido tudo.

## Leia este post:

[Aprendi jQuery e agora?](http://wbruno.com.br/2011/07/18/vixi-aprendi-jquery-mas-agora/)

E para terminar:

## Faça bem o básico

É básico indentar corretamente, comentar qndo necessário, e documentar.

Estas são algumas pequenas boas práticas que vão fazer uma boa diferença nos teus scripts.
