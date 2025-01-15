---
id: 2919
title: Otimizações para websites não óbvias
date: 2013-03-08T16:54:16+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=2919
permalink: /css/otimizacoes-para-websites-nao-obvias/
dsq_thread_id:
  - "2103806763"
categories:
  - CSS
  - HTML
tags:
  - boas práticas
---
A minha idéia nesse post, é apenas fazer uma listagem de otimizações em sites não óbvias. Ir um pouco além do que vemos por ai, e fazer um apanhado de tudo.

Bem rápido, por isso que vai ser em formato de lista.

## Imagens

<ul class="bullet">
  <li>
    Usar sprites
  </li>
  <li>
    Passar imagens pelo SmushIt
  </li>
  <li>
    Declarar as dimensões das imagens no html
  </li>
  <li>
    Usar imagens em base 64
  </li>
  <li>
    Preferir extesões .jpg e .gif(no lugar de png)
  </li>
  <li>
    Usar patterns pequenos nos repeats
  </li>
  <li>
    Usar backgrounds otimizados com media queries
  </li>
</ul>

## Evitar Imagens

<ul class="bullet">
  <li>
    Usar códigos para degradês e bordas redondas
  </li>
</ul>

## Evitar

<ul class="bullet">
  <li>
    Evitar requisições inválidas
  </li>
</ul>

## JavaScript

<ul class="bullet">
  <li>
    Arquivos js no final da página
  </li>
  <li>
    Carregar js de modo assincrono
  </li>
  <li>
    Cache de variaveis
  </li>
  <li>
    Carregar youtube, twitter e facebook via ajax
  </li>
  <li>
    Carregar modais e tooltips via ajax
  </li>
</ul>

## CSS

<ul class="bullet">
  <li>
    Evitar regras css com virgulas nos seletores
  </li>
</ul>

## Talvez

<ul class="bullet">
  <li>
    Talvez até simplificar o layout, removendo alguma sombra que não cause muita diferença visual, mas estava pesando na implementação
  </li>
  <li>
    Evitar jQuery e plugins de terceiros
  </li>
</ul>

## Ferramentas

<ul class="bullet">
  <li>
    Usar ySlow
  </li>
  <li>
    Usar PageSpeed
  </li>
  <li>
    Merge e minify de css, js e html
  </li>
  <li>
    Validar w3c html, css
  </li>
  <li>
    Validar link checker
  </li>
</ul>

## Servidor

<ul class="bullet">
  <li>
    Usar mod_deflate e mod_expires
  </li>
</ul>
