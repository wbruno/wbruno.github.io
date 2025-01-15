---
id: 2950
title: 'Tableless: Como posicionar elementos de um layout - Recorte CSS'
date: 2013-05-10T11:42:41+00:00
author: William Bruno
layout: post
guid: https://wbruno.com.br/?p=2950
permalink: /css/tableless-como-posicionar-elementos-de-um-layout-recorte-css/
dsq_thread_id:
  - "2116233132"
categories:
  - CSS
tags:
  - tableless
---
Sim, um tema básico aqui no blog. Ou talvez nem tanto.

Diariamente vejo diversos desenvolvedores se enrolando com essa questão: &#8220;Como estruturar um layout css?&#8221;, ou &#8220;Por que tableless é tão difícil?&#8221;, e &#8220;Por que no Chrome/Internet Explorer, não fica igual?&#8221;

<!--more-->



Impossível escrever uma receita de bolo que sirva para todos os layouts, que resolva todos os efeitos visuais..

Depende de cada projeto, a variação do design faz que tenhamos que analisar cada um individualmente, mas ainda assim, vou tentar escrever algumas dicas que de forma geral podem te ajudar a ter menos problemas ao fazer um recorte tableless.

## CSS Reset/Normalize

Só comece a escrever o teu css, depois te ter algum css reset declarado. Nem que seja um:

``` css
* { margin: 0; padding: 0; border: none; }
```

## DOCTYPE

Escolha algum. Eu recomendo o doctype html5, ou o strict xhtml.

## Position

Evite usar position. Muitos se perdem e saem fazendo tudo, absolutamente tudo com position: absolute;

Pare já com isso. Não use. Posicione os &#8220;grandes blocos&#8221;, a estrutura do layout, ou seja, topo, conteudo , colunas e rodapé, com float, margin e clear.

Apenas isso. Evite também valores muito altos de margins e paddings.

## Semântica

Seja semântico. Se você tem um texto, use a tag <var><p></var>, se tem uma imagem que passa informação, use <var><img /></var> e assim por diante.

Deixe que o conteúdo lhe diga qual tag vc deve usar.

## Use poucos elementos

Evite desperdiçar marcação html. Não há motivo para por exemplo, usar uma tag <var><figure></var> em um banner, que não possui nenhum outro conteudo relacionado na pagina, e não possui uma legenda. Use o bom senso.

8

## Não chute

Sei que nem sempre sabemos como chegar a tal feito, mas não fique chutando regras css e elementos html. Limpe eles depois. Não deixe regras css inúteis nos teus elementos.

## Leia estes posts

  1. [Nem só de <div> vive um desenvolvedor FrontEnd](https://wbruno.com.br/opiniao/nem-so-de-div-vive-um-desenvolvedor-frontend/)
  2. [Como iniciar um recorte Tableless – comece !](https://wbruno.com.br/css/como-iniciar-um-recorte-tableless-comece/)
  3. [Como iniciar um recorte tableless – ensinando a pensar](https://wbruno.com.br/css/como-iniciar-um-recorte-tableless-ensinando-pensar/)
  4. [O elemento HTML body nos nossos sites, como melhor aproveitá-lo.](https://wbruno.com.br/html/elemento-body-nos-nossos-sites-como-melhor-aproveita-lo/)
  5. [Mau cheiro em código css – Como sentir](https://wbruno.com.br/css/mau-cheiro-em-codigo-css-como-sentir/)
  6. [Outros maus cheiros em código css – Como sentir](https://wbruno.com.br/css/como-sentir-mau-cheiro-em-codigo-css/)
  7. [Separação de camadas no FrontEnd](https://wbruno.com.br/css/separacao-de-camadas-no-frontend/)
  8. [Otimizações para websites não óbvias](https://wbruno.com.br/css/otimizacoes-para-websites-nao-obvias/)
  9. [Meu boilerplate de projetos de sites html5 e mobile](https://wbruno.com.br/html/meu-boilerplate-de-projetos-de-sites-html5-e-mobile/)
 10. [Semântica html5 – Comece agora mesmo! Use!](https://wbruno.com.br/html/semantica-html5/)
 11. [A semântica da tag <br /> – Simplesmente não use !](https://wbruno.com.br/html/semantica-da-tag-br/)
 12. [Devemos saber desenvolver para internet explorer [ie]!](https://wbruno.com.br/css/devemos-saber-desenvolver-para-internet-explorer-ie/)

Depois de ler esse arsenal de posts, espero ter aberto a sua mente para que você comece a criticar a forma com que vc vinha fazendo sites até hoje, e passe para o próximo nível, desenvolvendo em menos tempo, e com muito mais qualidade.

=)
