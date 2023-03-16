---
id: 1837
title: Meu CSS mínimo comum a todos os projetos que desenvolvo
date: 2012-03-06T07:00:46+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1837
permalink: /css/meu-css-minimo-comum-todos-os-projetos-desenvolvo/
dsq_thread_id:
  - "2102075223"
categories:
  - CSS
---
Gostaria de compartilhar, o meu reset.css, e as demais classes utilitárias e estilizações, que &#8220;sempre faço&#8221; inicialmente nos meus trabalhos.

Não uso nenhum dos &#8220;consagrados reset.css&#8221;, porque considero gordura ao meu estilo de desenvolver. Apenas zerar margin e padding, e me deixar livre para definir as regras das minhas tags é o suficiente, e tenho trabalhado bem assim.

Tudo bem simples, a idéia é não encher a folha de coisas desnecessárias.
  
<!--more-->

``` css
* { margin: 0; padding: 0; list-style: none; border: none; }

html, body { height: 100%; }
body,
input, select, textarea { font-size: 12px; font-family: Tahoma, sans-serif; color: #333; }

body { min-width: 300px; }

h1, h2, h3, h4, h5, h6 { }

a { text-decoration: none; color: #4b4d4d; }
a:hover { text-decoration: underline; }
p { margin-bottom: 15px; }

.content { width: 960px; margin: 0 auto; }
.fleft { float: left; }
.fright { float: right; }
.clear { clear: both; }

@media only screen and (max-width: 800px){
  .content { width: auto; }
  img { max-width: 100% !important; height: auto !important; }
}
```

Uso meu blog como repositório também, então tá aqui. =)