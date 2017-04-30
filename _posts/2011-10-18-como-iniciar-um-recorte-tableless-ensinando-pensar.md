---
id: 1477
title: 'Como iniciar um recorte tableless &#8211; ensinando a pensar'
date: 2011-10-18T16:30:21+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1477
permalink: /css/como-iniciar-um-recorte-tableless-ensinando-pensar/
dsq_thread_id:
  - "2104736011"
categories:
  - CSS
tags:
  - tableless
---
Depois do post motivacional para [iniciar o recorte Tableless](http://wbruno.com.br/2011/10/10/como-iniciar-um-recorte-tableless-comece/), vamos agora entender como pensar.
  
<!--more-->

## Abstraindo a estrutura

Uma das capacidades mais importantes para um desenvolvedor/programador, é a habilidade de abstrair.
  
Você deve ser capaz de olhar para uma estrutura complexa, e quebrar esta em diversas partes. Resolva cada uma das partes, cada um dos &#8220;probleminhas menores&#8221;, e então no final você terá resolvido o todo.
  
[<img src="http://wbruno.com.br/wp-content/uploads/2011/10/lay1.jpg" alt="" title="lay1" width="400" height="238" class="aligncenter size-full wp-image-1490" srcset="http://wbruno.com.br/wp-content/uploads/2011/10/lay1.jpg 400w, http://wbruno.com.br/wp-content/uploads/2011/10/lay1-300x178.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" />](http://wbruno.com.br/wp-content/uploads/2011/10/lay1.jpg)

## Não desperdice elementos

[<img src="http://wbruno.com.br/wp-content/uploads/2011/10/filete1-12x300.jpg" alt="" title="filete" width="12" height="300" class="alignright size-medium wp-image-1496" srcset="http://wbruno.com.br/wp-content/uploads/2011/10/filete1-12x300.jpg 12w, http://wbruno.com.br/wp-content/uploads/2011/10/filete1.jpg 24w" sizes="(max-width: 12px) 100vw, 12px" />](http://wbruno.com.br/wp-content/uploads/2011/10/filete1.jpg)
  
Nem sempre precisamos de mais marcação html para resolver um efeito de layout.
  
Um elemento muito bom que temos &#8220;de graça&#8221; na nossa marcação é o <body>, use!
  
Ele ocupa por default 100% da largura da viewport do browser. Ele sempre estará lá, e por trás de todo e qualquer elemento novo que adicionemos.

Logo, a escolha óbvia para esse elemento, é que ele receba um **background-image|color:** do fundo do site. Pode parecer básico para alguns, mas frequentemente navego em sites, em que seus DEVs, criaram um outro elemento apenas para o fundo, em vez de utilizar o body.

A nossa escolha mais óbvia para o bg image do <body> é aquele degradê azul ali no fundo. Sim, começamos montando o palco, e então vamos vindo para frente.
  
Note que é este filete que coloquei de imagem aqui do lado direito: 

Este filete pode ser tão fino quanto quisermos, 1px de largura basta, pois o efeito de degradê está na orientação vertical.
  
Outras variações, seriam um fundo com linhas diagonais, degradê invertido(mais claro no topo)&#8230;

## Identificando as partes grandes

Por mais complexo que seja, inicie do simples, de fora para dentro.[ regra da cadeia ]
  
Olhe para o todo, e veja quais partes são &#8220;independentes&#8221; e até &#8220;imutáveis&#8221;. Nessa etapa, você vai dar uma borrada mental no conteudo, e enxergar mais ou menos assim:
  
[<img src="http://wbruno.com.br/wp-content/uploads/2011/10/borrado1.jpg" alt="" title="borrado1" width="400" height="238" class="aligncenter size-full wp-image-1487" srcset="http://wbruno.com.br/wp-content/uploads/2011/10/borrado1.jpg 400w, http://wbruno.com.br/wp-content/uploads/2011/10/borrado1-300x178.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" />](http://wbruno.com.br/wp-content/uploads/2011/10/borrado1.jpg)

## Resolvido o fundo, vamos para os proximos blocos

[<img src="http://wbruno.com.br/wp-content/uploads/2011/10/bgrodape2.jpg" alt="" title="bgrodape" width="5" height="140" class="alignleft size-full wp-image-1509" style="margin-right: 20px;" />](http://wbruno.com.br/wp-content/uploads/2011/10/bgrodape2.jpg)

Aqui vejo 2 prioridades:
  
topo em 100% de largura(um pouco mal feito no site atual), e rodapé 100% largura.
  
Uma técnica que tenho gostado bastante de utilizar é a seguinte:

<div style="clear: both;">
</div>

<pre class="html" name="code">&lt;div id="header">
    &lt;div class="content">
        aqui dentro o conteudo do topo
    &lt;/div><!-- /content -->
&lt;/div>&lt;!-- /header -->
...


&lt;div id="footer">
    &lt;div class="content">
        aqui dentro o conteudo do topo
    &lt;/div>

<!-- /content -->
&lt;/div>&lt;!-- /footer -->
</pre>

sendo a class **.content**, a nossa div responsável por centralizar o conteudo, e as externas **#header**, e **#footer**, os elementos que vão ter o nosso background 100% de largura.

<pre name="code" class="css">.content {
    width: 960px;
    margin: 0 auto;
}</pre>

[<img src="http://wbruno.com.br/wp-content/uploads/2011/10/bgtopo-300x25.jpg" alt="" title="bgtopo" width="300" height="25" class="aligncenter size-medium wp-image-1507" srcset="http://wbruno.com.br/wp-content/uploads/2011/10/bgtopo-300x25.jpg 300w, http://wbruno.com.br/wp-content/uploads/2011/10/bgtopo.jpg 400w" sizes="(max-width: 300px) 100vw, 300px" />](http://wbruno.com.br/wp-content/uploads/2011/10/bgtopo.jpg)
  
ok ? repetimos o mesmo processo anterior para definir o filete de bg do rodapé, e temos q usar uma imagem gigantesca em largura para o fundo do topo. Atenção para usá-la, com background-position: center top;

## O miolo

aqui, tem aquela sidebar laranja, que pede obviamente um float : left; e o restante na direita.

<pre class="html" name="code">&lt;div id="content" clas="content">
    &lt;div id="sidebar">
        conteudo da sidebar laranja
    &lt;/div>&lt;!-- /sidebar -->
    &lt;div id="main">
        aquelas 3 caixinhas, o produto em destaque(slideshow)..
    &lt;/div>&lt;!-- /main -->
&lt;/div>&lt;!-- /content -->
</pre>

Note que idento corretamente meu HTML, e uso um comentário para marcar o final de cada bloco. 

Essa é a estrutura simples e básica que precisamos para o &#8220;palco&#8221; do nosso recorte. Em cima disso, vamos montando cada parte, repetindo os passos que aqui fizemos, e adicionando algumas particularidades.
  
É muito importante entender bem os conceitos de box model, só usar position qndo realmente necessário, e se vc souber como fazê-lo(assunto extenso, então depois falo sobre isso especificamente), evitar hacks e tb propriedades com valores gigantescos, como: margin-left: 500px;..

Esse tipo de declaração, geralmente deve ter um cheiro ruim para você.. indicando que algo provavelmente está errado.
  
Bom, é isso.