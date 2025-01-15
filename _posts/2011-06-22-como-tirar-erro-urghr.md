---
id: 1107
title: 'Como &#8216;tirar erro&#8217;? Urghr !!'
date: 2011-06-22T07:00:11+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1107
permalink: /opiniao/como-tirar-erro-urghr/
categories:
  - Opinião
tags:
  - programação
---
Ahhhh!! como fico revoltado qndo vejo desenvolvedores procurando formas de &#8216;se livrar dos erros&#8217;!!

> _Os erros são teus amigos!_

Para de varre-los para debaixo do tapete.

Sério. Imagine se vc <u>não sentisse dor</u>! Você se machucaria, perderia uma perna, e nem notaria!

Você prefere **esconder** a dor de estar perdendo a perna, ou **entender o motivo** do que está te levando a perdê-la ? E então tentar recuperá-la ?

<!--more-->



Pois é. Acontece o mesmo com os erros que as linguagens de programação nos apresentam.

Não fuja deles. Pelo contrário, vá atrás. Busque!

Fique preocupado quando vc não ver nenhum erro, e ainda assim a aplicação se comportar de forma inesperada, ou &#8216;incorreta&#8217;. Ai sim começa a tua dor de cabeça. Enquanto os erros estão sendo exibidos, e você não os ignora, você pode corrigi-los, alterar o script, melhorar rotinas, refatorar códigos!

Linguagens como o php são muito perigosas. Possuem recursos absurdos como supressores de erro ( @ ), desabilitar ou diminuir o nível de alertas..

Okay, se for para falhar, falhe de forma elegante, por isso em ambiente de produção, é recomendável sim, que você elimine ao máximo as configurações que mostram erros da linguagem.

Porém, é por esse mesmo motivo, que em ambiente de desenvolvimento, vc deve ser acostumado a trabalhar com o mais alto ruído de erros. Warnings, Fatal Errors, Notices..

Não falo de erros fantasmas, para os quais existem toda uma metodologia de testes, para desvendá-los.

Mas daqueles menores, que vejo no fórum, e estão tão presentes no nosso dia a dia. Tente pensar como programador.

Okay, tem um erro: Então: **Leia, entenda, revise o script e corrija**.

Não apareceu o erro ? tela branca ?

Tenha em mente, que se não for um erro comportamental, em algum lugar ele está. Abra o código fonte HTML gerado, Ctrl+U. Procure o log de erros do servidor web(Apache&#8230;), com isso em mãos, você será capaz de se virar e resolver a questão.

JavaScript então ? Use um navegador bom, como o Firefox, o Chrome, Ctrl+Shif+J, ou ótimas ferramentas como o Firebug, o Dragonfly.. ou então até mesmo se &#8216;só não funcionar no IE&#8217;. Procure entender o motivo. Alguma coisa tem.

CSS ? Existe o FirebugLite para IE, aquela barrinha de desenvolvedores da própria M$..

Existem diversas formas de se chegar a um mesmo resultado. Procure aquela que faça sentido para você primeiramente, e que funcione bem.

&#8220;_Existem diversas formas de <u>bloquear um site para tal navegador</u>, com javascript, com php, e até com html puro é possível (comentários condicionais)

porém essa não é uma forma elegante de desenvolver para web.</p>

Imagine se o desenvolvedor de um sistema de ecommerce resolve usar essa solução.

O cliente dele simplesmente não conseguiria **vender**(e atenção pois vender significa grana, dinheiro), por que foi informado que aquele site não é bem visualizado em tal navegador(coisa bem anos 90 isso).

Hoje em dia não é tão dificil assim, fazer ao menos um básico que funcione bem e bonito, nivelando por baixo, que é o nosso amigo ie6.

Vai de cada desenvolvedor escolher, porém entregar as pontas, e tacar a culpa toda no navegador não é a única solução. </em>&#8220;.

Enfim, não existe desculpa! não tenha medo do erros, procure eles.

E mais do que isso, procure entenda-os para assim corrigi-los.
