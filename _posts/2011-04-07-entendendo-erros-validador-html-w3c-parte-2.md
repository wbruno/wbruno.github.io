---
id: 635
title: 'Entendendo erros do validador HTML w3c &#8211; Parte 2'
date: 2011-04-07T06:50:44+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=635
permalink: /html/entendendo-erros-validador-html-w3c-parte-2/
dsq_thread_id:
  - "2103188454"
categories:
  - HTML
tags:
  - validador
  - w3c
  - xhtml
---
Continuando o [artigo anterior](https://wbruno.com.br/html/entendendo-erros-validador-html-w3c/), primeiro antes de entendermos os **erros do validador**, precisamos entender a forma com que ele nos apresenta eles.

Nossos documentos são processados da mesma forma que idealmente|naturalmente escrevemos eles: De cima para baixo, da esquerda para a direita. O validador percorre todo nosso documento procurando por <u>defeitos na sintaxe</u>. Importante ressaltarmos isso. Erros na sintaxe</u>, e nada mais.

<!--more-->



Existem os **alertas** [<img src="/wp-content/uploads/2011/04/warnings1.jpg" alt="" title="warnings" width="21" height="21" class="alignnone size-full wp-image-643" />](/wp-content/uploads/2011/04/warnings1.jpg).

Que geralmente são causados por algum erro, ou falha de melhor significância.

Existem as **informações** [<img src="/wp-content/uploads/2011/04/infos1.jpg" alt="" title="infos" width="21" height="21" class="alignnone size-full wp-image-642" />](/wp-content/uploads/2011/04/infos1.jpg).

Geralmente também apenas nos servirão como &#8216;dicas&#8217;

E os **erros** de fato [<img src="/wp-content/uploads/2011/04/errors1.jpg" alt="" title="errors" width="17" height="18" class="alignnone size-full wp-image-641" />](/wp-content/uploads/2011/04/errors1.jpg).

Com este sim, precisamos nos preocupar. Nesse primeiro momento vamos olhar apenas as linhas que tiverem esse ícone [<img src="/wp-content/uploads/2011/04/errors1.jpg" alt="" title="errors" width="17" height="18" class="alignnone size-full wp-image-641" />](/wp-content/uploads/2011/04/errors1.jpg).

## Erro 1a: end tag for &#8220;blablabla&#8221; omitted, but OMITTAG NO was specified

[<img src="/wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM-1024x338.png" alt="" title="Screen shot 2011-04-04 at 2.21.36 PM" width="695" height="229" class="aligncenter size-large wp-image-614" srcset="/wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM-1024x338.png 1024w, /wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM-300x99.png 300w, /wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM.png 1432w" sizes="(max-width: 695px) 100vw, 695px" />](/wp-content/uploads/2011/04/Screen-shot-2011-04-04-at-2.21.36-PM.png)

Gerado por:

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>wbruno</title>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<br>
</body>
</html>
```

Apenas temos que lembrar de uma regra básica do xHTML: **Todas as tags devem obrigatoriamente ser fechadas**.

Logo, deve ficar:

``` html
<br />
```
Costumo colocar um espaço entre a tag e o fechamento, pois em algum browser antigo, isso pode gerar problemas, além do que fica mais bonito ver a tag assim.

<br /> é uma tag vazia, assim como <meta />, <img />&#8230; então o fechamento é apenas /> (barra sinal de maior)

<h2 style="margin-top: 30px;">
  Erro 1b: end tag for &#8220;blablabla&#8221; omitted, but OMITTAG NO was specified
</h2>

``` html
<p>Texto..
</body>
```
nesse caso, estamos trabalhando com uma tag que possui fechamento </p>. Pois possui conteúdo, porém não colocamos, ai o validador nos indica erro:

[<img src="/wp-content/uploads/2011/04/erro21.jpg" alt="" title="erro2" width="583" height="146" class="aligncenter size-full wp-image-665" srcset="/wp-content/uploads/2011/04/erro21.jpg 583w, /wp-content/uploads/2011/04/erro21-300x75.jpg 300w" sizes="(max-width: 583px) 100vw, 583px" />](/wp-content/uploads/2011/04/erro21.jpg)

Note que o erro foi disparado na tag seguinte. Porém o problema mesmo está no nosso <p>, que esquecemos de fechar.

A info <img src="/wp-content/uploads/2011/04/infos1.jpg" alt="" title="infos" width="21" height="21" class="alignnone size-full wp-image-642" />, nos ajuda nisso. Indicando quem foi que &#8216;gerou&#8217; o erro.

Corrigindo:

``` html
<p>Texto..</p>
```
Fica tudo certo.

<h2 style="margin-top: 30px;">
  Erro 2a: end tag for element &#8220;blablabla&#8221; which is not open
</h2>

[<img src="/wp-content/uploads/2011/04/erro4.jpg" alt="" title="erro4" width="403" height="48" class="aligncenter size-full wp-image-661" srcset="/wp-content/uploads/2011/04/erro4.jpg 403w, /wp-content/uploads/2011/04/erro4-300x35.jpg 300w" sizes="(max-width: 403px) 100vw, 403px" />](/wp-content/uploads/2011/04/erro4.jpg)

Esse erro pode acontecer tanto quando fechamos algo que realmente não abrimos:

``` html
<body>
<SPAN>Texto</sPan>
</p>
</body>
```
Como também, no Erro 2a que mostrei. Tentando fechar uma tag que não existe, por causa do case-sensitive da linguagem.

<h2 style="margin-top: 30px;">
  Erro 1a e 2a
</h2>

##### end tag for &#8220;blablabla&#8221; omitted, but OMITTAG NO was specified, end tag for element &#8220;blablabla&#8221; which is not open

``` html
<p><span>Texto</p></span>
```
O aninhamento deve ser correto. Respeitando a ordem.

Abri um p, depois abri um span, então primeiro preciso fechar o span, para depois fechar o p.

Estou dando exemplos com estas tags, porém o conceito se aplica para quaisquer tags.

Correto:

``` html
<p><span>Texto</span></p>
```
<h2 style="margin-top: 30px;">
  Erro 3a: element &#8220;blablabla&#8221; undefined
</h2>

``` html
<SPAN>Texto</sPan>
```
Outros erros &#8216;absurdos&#8217;: [<img src="/wp-content/uploads/2011/04/erro31.jpg" alt="" title="erro3" width="412" height="99" class="aligncenter size-full wp-image-663" srcset="/wp-content/uploads/2011/04/erro31.jpg 412w, /wp-content/uploads/2011/04/erro31-300x72.jpg 300w" sizes="(max-width: 412px) 100vw, 412px" />](/wp-content/uploads/2011/04/erro31.jpg)

Outra regra básica do xHTML, por esse ser baseado em XML: **Todas as tags devem ser escritas em minúsculo**.

O segundo erro é interessante, pois nos mostra como xHTML é também **case sensitive**, nos informa que SPAN todo em maiusculo, é diferente de sPan, dessa forma estranha, escrito com uma alternância entre maiuscula e minusculas.

Basta escrever as tags todas em minúsculo, sempre.

<h2 style="margin-top: 30px;">
  Erro 3b: element &#8220;blablabla&#8221; undefined
</h2>

``` html

<wb></wb>
```


<p>
  De fato, não existe nosso elemento <strong>wb</strong>. Não devemos inventar tags. xHTML foi escrito com base em XML, mas usando as tags da linguagem HTML4.01
</p>


<h2 style="margin-top: 30px;">
  Erro 4a: document type does not allow element &#8220;blablabla&#8221; here; missing one of &#8220;wishkas sachê..&#8221;
</h2>


<p>
  <a href="/wp-content/uploads/2011/04/erro5.jpg"><img src="/wp-content/uploads/2011/04/erro5.jpg" alt="" title="erro5" width="502" height="31" class="aligncenter size-full wp-image-671" srcset="/wp-content/uploads/2011/04/erro5.jpg 502w, /wp-content/uploads/2011/04/erro5-300x18.jpg 300w" sizes="(max-width: 502px) 100vw, 502px" /></a><br />
  Um elemento <strong>inline</strong>, não deve conter um elemento <strong>nível de bloco</strong>.<br />
  é nivel de bloco.<br />
  <span> é inline.<br />
  Nas possíveis causas, o próprio validador nos informa o motivo real:
</p>



<p>
  <em>&#8220;One possible cause for this message is that you have attempted to put a block-level element (such as &#8220;&#8221; or &#8220;<table>&#8221;) inside an inline element (such as &#8220;<a&gt;&#8221;, &#8220;<span>&#8221;, or &#8220;&#8221;)&#8221;</em>
</p>


<p>
  Porém não dá para sempre confiar apenas nessas mensagens, e é muito mais interessante saber o motivo, do que apenas saber arrumar.
</p>


<h2 style="margin-top: 30px;">
  Erro 4b: document type does not allow element &#8220;blablabla&#8221; here; missing one of &#8220;wishkas sachê..&#8221;
</h2>


<p>
  Não raramente vejo desenvolvedores fazendo:
</p>


``` html
<a href=""><h1>Texto</h1></a>

```


<p>
  Não pode pelo mesmo motivo. H1 é nivel de bloco. A é inline.<br />
  Nesse caso, abrimos o A como filho do H1, e então com <strong>CSS</strong> resolvemos essa questão, do &#8216;bloco inteiro ser clicável&#8217;, apenas declarando um display: block; para o A.
</p>


<h2 style="margin-top: 30px;">
  Erro 4c: document type does not allow element &#8220;blablabla&#8221; here; missing one of &#8220;wishkas sachê..&#8221;
</h2>


<p>
  <a href="/wp-content/uploads/2011/04/erro62.jpg"><img src="/wp-content/uploads/2011/04/erro62.jpg" alt="" title="erro6" width="703" height="43" class="aligncenter size-full wp-image-683" srcset="/wp-content/uploads/2011/04/erro62.jpg 703w, /wp-content/uploads/2011/04/erro62-300x18.jpg 300w" sizes="(max-width: 703px) 100vw, 703px" /></a>
</p>


``` html
<body>
<span>Texto...</span>
```

<p>
  Não faz sentido jogarmos assim, um elemento inline no meio do nada. Como filho direto do BODY.
</p>


<h2 style="margin-top: 30px;">
  Erro 5a:document type does not allow element &#8220;blablabla&#8221; here
</h2>


<p>
  <a href="/wp-content/uploads/2011/04/erro11.jpg"><img src="/wp-content/uploads/2011/04/erro11.jpg" alt="" title="erro11" width="389" height="39" class="aligncenter size-full wp-image-691" srcset="/wp-content/uploads/2011/04/erro11.jpg 389w, /wp-content/uploads/2011/04/erro11-300x30.jpg 300w" sizes="(max-width: 389px) 100vw, 389px" /></a><br />
  Parecido com os erros acima, mas não é a mesma coisa. Neste caso, a tag <link />, <strong>deve</strong> estar dentro da sessão HEAD do nosso documento, e não no meio do BODY..
</p>


``` html

</head>
<body>
<link />
```


<h2 style="margin-top: 30px;">
  Erro 6a: there is no attribute &#8220;blablabla&#8221;
</h2>


<p>
  <a href="/wp-content/uploads/2011/04/erro7.jpg"><img src="/wp-content/uploads/2011/04/erro7.jpg" alt="" title="erro7" width="298" height="42" class="aligncenter size-full wp-image-684" /></a><br />
  Assim como as tags, os atributos também devem ser escritos em letras minúsculas. Logo:
</p>


``` html
<p onclick="alert( this.innerHTML );">Texto...</p>
```

<h2 style="margin-top: 30px;">
  Erro 6b: there is no attribute &#8220;blablabla&#8221;
</h2>


``` html
<p checked="checked">Texto...</p>
```

<p>
  Esse atributo existe para inputs, mas não para parágrafos por exemplo. O erro é claro, mas nem sempre a galera se dá ao trabalho de ler:
</p>


<blockquote>
  <p>
    <em>&#8220;the document type you are using does not support that attribute for this element.&#8221;</em>
  </p>
</blockquote>


<h2 style="margin-top: 30px;">
  Erro 6c: there is no attribute &#8220;blablabla&#8221;
</h2>


``` html
<p meuatributo="true">Texto...</p>
```


<p>
  Acontece muito, ainda mais hoje em dia. Com a popularização novamente da linguagem javascript. O pessoal começa a inventar atributos absurdos só para conseguir resgatar certos valores mais facilmente. Não faça isso. Não vale apena.<br />
  Aprenda a percorrer o DOM corretamente.
</p>


<h2 style="margin-top: 30px;">
  Erro 6d: there is no attribute &#8220;blablabla&#8221;
</h2>


``` html
<a href="" target="">Link</a>
```

<p>
  No caso, o atributo <strong>target</strong>, foi <u>banido</u> nos DTDs Strict. Ele &#8216;fere&#8217; a escolha do usuário.<br />
  O que devemos fazer é deixar o usuário escolher onde ele quer abrir nossos links. Uma forma de contornar, afinal, não queremos perder visitantes, e temos que indicar sites externos, é usar javascript para fazer abrir em &#8216;nova aba|janela&#8217;.
</p>


<h2 style="margin-top: 30px;">
  Erro 7a: value of attribute &#8220;blablabla&#8221; invalid: &#8220;([:^alpha:|_])&#8221; cannot start a name
</h2>


<p>
  <a href="/wp-content/uploads/2011/04/erro8.jpg"><img src="/wp-content/uploads/2011/04/erro8.jpg" alt="" title="erro8" width="410" height="48" class="aligncenter size-full wp-image-685" srcset="/wp-content/uploads/2011/04/erro8.jpg 410w, /wp-content/uploads/2011/04/erro8-300x35.jpg 300w" sizes="(max-width: 410px) 100vw, 410px" /></a><br />
  Não devemos começar os valores de nossos atributos, com caracteres que não sejam letras, ou underline.
</p>


<h2 style="margin-top: 30px;">
  Erro 8a: ID &#8220;blablabla&#8221; already defined
</h2>


<p>
  <a href="/wp-content/uploads/2011/04/erro91.jpg"><img src="/wp-content/uploads/2011/04/erro91.jpg" alt="" title="erro9" width="263" height="43" class="aligncenter size-full wp-image-688" /></a>
</p>


``` html

<body>
<p id="texto">Texto...</p>
<p id="texto">Texto...</p>
```


<p>
  ID deve ser um identificador único no nosso documento. Se precisamos aplicar um mesmo estilo CSS, ou função jQuery, podemos nos valer do atributo <strong>class</strong>.<br />
  Aqui, a linha de info <img src="/wp-content/uploads/2011/04/infos1.jpg" alt="" title="infos" width="21" height="21" class="alignnone size-full wp-image-642" />, nos ajuda a encontrar em qual lugar do documento já tínhamos usado este ID.
</p>


<h2 style="margin-top: 30px;">
  Erro 9a: general entity &#8220;blablabla&#8221; not defined and no default entity
</h2>


<p>
  <a href="/wp-content/uploads/2011/04/erro10.jpg"><img src="/wp-content/uploads/2011/04/erro10.jpg" alt="" title="erro10" width="426" height="40" class="aligncenter size-full wp-image-689" srcset="/wp-content/uploads/2011/04/erro10.jpg 426w, /wp-content/uploads/2011/04/erro10-300x28.jpg 300w" sizes="(max-width: 426px) 100vw, 426px" /></a><br />
  Este acontece porque o &#8216;e comercial&#8217; & é um caracter especial no XML. Devemos codificá-lo para o seu respectivo entity antes de usá-lo em nosso documento.<br />
  Existe uma outra forma que é adicionar o nosso &#8216;novo entitie&#8217; na lista de entidades, mas não acho isso uma boa prática.
</p>


<h2 style="margin-top: 30px;">
  Erro 10a: required attribute &#8220;blablabla&#8221; not specified
</h2>


<p>
  <a href="/wp-content/uploads/2011/04/erro12.jpg"><img src="/wp-content/uploads/2011/04/erro12.jpg" alt="" title="erro12" width="315" height="43" class="aligncenter size-full wp-image-694" srcset="/wp-content/uploads/2011/04/erro12.jpg 315w, /wp-content/uploads/2011/04/erro12-300x40.jpg 300w" sizes="(max-width: 315px) 100vw, 315px" /></a><br />
  Tags <script> por exemplo, em xHTML1, e HTML4, devem ter o atributo <strong>type</strong> obrigatoriamente declarado.
</p>


<p>
  Conforme eu lembrar de mais algum &#8216;motivo genérico&#8217;, incluo por aqui.
</p>


<p>
  Formulários é um assunto extenso, vou deixar para o próximo post.<br />
  Por enquanto é isso, opinem! me digam o que estão achando.
</p>
