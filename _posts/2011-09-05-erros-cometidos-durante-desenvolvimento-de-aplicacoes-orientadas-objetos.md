---
id: 1372
title: Erros cometidos durante desenvolvimento de aplicações orientadas a objetos.
date: 2011-09-05T09:54:41+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1372
permalink: /opiniao/erros-cometidos-durante-desenvolvimento-de-aplicacoes-orientadas-objetos/
categories:
  - Opinião
tags:
  - oo
---
Este post, será um breve relato do que aprendi e observei durante a minha experiência com desenvolvimento web.
  
<!--more-->

## Não (saber|utilizar) OO

Escrever um aplicação com o paradgma de orientação a objetos, não é simplesmente sair criando classes.
  
E colocar em métodos todo aquele teu código estruturado, colocando um public ou private, na frente das tuas antigas funções.

OO não é isso. Para fazer corretamente, vc deve enchergar os objetos, e as relações deles. Como eles devem se comunicar, delegando responsabilidades.

## Misturar camadas

É muito fácil querer resolver tudo de uma vez, mas ai nos encontramos misturando as coisas. Colocando partes do controller nos models..
  
OO e MVC são duas coisas distintas, mas que caminham juntas. Escrever em camadas, é uma abstração maior, para fazermos além, de converter nosso sistema em objetos.

Na minha opinião server-side, não deve, ou deveria gerar o mínimo de HTML possível. Quando vejo classes que encapsulam toneladas de código HTML, ou outras destinadas a formar tags, ouço uma voz: &#8220;isso está misturado&#8221;. Estão praticando um acoplamento das classes com aquele HTML.
  
Se eu tiver um sistema administrativo, e precisar trocar o layout dele, não quero ter que mecher nas classes responsáveis pelas regras de negócio, quero ver o mínimo de server-side, e ter um arquivo com html simples e puro.

Trabalhando em equipe, onde temos um FrontEnd, que nem sabe BackEnd, não dá para pedir pra esse cara mudar o HTML lá dentro da classe. Ou então esperar que ele aprenda a instanciar classes para gerar o HTML dos formulários..

Sério, acho muito estranho essa idéia de classes geradoras de TAGs, ou que encapsulam quantidades absurdas de HTML.
  
A princípio, acho que BackEnd, deve retornar dados. E então, só no template, é que esses dados serão divididos e organizados na marcação.

## Superestimar a aplicação

Faça o simples. Menos funcionalidades, mais objetividade. Meus sistemas nunca mudarão de banco de dados. Isso é um requisito.
  
Aplicações com poucos acessos, não precisam prever uma mudança de MySQL para Oracle. Não vou usar a lib PDO do php, para abstrair acesso aos dados, sendo que a extensão mysqli é muito boa, rápida, e resolve o que preciso.

## Não subestime

Devo deixar um mínimo pronto para expansão. O importante não é apenas resolver, mas garantir que o sistema cresça. Uma modelagem correta dos dados, uma estratégia que prevê mais recursos, deixando a estrutura robusta, pode poupar muito tempo no futuro. Note, não estou implementando tudo, estou apenas deixando preparado. 

O que eu consigo lembrar por enqnto é isso. Você tem mais alguma dica ? compartilhe.