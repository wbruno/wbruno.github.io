---
id: 1459
title: 'Como iniciar um recorte Tableless &#8211; comece !'
date: 2011-10-10T07:00:31+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1459
permalink: /css/como-iniciar-um-recorte-tableless-comece/
dsq_thread_id:
  - "2104735998"
categories:
  - CSS
tags:
  - tableless
---
Não basta apenas conhecer todas as tags HTML, decorar todas as propriedades CSS, assim como todos os seus respectivos valores. Tem que saber usar.

Cada tag representa uma informação, cada par: propriedade: valor css modifica nosso elemento e a cascata afetada por ele. Temos que fazer o melhor uso possível dessas ferramentas que temos disponvíveis.
  
<!--more-->

## O seu nível de conhecimento

Se você é iniciante e tem diversas dificuldades, usa mais tempo do que gostaria, e pretende se aperfeiçoar, guarde bem as idéias que vou expor. São baseadas na minha _&#8220;nem tão curta assim&#8221;_ experiência com recortes css.
  
Se você já está num nível mais alto, continue lendo pois entendendo como um colega de profissão trabalha, seremos capazes de melhorar os nossos próprios métodos e os dele também. Aceito sugestões e dicas no final do artigo (comente a vontade).

Vou mostrar como penso ao iniciar qualquer layout, ou qualquer alteração em uma página. Note que não é apenas &#8220;criar as DIVs&#8221;(como vi um outro tutorial por ai dizendo). Este não é um guia, e nem a única forma de ser fazer.
  
É mais como _a forma que faço_, e acho válido compartilhar com você.

Na verdade, &#8216;criar as divs&#8217;, é o de menos. Precisamos saber porque criar, e onde criar. Não tem fórmula mágica, ou uma estrutura padrão(topo, conteudo e rodapé) que vai atender a todos os wireframes possíveis. Precisamos analisar cada um individualmente, e então decidir qual a melhor estrutura para aquele projeto.

## Iniciando

A _estrutura padrão_, é a marcação **mínima necessária** para criar um documento válido:

<pre name="code" class="html">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
	"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
&lt;html xmlns="http://www.w3.org/1999/xhtml">
&lt;head>
	&lt;title>Iniciando um Recorte Tableless&lt;/title>
	
	&lt;meta name="author" content="William Bruno" />
	&lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
	
	&lt;link rel="shortcut icon" type="image/x-icon" href="favicon.ico" />
	&lt;link rel="stylesheet" href="css/main.css" type="text/css" />
	&lt;script type="text/javascript">&lt;/script>
&lt;/head>
&lt;body>

&lt;/body>
&lt;/html>
</pre>

## Algumas metas básicas

<pre name="code" class="html:firstLine[7]">&lt;meta name="keywords" content="" />
	&lt;meta name="description" content="" />
	
	&lt;meta name="google-site-verification" content="" />

	&lt;meta http-equiv="imagetoolbar" content="no" />	
	&lt;meta http-equiv="Pragma" content="no-cache" />
	&lt;meta http-equiv="content-language" content="pt-br" />
</pre>

Estas são as meta tags mais básicas que vamos precisar, assim que tivermos terminado a implementação da estrutura, e formos publicar a página. A meta **google-site-verification**, pode ser trocada apenas pelo snipet do seu Google Analytics.

Com essa base pronta, podemos começar a analisar o layout.

## Analisando o layout

É necessário bater o olho, e ser capaz de analisar as partes grandes do layout.
  
Enchergar a estrutura. Escolhi meio ao acaso aqui, o layout do site da <a href="http://www.voegol.com.br/pt-br/Paginas/default.aspx" target="_blank">Gol</a>.

Gaste um tempo aqui nesse passo. Planeje.
  
Olhe para o **\.(psd|png)** que o designer te enviou e resolva mentalmente ele. Vá decidindo quais elementos você pretende usar, como posicionar cada coisa.. uma olhada rápida, e apenas mental.
  
Pense, só isso. Não adianta sair desembestado fazendo, é necessário ter conciência do que será feito.

## Incompatibilidade

Se a estrutura for realmente bem feita, e fizer primeiramente sentido para você mesmo, para o motor de renderização que é o seu cérebro, então provavelmente menos problemas de compabilidades você terá.
  
Os layouts que mais quebram no Internet Explorer, Safari, e aqueles que funcionam somente no Firefox, são aqueles em que apenas &#8220;sairam fazendo&#8221;. Foram testando coisas sem sentido, e conforme a complexidade aumentava, mais camadas de html, hacks, soluções mirabolosas, foram sendo adicionadas.

Seja bem vindo ao mundo do simples, onde tudo funciona, e vários problemas de incompatibilidade são evitados, simplesmente pq vc sabe oque está fazendo.
  
No próximo post vou mostrar &#8220;como pensar&#8221; simples.