---
id: 1725
title: Galerias de imagens com jQuery.lightBox do Leandro Vieira
date: 2012-01-19T02:14:32+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1725
permalink: /jquery/galerias-de-imagens-jquery-lightbox-leandro-vieira/
dsq_thread_id:
  - "2101118876"
categories:
  - jQuery
tags:
  - lightbox
---
Muito bom o plugin jQuery de lightbox do brasileiro Leandro Vieira:

[leandrovieira.com/projects/jquery/lightbox/](http://leandrovieira.com/projects/jquery/lightbox/)

é verdade que o projeto está &#8216;sem atualizações&#8217;, mas também nem precisa.

O plugin cumpre o papel dele, funciona perfeitamente e para um simples modal de imagens funciona muito bem, obrigado.

<!--more-->



Precisei ontem, de uma galeria, onde várias classes seriam as disparadoras. Este html:

``` html
<ul class="fotos">
  <li class="lightbox"><a href="images/banner-primeira-diretoria-eleita-da-abtf.jpg" title="Primeira Diretoria Eleita da ABTF">
    <img src="images/banner-primeira-diretoria-eleita-da-abtf.jpg" alt="" /></a><p>Primeira Diretoria Eleita da ABTF</p>
    <div style="display: none;">
      <a href="images/banner-primeira-diretoria-eleita-da-abtf.jpg" title="Imagem 2">
        <img src="images/banner-primeira-diretoria-eleita-da-abtf.jpg" alt="" /></a>
      <a href="images/banner-primeira-diretoria-eleita-da-abtf.jpg" title="Imagem 3">
        <img src="images/banner-primeira-diretoria-eleita-da-abtf.jpg" alt="" /></a>
      <a href="images/banner-primeira-diretoria-eleita-da-abtf.jpg" title="Imagem 4">
        <img src="images/banner-primeira-diretoria-eleita-da-abtf.jpg" alt="" /></a>
    </div><!-- /none -->
  </li>
  <li class="lightbox"><a href="images/banner-presidentes-da-abtf.jpg" title="Presidentes da ABTF">
    <img src="images/banner-presidentes-da-abtf.jpg" alt="" /></a><p>Presidentes da ABTF</p>
    <div style="display: none;">
      <a href="images/banner-presidentes-da-abtf.jpg" title="Imagem 2">
        <img src="images/banner-presidentes-da-abtf.jpg" alt="" /></a>
      <a href="images/banner-presidentes-da-abtf.jpg" title="Imagem 3">
        <img src="images/banner-presidentes-da-abtf.jpg" alt="" /></a>
    </div><!-- /none -->
  </li>
  <li class="lightbox last"><a href="images/banner-diretoria-atual.jpg" title="Diretoria Atual">
    <img src="images/banner-diretoria-atual.jpg" alt="" /></a><p>Diretoria Atual</p>
    <div style="display: none;">
      <a href="images/banner-diretoria-atual.jpg" title="Imagem 2">
        <img src="images/banner-diretoria-atual.jpg" alt="" /></a>
    </div><!-- /none -->
  </li>
</ul><!-- /fotos -->
```

Não achei nenhuma configuração de galeria no plugin.

Então ao disparar da maneira básica:

``` js
jQuery(document).ready(function(){
    jQuery('.lightbox a').lightBox({
      txtImage: 'Imagem',
      txtOf: 'de'
    });
  });
```

O que o plugin fez, foi juntar todas as imagens numa única galeria de 9 imagens no total.

Mas na verdade, eu queria que cada LI, fosse um album separado dos demais.

Sendo a primeira galeria, com 4 imagens, a segunda com 3, e a ultima com 2 imagens.

Bom, eu poderia muito bem trocar de plugin, usar um fancybox, ou sei lá.. porém apenas pelo desafio, resolvi de uma maneira bem simples essa situação de: criar galerias diferentes para uma mesma classe html, com o plugin jQuery.lightBox:

``` js
jQuery(document).ready(function(){
    jQuery('.lightbox').each(function(){
      $( this ).find('a').lightBox({
        txtImage: 'Imagem',
        txtOf: 'de'
      });
    });
  });
```

Dessa forma, o plugin vai rodar um grupo(cada li), um de cada vez, e vai separou como eu queria.

é isso. =)
