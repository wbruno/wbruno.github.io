---
id: 2849
title: Parem de usar ajax! Eu imploro!
date: 2012-11-22T10:44:25+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2849
permalink: /opiniao/parem-de-usar-ajax-eu-imploro/
dsq_thread_id:
  - "2102232625"
categories:
  - Opinião
---
Parem de usar! parem agora. Pelo menos da forma com que estou vendo que estão usando ultimamente.

Cuidado pessoal! Antes de sair enfiando ajax em tudo, pelo menos pense antes.

<!--more-->



Era preciso ? realmente melhorei a experiência do usuário ?

Ou só achei legal a tecnologia, e resolvi inchar o carregamento da minha aplicação ou site, com trocentas linhas de código javascript para fazer algo desnecessário ?

Eu já lhes disse para [não usar jquery](https://wbruno.com.br/opiniao/nao-jquery-nao-aprenda-qualquer-framework-antes-de/), e agora volto para dizer para vocês não usarem ajax!

## Eu uso

Eu usei ajax essa semana. No meu formulário de contato, utilizei da API html5 para pegar a localização do usuário, e com ajax, vou no servidor consulto a posição de coordenadas, e devolvo o campo CEP preenchido, sem que o cliente tivesse que digitar nada. O único trabalho do usuário foi clicar num botão.

E adivinhem, eu não usei jQuery. Fiz o ajax no js puro. 35 linhas para a lib ajax, e mais umas 10 para a chamada da minha função. Pronto, problema resolvido e usuário feliz.

## O que é ajax?

Hein? você sabe [o que é ajax](https://wbruno.com.br/ajax/o-que-e-ajax-e-o-que-nao-e/)?

Se não sabe, ou não tem muita certeza.. então você não deveria estar usando. Pare um pouquinho e leia a definição da tecnologia, os princípios dela.

Eu tenho medo qndo vejo o pessoal usando algo que não dominam. É como me colocar para pilotar um avião ou um helicóptero. Haverá um desastre, com certeza.

## Carregar páginas com ajax

Eu já mostrei diversas formas de [carregar páginas com ajax](https://wbruno.com.br/ajax/navegacao-sem-refresh-–-carregando-conteudo-ajax-em-div-2/), e já mostrei até [como usar um lightbox depois de carregar uma página com ajax](https://wbruno.com.br/ajax/usando-lightbox-em-pagina-carregada-ajax/), pois se não fosse essa artimanha, ele não funcionaria.

A galera carrega páginas inteiras com ajax, apenas por que acha bonito. &#8220;Não ter refresh&#8221;.

Mas será que precisamos realmente disso ? Será que a percepção do usuário foi realmente legal ?

E se gastássemos esse tempo que desperdiçamos fazendo o menu em ajax, fazendo que o site ficasse mais leve ? Minificando css, js, ativando gzip(mod_deflate), ativando eTags, compactando as imagens, fazendo sprites, melhorando o html dando mais semântica, colocando dados estruturados, revisando os textos para levar mais informação relevante, repensando na usabilidade, medindo se estamos acessíveis&#8230;

Ufa! enfim.. viram existem muitas outras coisas muito mais importantes e que farão muito mais diferença para o nosso cliente, do que &#8220;a div carregar sem refresh&#8221;.

## Onde vc usa ajax?

Será que não dava para ser mais inteligente ? e já carregar um arquivo .js, com o json dos dados que vc está buscando com ajax, logo no load da página ?

Esse arquivo entrará em cache, e se você tiver investido o seu tempo configurando corretamente o seu servidor e a sua aplicação, a experiência do usuário será muito melhor do que se você buscasse esses dados no onclick dele, ou no onblur, onkeyup de um certo campo.

## Precisava de ajax ?

E se fosse apenas um texto oculto ? qndo o cara clicar vc dá um display: block; e pronto!

Não, isso não é feio! Certamente será mais rápido e consumirá menos recursos do servidor.

Estou falando isso, pq já vi no fórum um cara que carregava tooltips com ajax.

Cada vez que o usuário fazia um mouseover em dadas palavras, era disparado um ajax, que não cacheava o dado, e trazia o conteúdo do tooltip lá do servidor.

## São detalhes

Estou aqui falando de detalhes. Lógico que existem boas aplicações de ajax.

E não quero que vc onere o primeiro load do site, trazendo toneladas de dados que talvez não serão usados.

O que eu realmente quero, é colocar uma pulga nas nossas orelhas, para que pelo menos pensamos antes de sair fazendo.
