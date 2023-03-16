---
id: 2957
title: Otimização de imagens com media queries
date: 2013-05-15T08:58:04+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2957
permalink: /css/otimizacao-de-imagens-com-media-queries/
categories:
  - CSS
---
## Otimizando imagens

Já sabemos que:

<ol class="bullet">
  <li>
    o <a href="http://www.smushit.com/ysmush.it/" rel="nofollow">smushit</a> comprime imagens sem perda de qualidade;
  </li>
  <li>
    servir imagens a partir de um subdomínio ajuda enganar o browser para então aumentarmos o paralelismo;
  </li>
  <li>
    se esse subdomínio for cookieless melhor ainda;
  </li>
  <li>
    o servidor nginx no lugar do apache, é mais recomendado para assets;
  </li>
  <li>
    se configurarmos eTags no servidor os assets irão cachear;
  </li>
  <li>
    devemos ter gzip para que sejam servidos arquivos menores;
  </li>
  <li>
    devemos ter certeza de que não há nenhuma requisição inválida, afinal o browser perde um tempo considerável ao buscar um recurso com erro, e isso impacta na performance do site.
  </li>
</ol>



Mas hoje em dia, temos que nos preocupar **também com os diversos tamanhos** de tela, por isso, não faz sentido deixar nosso visitante fazer download de uma imagem gigante que não apareça na tela dele.

## Servindo imagens específicas

As nossas novas amigas **media queries** podem nos ajudar nessa otimização de imagens. E para isso, me apoio num comportamento inteligente dos browsers modernos.

<!--more-->



Note o código abaixo:

<pre class="css">body { background: url('image-1.jpg'); }
body { background: url('image-2.jpg'); }
```

Mesmo declarando dois backgrounds image diferentes para um mesmo elemento, o browser não faz download dos dois arquivos. Ele trás apenas aquele que realmente irá ser usado.

<img src="/wp-content/uploads/2013/05/download-img.jpg" alt="download-img" width="600" height="151" class="aligncenter size-full wp-image-2960" srcset="/wp-content/uploads/2013/05/download-img.jpg 600w, /wp-content/uploads/2013/05/download-img-300x75.jpg 300w" sizes="(max-width: 600px) 100vw, 600px" />

## Media Queries

Podemos usar media queries para trocar backgrounds, colocando arquivos menores e mais otimizados para específicas resoluções de tela, com a tranquilidade de saber que apenas o recurso que tiver com mais especificidade será baixado.

### Para dispositivos pequenos

Podemos servir um background mais largo que 480px de largura para as telas que tiverem essa largura ou mais, e podemos servir outro background menor para as telas em que essa imagem não seria completamente visualizada.

<pre class="css">body { background: url('image-1.jpg'); }
@media screen and (max-width: 480px) {
  body { background: url('image-2.jpg'); }
}
```

### Para telas grandes

Assim como podemos fazer o contrário também, e só mostrar um background grande se a tela for grande:

<pre class="css">@media screen and (min-width: 1280px) {
  body { background: url('image-1.jpg'); }
}
```

Nesse caso, se a tela tiver no mínimo 1280px, ai apresento esse background, caso ela for menor, não coloco nada.

## A imagem mais otimizada é aquela que não precisa ser baixada

Antes fazíamos isso trocando imagens por regras css, como <var>linear-gradient</var>, <var>border-radius</var> e agora com as medias queries podemos evitar que um recurso de imagem seja baixado, ou que um outro menor e mais otimizado seja servido para cada tamanho de tela que suportarmos.

Já tinha pensado nisso ?
