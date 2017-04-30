---
id: 3161
title: 'Review Livro: JavaScript de Alto Desempenho'
date: 2014-02-09T09:26:47+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3161
permalink: /livro/review-livro-javascript-de-alto-desempenho/
categories:
  - Livro
tags:
  - programação
  - review
---
<img src="/wp-content/uploads/2014/02/javascript-de-alto-desempenho_MLB-O-226180730_6939.jpg" alt="javascript-de-alto-desempenho_MLB-O-226180730_6939" width="292" height="405" class="aligncenter size-full wp-image-3162" />

Livro publicado pela Novatec, escrito por Nicholas C Zakas, com participações de diversos outros autores.

## Opinião Geral

O livro aborda de maneira bem fundamentada e profunda tópicos importantíssimos para construirmos aplicações mais rápidas e responsivas.

O livro diz que é dirigido a desenvolvedores que procuram uma compreensão intermediária e avançada de javascript e que procuram formas de melhorar o desempenho, ou seja, todos nós. **Leitura obrigatória para desenvolvedores web**.

Ainda no prefácio, conta a evolução ao longo da história, além de falar um pouco sobre garbage collector (conceito que todos os programadores deveriam conhecer).

<!--more-->

## Capítulo 1 &#8211; Carregamento e execução

Curto, explica como funciona o carregamento de recursos javascript, e como a natureza bloqueadora da tag script age. Apresenta formas de melhorar, desde colocar as tags scripts no final do documento, até carregar scripts assincronamente, criando a tag script com js, ou buscando com ajax o arquivo .js.

## Capítulo 2 &#8211; Acesso aos dados

Explica sobre gerenciamento de escopo e como o acesso aos dados produz um impacto na performance.

Um ponto muito bacana desse livro, é que no final de cada capítulo, existe uma sessão chamada **Resumo**, onde através de uma lista de tópicos, é apresentado de forma rápida e resumida tudo o que foi visto.

Funciona como link mental, e posterior remember para consulta, após você terminar a primeira leitura do livro.

## Capítulo 3 &#8211; Criação de scrips DOM

Explica o que é e para o que serve o DOM, além de apresentar gráficos de comparação entre as formas de inserir elementos no DOM. Um lugar bacana para testar snippets de código, como os propostos no livro, é o <a href="http://jsperf.com/" rel="nofollow">http://jsperf.com/</a>.

O DOM é lento, e hoje em dia, é algo básico se preocupar com a performance de quando vamos manipulá-lo.

## Capítulo 4 &#8211; Algorítmos e controle de fluxo

Evitar Memory Leak deve ser uma preocupação constante, e será com pequenas otimizações, que deixaremos o todo mais rápido. Capítulo muito bom também e obrigatório ler mais de uma vez.

## Capítulo 5 &#8211; Strings e expressões regulares

Capítulo bem avançado. Confesso que otimizar strings e expressões regulares, é algo que ainda não havia passado pela minha cabeça antes de ler esse livro. Vai servir como base de consulta, até nos acostumarmos a fazer isso no dia a dia.

## Capítulo 6 &#8211; Interfaces responsivas

Por que e como fazer as interfaces responderem melhor as ações de usuário, e como usar WebWorkers para dividir tarefas.

## Capítulo 7 &#8211; Ajax

Apesar de parecer trivial, não é. E desde a forma com que vc envia até como recebe os dados de um ajax, faz diferença na performance. E você ainda pode usar ajax em certos pontos da aplicação, com o único intuito de melhorar a experiência dela.

## Capítulo 8 &#8211; Práticas de programação

Esse capítulo é bem específico da linguagem javascript, e mostra algumas práticas de programação como evitar dupla avaliação, utilização de literais e DRY.

## Capítulo 9 &#8211; Criação e disponibilização de aplicações JavaScript de alto desempenho

Já focado mais no deploy da aplicação, mostra alguns tópicos sobre otimização de carregamento, cache e minificação.

## Capítulo 10 &#8211; Ferramentas

Exatamente o que vc acha que é. Apresenta o Firebug, o WebInspector, PageSpeed, YSlow e finaliza esse ótimo livro.
