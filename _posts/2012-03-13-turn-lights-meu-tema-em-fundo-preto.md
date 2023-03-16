---
id: 1870
title: 'Turn lights Off &#8211; Meu tema em fundo preto'
date: 2012-03-13T15:56:10+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1870
permalink: /css/turn-lights-meu-tema-em-fundo-preto/
categories:
  - CSS
---
Site com fundo preto é cansativo, ainda mais se for um site com bastante conteúdo para lermos.
  
Porém, por diversas razões há quem goste.

Pensando nessa linha, implementei um botão ali no header do meu blog: &#8220;black theme&#8221;.
  
Estou em fase de testes. Não travei com cookie ainda.

Adicionei as seguintes linhas no meu css, para &#8220;mudar&#8221; a cor do meu tema.
  
<!--more-->

<pre name="code" class="css:firstLine[199]">/* black style */
#switch { cursor: pointer; border: 1px solid #ccc; 
display: inline-block; padding: 5px 20px; }
body.black { background: #090909; }

.black .post time,
.black #main { background: transparent; }

.black #sidebar a,
.black, .black #switch,
.black h1 a, .black h2 a { color: #fff; }

.black .post time,
.black h1, .black h2, .black h3, .black h4, .black h5, .black h6,
.black a { color: #00aaff; }


/* highlight */
.black .dp-highlighter ol li span { color: #333; }

.black .dp-highlighter .tools,
.black .dp-highlighter, .black .dp-highlighter ol,
.black .dp-highlighter ol li, .black .dp-highlighter .columns div,
.black .dp-highlighter ol li.alt { background: transparent; }

.black .dp-highlighter .tools,
.black .dp-highlighter ol li, .black .dp-highlighter .columns div { border-color: #00aaff; }
```

Como podem ver, o javascript apenas adiciona uma class ao body e pronto. O css cuida do restante.

Tendo ficado bom, eu termino a implementação e travo com cookie a sua opção de ver meu blog _in black_.
  
Me digam oque acharam. =)