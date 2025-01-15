---
id: 1853
title: CSS reset, usar ou não usar ? Eis a questão !
date: 2012-08-09T07:00:39+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=1853
permalink: /opiniao/css-reset-usar-ou-nao-usar-eis-a-questao/
dsq_thread_id:
  - "2100987622"
categories:
  - Opinião
---
[<img src="/wp-content/uploads/2012/10/guerradosnavegadores.jpeg" alt="" title="guerradosnavegadores" width="558" height="440" class="aligncenter size-full wp-image-2250" srcset="/wp-content/uploads/2012/10/guerradosnavegadores.jpeg 558w, /wp-content/uploads/2012/10/guerradosnavegadores-300x236.jpeg 300w" sizes="(max-width: 558px) 100vw, 558px" />](/wp-content/uploads/2012/10/guerradosnavegadores.jpeg)

Não concordo com a maioria dos css reset! não concordo!

<!--more-->

## CSS Reset ?

Quantos vc conhece ?

normalize.css, do Eric Meyer, do Yahoo!&#8230; e tantos outros.

Exagero, gordura, excesso&#8230; muitos deles &#8220;fazem coisas demais&#8221;.

Eu uso isto aqui:

``` css
* { margin: 0; padding: 0; }
```

E só, praticamente.

Fiz um post com &#8220;o meu css mínimo&#8221;: [Meu CSS mínimo comum a todos os projetos que desenvolvo](https://wbruno.com.br/css/meu-css-minimo-comum-todos-os-projetos-desenvolvo/ "Meu CSS mínimo comum a todos os projetos que desenvolvo").

## A mágica

[<img src="/wp-content/uploads/2012/10/browser-logos-30-293x300.jpeg" alt="" title="browser-logos-30" width="293" height="300" class="alignright size-medium wp-image-2252" srcset="/wp-content/uploads/2012/10/browser-logos-30-293x300.jpeg 293w, /wp-content/uploads/2012/10/browser-logos-30.jpeg 465w" sizes="(max-width: 293px) 100vw, 293px" />](/wp-content/uploads/2012/10/browser-logos-30.jpeg)Não sou contra _o conceito_ de CSS Reset. A idéia é muito boa: nivelar diversas propriedades de diversos elementos, de vários browsers!

Soa como mágica. E talvez até seja mágica, em um certo nível.

Afinal, alguns diferenças entre navegadores &#8220;somem&#8221;. Padronizamos por baixo, margins, paddings.. de fato, **resetamos** os elementos.

Sempre inicie os teus projetos com ao menos, um css reset mínimo. Pode ser o seletor global, retirando margin e padding. Já está ótimo.

## Use o conceito

Crie o teu próprio _css reset_. Não, isso não é &#8220;reinventar a roda&#8221;. Mas sim, ser objetivo.

A minha necessidade é diferente da sua. A do normalize.css, ou do reset.css do Eric Meyer também são diferentes.

Cada projeto é um projeto.

A minha crítica é contra a falta de controle e conhecimento.

Será que o teu site precisa setar display: inline-block para os controles da tag vídeo ?

Tome cuidado para não fazer as coisas sem pensar. Para não sair importando css resets milagrosos, sem nem entender ou ter lido o que eles fazem.

## O seletor global *

Sei que existem críticas sobre o seletor global. Alguns xiitas pregam para não usarmos.

Porém, ainda pior é usar um css reset específico, que declara diversas tags. O reflow é ainda pior.

A briga por especificidade é ainda mais acirrada!

É bem ruim trabalhar em um projeto de código legado, onde vc não pode mudar alguns estilos &#8220;default&#8221;, pois isso quebraria certas áreas que não estão sendo alteradas.

A minha impressão, é que indo direto em cada tag, estamos brigando contra nós mesmos.

O seletor global, colocando margin: 0; faz isso até para tags em que não era necessário, sim realmente.

Mas e daí? Não perdemos performance por isso. Nada significativo realmente ocorre.

E ainda não temos que nos preocupar em &#8220;lembrar de todas as tags&#8221;, de adicionar novas tags que surgirem com o html5&#8230;

### Use css reset

É praticamente o mesmo que venho falando em outros posts aqui no blog. Use, mas saiba o que está usando.

Faça o teu próprio, entenda o que é. Não se prenda, não se limite, nem seja preguiçoso.

**Use!** algum css reset. Se for o seu próprio, ainda melhor.
