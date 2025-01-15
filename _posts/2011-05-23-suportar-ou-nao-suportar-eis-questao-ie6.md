---
id: 985
title: 'Suportar ou não suportar ? Eis a questão [ ie6- ]'
date: 2011-05-23T07:00:51+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=985
permalink: /opiniao/suportar-ou-nao-suportar-eis-questao-ie6/
categories:
  - Opinião
tags:
  - html5
---
[<img class="alignright size-thumbnail wp-image-986" title="Internet_Explorer_logo_old" src="/wp-content/uploads/2011/05/Internet_Explorer_logo_old-150x150.png" alt="" width="150" height="150" />](/wp-content/uploads/2011/05/Internet_Explorer_logo_old.png)Acredito que quem realmente deve _decidir_ se o site ou aplicação web&#8230; deve ou não ser compatível com o Internet Explorer 6, ou qualquer outro, é o cliente final para o qual estamos trabalhando.

Nós desenvolvedores, afinal de contas, temos que satisfazer as demandas de quem nos contratou. O sucesso da loja virtual, da vitrine de produtos, do portal de notícias, do blog, do site institucional, do sistema para uso interno, externo, whatever&#8230; depende em partes, diretamente do que fizermos. O sucesso deles, é uma alavanca para o nosso próprio. Afinal, se o cliente tiver resultados, mais trabalhos e indicações receberemos.

<!--more-->



Não queremos que nosso cliente deixe de vender, ou que os **clientes de nossos clientes** não usem a interface que desenvolvemos, por que não fomos atenciosos o suficiente, para deixar um mínimo de usabilidade e acessibilidade disponíveis para plataformas mais &#8216;antigas&#8217;, porém ainda utilizadas.

[<img class="alignleft size-medium wp-image-998" title="top-best-browsers" src="/wp-content/uploads/2011/05/top-best-browsers-300x191.jpg" alt="" width="300" height="191" srcset="/wp-content/uploads/2011/05/top-best-browsers-300x191.jpg 300w, /wp-content/uploads/2011/05/top-best-browsers.jpg 510w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2011/05/top-best-browsers.jpg)No dia a dia, temos que nos preocupar com bugs, e diferentes interpretações entre Firefox, Chrome, Internet Explorer, Opera..

Apesar de serem os mais utilizados e conhecidos, não existem apenas esses. Alguns frontends, esquecem ou não sabem de todos os outros browsers, ou nunca repararam que existem diferenças entre o Sistema Operacional também. O resultado do Firefox no Windows, é diferente do resultado da mesma versão do Firefox no Mac por exemplo.

O ponto mais sensível é a fonte. O tamanho, o espaçamento, o alising variam entre SOs. Quanto a diferenças propriamente ditas de renderização, basta que nos preocupemos no máximo com os motores [ **Gecko, Presto, Webkit, Trident..** ], e não tanto com cada uma das distrubuições(salvos bugs entre versões, é aqui que o IE é o maior vilão) que rodam sob um mesmo motor. Quero dizer que se um certo posicionamento falhar no Chrome, provavelmente você vai notar o mesmo comportamento no Safari, entendeu ?

O meu Analytics, indica que 12,55% dos meus visitantes usam Internet Explorer(terceiro lugar, sendo Chrome segundo e Firefox o primeiro, com praticamente metade da massa). Desses, apenas 2,71% usam a versão 6 dele (durante todo o período de monitoração, desde que instalei o ga). Esse número representa apenas que **o meu público** se comporta dessa forma.

Hoje em dia, é simples quantificar, e então daí decidir se _vale ou não apena_ investirmos tempo de implementação, para que a aplicação não deixe de atender os visitantes|usuários. O <u>erro</u>, que na minha opinião não devemos cometer, é:

> _Lançar o produto, sem que ele seja &#8216;usável'(ao menos navegável). Sem ter uma mínima noção de como e quais plataformas os clientes usarão._

Melhor &#8216;pecar&#8217; pelo excesso de zelo no lançamento, e então depois adequar as estratégias com a realidade observada, do que ver naufragar sem nem ao menos ter tido tempo de avaliar a situação.

Novidade é sempre bom, e muito legal. Duas linguagens que estão causando um belo alvoroço, é a nova versão do HTML, que trás consigo diversas inovações, e pesa ainda mais na semântica, e a nova do CSS, com praticamente uma metodologia de desenvolvimento diferente da que estamos acostumados. Junto com elas, um novo mundo de possibilidades.

Porém é bem arriscado usar tecnologias que não estão estáveis. Nesse ponto, alguns desenvolvedores falham, pois deveriam se ater em estudar a base, HTML4, e CSS2.1 do que ficar decorando novas propriedades e tags, que não são muito bem suportadas.

Afinal de contas a parte estrutural, o box model, está definido no CSS 2.1 ainda. Se você não souber manipular corretamente, padding, margin, border, float, clear, position.. de nada vai lhe valer text-shadow, backgrounds multiplos.. Seja &#8216;bom&#8217; em CSS 1 e CSS 2.1 só depois estude CSS 3, se necessário, e se o teu projeto assim permitir.

O mesmo digo para HTML5, de nada adianta você não entender o que é semântica com HTML4, e já querer usar as tags da nova versão. Se você ainda não é hard coder nas versões atuais, se dedique a isso.

A compatibilidade virá. Mas se o próprio grupo de desenvolvimento demora para lançar integralmente, versões finais, ou no mínimo estáveis, não podemos esperar muito de uma parcela mais leiga de usuários, que não conhecem os motivos para manter atualizadas as vesões dos softwares.

Não deixe a sua taxa de bounces aumentar por causa de &#8216;birra&#8217; pessoal contra o navegador. Okay, custa e leva tempo ajustar para ficar compatível, porém **a análise** dos usuários vai lhe dizer o que fazer. E não uma decisão, tomada sem pensar no todo.

Analise teus usuários, e no mínimo faça funcionar(talvez com menos funcionalidades, um pouco mais feio, porém funcional). Não perder dinheiro é a meta.
