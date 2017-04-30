---
id: 2998
title: 'SlideShow JavaScript &#8211; VanillaJS'
date: 2013-05-29T07:00:50+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2998
permalink: /javascript-puro/slideshow-javascript-vanillajs/
dsq_thread_id:
  - "2102782385"
categories:
  - Javascript
tags:
  - oo
  - slideshow
---
[<img src="http://wbruno.com.br/wp-content/uploads/2013/05/slideshow.png" alt="slideshow" width="800" height="456" class="alignleft size-full wp-image-3000" srcset="http://wbruno.com.br/wp-content/uploads/2013/05/slideshow.png 800w, http://wbruno.com.br/wp-content/uploads/2013/05/slideshow-300x171.png 300w" sizes="(max-width: 800px) 100vw, 800px" />](http://wbruno.com.br/wp-content/uploads/2013/05/slideshow.png)

<!--more-->

Estou escrevendo alguns posts sobre Orientação a Objetos em JavaScript:

  1. [Orientação a Objetos em JavaScript &#8211; Objeto Literal](http://wbruno.com.br/javascript-puro/afinal-como-e-orientacao-a-objetos-em-javascript-exemplos/)
  2. [Orientação a Objetos em Javascript – Função Construtora](http://wbruno.com.br/javascript-puro/orientacao-a-objetos-em-javascript-funcao-construtora/)



## Exemplo JavaScript Orientado a Objetos

Para mostrar oo em js nada melhor do que codificarmos componentes do nosso dia-a-dia. 

O projeto de hoje é um **slideshow** daqueles usados em adcasts de sites. Onde uma lista de imagens vai passando com efeito fade, e uma paginação controla o total de fotos, além de pausar a rotação automática, caso o usuário coloque o mouse sob um dos itens.

Já está no github: <a href="https://github.com/wbruno/slideshow" rel="nofollow">https://github.com/wbruno/slideshow</a>, pode fazer um fork lá e sair usando.

## Extensível

Como deixei toda transição de slides por conta do CSS, fazendo o fadeIn pela transição suave da propriedade <var>opacity</var>.

<pre class="css">.adcast-item {
    transition: 2s;
    opacity: 0;
}
#adcast .is-active { opacity: 1; }
</pre>

Este slideshow é completamente extensível. E para transformá-lo em um carousel passando os slides horizontalmente, apenas adiciono as seguintes linhas css:

<pre class="css">#adcast {
	width: 3640px;
	position: absolute;
	top: 0; left: 0;
	transition: 2s;
}
.adcast-item { float: left; position: static; margin: 0; }
#adcast.adcast-item-0 { left: 0; }
#adcast.adcast-item-1 { left: -728px; }
#adcast.adcast-item-2 { left: -1456px; }
#adcast.adcast-item-3 { left: -2184px; }
#adcast.adcast-item-4 { left: -2912px; }
</pre>

## Forma de uso

Basta chamar a função pública <var>adcast.init()</var>, passando como argumento a lista de elementos adcasts, e a lista de elementos pagers.

<pre class="javascript">(function() {
    "use strict";
    /*global document:false */
    var $ = function(selector) {
        return document.querySelectorAll(selector);
    },
        $adcasts = $('.adcast-item'),
        $pagers = $('.pager-item');

    adcast.init({
        adcasts: $adcasts,
        pagers: $pagers
    });

}());
</pre>

Note que acima eu declaro a função <var>$()</var>, para evitar repetir o <var>document.querySelectorAll</var>. Porém, ainda assim é apenas javascript puro. **VanillaJS**.

### Compatível com jQuery

Se você já estiver incorporando o jQuery no seu projeto, esse slideshow também é compatível.

<pre class="javascript">var $adcasts = jQuery('.adcast-item'),
        $pagers = jQuery('.pager-item');

    adcast.init({
        adcasts: $adcasts,
        pagers: $pagers
    });
</pre>

A forma de uso é a mesma, apenas invocando a função <var>adcast.init()</var>. Lá no <a href="https://github.com/wbruno/slideshow" rel="nofollow">github</a>, tem um html de exemplo usando jQuery.

## Demonstração

Live preview!! acessem:

<http://wbruno.github.io/slideshow/>

Já atualizei com todas as transições que fiz. Quer mais alguma ? faz um fork e me manda o pull, ou abre uma issue =)

Gostou ?