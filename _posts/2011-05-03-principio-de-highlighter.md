---
id: 891
title: Princípio de highlighter
date: 2011-05-03T22:26:08+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=891
permalink: /expressao-regular/principio-de-highlighter/
categories:
  - Expressão Regular
---
<pre name="code" class="php">&lt;?php
    $str = 'Lorem ipsum del boa pergunta, \blah/ blah blah... \SOU VERDE/... eu não sou, por que? ';

    echo preg_replace( '/(\\\[a-z\s]+\/)/i', '&lt;span style="color: #0f0;">$1&lt;/span>', $str );
</pre>

segundo a minha expressão regular, vai ficar verde, as letras e espaços que estiverem entre \ e /

Código rápido que fiz para responder uma dúvida no iMasters.