---
id: 2173
title: 'Semântica html5 &#8211; Comece agora mesmo! Use!'
date: 2012-08-14T07:00:52+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2173
permalink: /html/semantica-html5/
dsq_thread_id:
  - "2100762248"
categories:
  - HTML
tags:
  - semântica
---
Vou lhes dar um ótimo motivo para já começar a usar html5 hoje nos teus projetos: **semântica**.

Os elementos <var><header></var>, <var><footer></var>, <var><article></var>, <var><aside></var>, <var><section></var> e <var><nav></var> são nivel de bloco tão bons quanto o elemento <var><div></var>. Para o usuário comum e para nós desenvolvedores não haverá nenhuma mudança perceptível(do ponto de vista visual).

E nem deveria! Desde o início, a linguagem nasceu com o intuito de marcar o conteúdo. Isso por si só, já justifica marcarmos mais adequadamente nossos conteúdos, usando as novas tags da html5.

<!--more-->



[<img src="/wp-content/uploads/2012/08/HTML5_Logo_512-300x300.png" alt="" title="HTML5_Logo_512" width="300" height="300" class="alignleft size-medium wp-image-2304" srcset="/wp-content/uploads/2012/08/HTML5_Logo_512-300x300.png 300w, /wp-content/uploads/2012/08/HTML5_Logo_512-150x150.png 150w, /wp-content/uploads/2012/08/HTML5_Logo_512.png 512w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2012/08/HTML5_Logo_512.png)Ok, ok.. essa nova versão da linguagem html não trouxe apenas novas tags. Vieram também <a href="http://tableless.com.br/entendendo-quais-apis-realmente-fazem-parte-do-html5/" rel="external" title="APIs html5">algumas apis.</a>. Mas este nem é o meu foco neste post, quero falar somente da marcação.

Todas as novidades são ótimas, e muito úteis. Mas se você ainda não usa html5 nos teus projetos, comece agora mesmo! E comece pela **semântica**.

A adoção de uma nova tecnologia demanda esforço, estudo, testes.. enfim: tempo.

Comece aos poucos.

Adote as tags semânticas. Isso já é um grande avanço.

O Doctype já é bem mais simples e possível de decorar, do que do xhtml que estamos acostumados.

## DOCTYPE html5

``` html
<!DOCTYPE html>```

Isto no lugar do nosso velho amigo:

``` html
<!!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">```

## Semântica html5

Existem as tags <var>header</var> e <var>footer</var>. Intuitivas, não ?

Chega de:

``` html
<div id="header">```

e

``` html
<div id="footer">```

agora podemos informar para os diversos meios de acesso que consomem as informações das nossas páginas, com essas 2 tags:

``` html
<header id="header">```

e

``` html
<footer id="footer">```

Podemos ter várias tags <var><header</var> num mesmo documento.

### O elemento header

Por exemplo, <var><header id=&#8221;header&#8221;></var>, pode marcar o cabeçalho do nosso template. Aquela parte que se mantém fixa mesmo com a mudança de páginas. Geralmente, é aquela área que contém o logotipo e a navegação principal do site.

E alguns outros elementos <var><header</var> que marquem o cabeçalho do nosso conteúdo.

Pense numa listagem de posts de um blog. Cada post possui uma data, um título, autor, categoria em que foi publicado&#8230; isso tudo é informação de cabeçalho daquele post, então podemos sim, ter várias tags header nesse documento.

Mas não uma tag header dentro da outra. o/

### O elemento footer

Nessa mesma idéia, o elemento <var><footer id=&#8221;footer&#8221;></var> geralmente contém aquele copyright &copy; de direitos autorais&#8230;

E quando visualizamos um post específico de um blog, aquela área no final do post, que contém os artigos relacionados, os botões das redes sociais&#8230; são o footer deste conteúdo.

### O elemento article

Eu falei um pouco sobre &#8220;conteúdo principal&#8221;. Entenda isso como aquele conteúdo, que pode ser apresentado &#8220;sozinho&#8221;. A informação que faz sentido por si só(sem o template, por exemplo).

Isto significa que podemos ter vários elementos <var>article</var> num mesmo documento.

Porém, vamos simplificar por enquanto: pensemos numa simples estrutura:

[<img src="/wp-content/uploads/2012/08/estrutura-200x300.jpg" alt="" title="estrutura" width="200" height="300" class="aligncenter size-medium wp-image-2363" srcset="/wp-content/uploads/2012/08/estrutura-200x300.jpg 200w, /wp-content/uploads/2012/08/estrutura.jpg 400w" sizes="(max-width: 200px) 100vw, 200px" />](/wp-content/uploads/2012/08/estrutura.jpg)

Mesmo sem os atributos IDs, conseguimos facilmente perceber que <var>header#content-header</var> pertence ao article <var>#content</var>, pois é filho deste elemento. Com essa melhora na semântica, ajudaremos os meios de acesso(tais como os robôs de busca), a fazer uma web melhor. Com mais significado.

### O elemento section

Esta tag identifica áreas de conteúdo, para ser mais exato: seções de conteúdo.

Também podemos ter vários desses elementos no nosso documento. Depende da necessidade do conteúdo que estamos apresentando.

Imagine a home de um site, com aquelas chamadas para páginas internas. Essa área é uma <var><section></var> dessa home. Um pedaço do conteúdo.

## Semântica dos elementos

Entenda que section e article **não são** _as novas DIVs_. Ainda podemos/devemos usar <var>div</var> nas nossas páginas.

As tags div e span, marcam conteúdos que não possuem nenhuma semântica. Tais como aquele container que serve somente para &#8220;centralizar&#8221; o site. Este é um bom uso da tag div, mesmo nos tempos de html5.

### O elemento nav e o elemento aside

Marcamos com <var>nav</var>, a **nav**egação do site. Os links pelos quais os visitantes vão alcançar nossos conteúdos. Até mesmo um formulário pode fazer parte da nossa navegação.

Marcamos com <var>aside</var>, aquele conteúdo relacionado ao conteúdo principal do site. Uma sidebar de links relacionados, e até mesmo toda a área de comentários de um post de um blog.

São conteúdos que possuem uma relação direta ao conteúdo principal.

## Semântica independe de posição

O <var>aside</var> não é necessariamente a sidebar do lado direito. Não se prenda a isso.

Por exemplo, o <var>header</var> de um site que vi recentemente ficava disposto como uma coluna na esquerda do site, pois era ali que continham as informações de cabeçalho, tais como o logotipo e a <var>nav</var> do site.

Podemos ter <var>section</var>s dentro do footer, do header, do article, dentro de outro section&#8230;

Devemos sempre nos lembrar que a disposição é responsabilidade exclusiva do **css**.

A semântica nos diz apenas o que cada elemento representa, qual é a informação que aquele conteúdo possui.

[Olhe para o teu conteúdo, e deixe que ele te responda o que ele é.](http://wbruno.com.br/2011/05/17/nem-so-de-div-vive-um-desenvolvedor-frontend/ "HTML Semântico")
