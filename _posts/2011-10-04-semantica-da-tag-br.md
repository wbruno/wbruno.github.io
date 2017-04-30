---
id: 1423
title: 'A semântica da tag &lt;br /> &#8211; Simplesmente não use !'
date: 2011-10-04T21:54:37+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1423
permalink: /html/semantica-da-tag-br/
dsq_thread_id:
  - "2101438254"
categories:
  - HTML
tags:
  - semântica
---
Impossível deixar de citar o texto do Henrique C. Pereira para o blog <a href="http://revolucao.etc.br/archives/introducao-a-semantica-web/" target="_blank">Revolução Etc</a>, nesse início de post:

> &#8220;Escrever algo semanticamente correto, nada mais é do que utilizar-se desses símbolos (leia-se tags) considerando o significado real pelo qual foram criados.&#8221;

<!--more-->



Não quero falar sobre **semântica** como um todo, pois já temos diversos ótimos textos espalhados por ai abordando esse tema. Vou focar este artigo somente em uma única tag: a tag <br />.

(se você tiver dúvidas sobre o básico de semântica, sugiro visitar o artigo que linkei ali no primeiro parágrafo).

Ok, então precisamos usar as tags para <cite>o real motivo pelo qual foram criadas</cite>.

Oras,

-> tags <p> foram criadas para **representar** parágrafos.

-> tags <h1> foram criadas para **representar** títulos de primeira importância.

E assim por diante.

Algumas são bem explícitas (todas são, ou deveriam ser para nós), mas e a incompreendida tag <br /> ?

Afinal, o que o **break**, _realmente_ significa ? O que essa tag deveria representar ?

<a href="http://www.w3.org/wiki/HTML/Elements/br" target="_blank">http://www.w3.org/wiki/HTML/Elements/br</a>

> The <br> element represents a line break.

Então, quando pensarmos em br, devemos pensar em **quebras de linha**.

## Não use!

Se você está em dúvida, simplesmente não use. Evite. Pelo menos até entender a hora correta de usar.

Então vamos falar sobre quando **não usar**, e sobre quando **usar**:

## Uso incomum

Sou capaz de apostar que nem 20% dos Desenvolvedores FrontEnd, conhecem o

<pre name="code" class="html">&shy;&lt;br /></pre>

Muito bem apresentado pelo Evandro, <a href="http://forum.imasters.com.br/topic/406694-manual-do-html-tag-br/" target="_blank">aqui</a>.

Então bacana, acabamos de encontrar um uso <del datetime="2011-10-04T23:27:17+00:00">incomum</del> bem desconhecido para a nossa famigerada tag! Porém, e as diferenças entre Sistema Operacional ? Entre browsers ?

Mais especificamente, entre a renderização das fontes ? aplicação ou não de antialising, smooth&#8230;

## Não force quebras de linha!

Por causa do motivo que citei acima: as diferenças de renderização.

Forçando quebras de linha com uma tag br, podemos estar condenando o nosso documento, a uma incompatibilidade entre SOs.

O espaçamento das fontes é maior no Windows do que no MAC, por exemplo.

## Não simule parágrafos

Não simule parágrafos, forçando pular linhas com br. Realmente faça os teus parágrafos.

Se precisar pular uma linha entre um ponto final e outro, então na verdade você tem um outro parágrafo. Use a tag p.

## Semântica para elementos nível de bloco

Se um elemento inline como <img />, <strong>, precisa ser colocado sozinho em uma linha, temos o valor block da propriedade display para tal. Não temos nenhum motivo para usar uma quebra de linha nesses casos.

## Tag de estruturação

Como já definido, é uma quebra de linha. Então não devemos usar como separador de 2 elementos distintos:

<pre name="code" class="html:firstLine[13]">&lt;h1>Titulo&lt;/h1>&lt;br />&lt;br />
&lt;p>Texto, texto mais texto.&lt;/p></pre>

Bem absurdo, pois se quisermos espaço entre um h1 e um p, devemos fazê-lo com css.

## Tag vazia

O break é uma tag vazia, não aceita conteúdo. O &#8216;conteudo&#8217; dela, é a linha (leia texto), que ela separa.

Uma aplicabilidade muito conhecida e defendida é a transcrição de poemas.

Realmente, temos um mesmo verso, que precisa ser escrito em diversas linhas, mas ainda estamos na mesma idéia, e só queremos representar uma pequena pausa, entre cada métrica.

<pre name="code" class="html:firstLine[13]">&lt;p>Ninguém venha me dar vida,&lt;br />
que estou morrendo de amor,&lt;br />
que estou feliz de morrer,&lt;br />
que não tenho mal nem dor,&lt;br />
que estou de sonho ferido,&lt;br />
que não me quero curar,&lt;br />
que estou deixando de ser,&lt;br />
e não quero me encontrar,&lt;br />
que estou dentro de um navio,&lt;br />
que sei que vai naufragar,&lt;/p>

&lt;p>já não falo e ainda sorrio,&lt;br />
porque está perto de mim&lt;br />
o dono verde do mar&lt;br />
que busquei desde o começo,&lt;br />
e estava apenas no fim.&lt;/p>

&lt;p>Corações, por que chorais?&lt;br />
Preparai meu arremesso&lt;br />
para as algas e os corais.&lt;/p>

&lt;p>Fim ditoso, hora feliz:&lt;br />
guardai meu amor sem preço,&lt;br />
que só quis quem não me quis.&lt;/p></pre>

Cecília Meireles

## Prefira ser semântico, do que preguiçoso

[<img src="/wp-content/uploads/2011/10/1.jpg" alt="" title="1" width="165" height="59" class="alignleft size-full wp-image-1426" />](/wp-content/uploads/2011/10/1.jpg)Muito comum no dia-a-dia, e a marcação que boa parte dos coders que já vi trabalhando, usariam é a seguinte:

<pre name="code" class="html:firstLine[13]">&lt;p>&lt;strong>Um pequeno titulo&lt;/strong>&lt;br />&lt;br />
	E aqui continua o texto&lt;/p></pre>

Sinceramente, isso fere meus princípios. Um parágrafo é um parágrafo.

Não faz nenhum sentido um parágrafo que dentro dele mesmo possui um &#8216;título&#8217;. Não estamos falando de headers do documento (tags hx), e nem de uma palavra que mereceu um destaque maior no decorrer de uma idéia.

Mas de um leve título ali, isso deve nos levar a criar um elemento separado:

<pre name="code" class="html:firstLine[13]">&lt;strong class="titulo">Um pequeno titulo&lt;/strong>
	&lt;p>E aqui continua o texto&lt;/p></pre>

E então por css, controlo o espaçamento, economizando 2 tags br que não deveriam ter sido utilizadas.

<pre name="code" class="css:firstLine[7]">.titulo {
	display: block;
	margin-bottom: 17px;
}</pre>

Bem melhor termos implementado assim. Se o espaçamento entre o título e o texto não casar exatamente com o line-height, definido para o nosso parágrafo, então não conseguiriamos nunca com a marcação anterior resolver o efeito de forma adequada.

## O break é uma leve pausa, e não espaçamentos

Tão comum vermos documentos lotados de brs seguidos um dos outros, para **espaçar**.

<pre name="code" class="html:firstLine[13]">&lt;p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.&lt;br />&lt;br />
	&lt;br />&lt;br />
	&lt;br />&lt;br />
	Pellentesque nulla tortor, lacinia eget ullamcorper id, aliquam vel metus. &lt;p>
</pre>

Ughr ! Isso agride. Pense bem, HTML é uma linguagem de **marcação**, e depois de longos esforços, **toda e qualquer** estilização foi deixada para o CSS, certo?

Então, porque raios, alguns desenvolvedores insistem em simular **espaçamentos**(algo que claramente entra no conceito de estilização, e box model), usando essa tag de **quebra de linha?**.

Não faz nenhum sentido.

Se tenho que aumentar o espaçamento entre uma oração e outra, aumento o margin-bottom do parágrafo de cima, mas nunca usarei tags <br /> para tal.

## Títulos &#8216;quebrados&#8217;

Aqui a tag br faz todo sentido:

<pre name="code" class="html:firstLine[13]">&lt;h2>Isso é:&lt;br />
Semântica.&lt;/h2></pre>

Não estamos no contexto de subtítulo, mas sim do mesmo título, da mesma idéia que mereceu uma quebra ali.

## Em conjunto com a tag <address>

Um endereço é renderizado e planejado para passar informações em várias linhas, sendo cada linha uma certa coisa.

<pre name="code" class="html:firstLine[13]">&lt;address>Rua dos bobos, 0&lt;br />
01234-567
&lt;/address></pre>

Cabe uma análise do seu contexto, lembrando que existem as listas de definição <dd> que também poderiam resolver muito bem a semântica que buscamos aqui.

## Entendeu ?

Nesse ponto, se você realmente entendeu e concorda com que propus, e você se sente habilitado para usar corretamente, use. Use sabiamente. Não para tampar buraco, ou por preguiça de fazer de outra forma.

Chegando até este ponto da leitura, você terá bagagem suficiente para usar a tag br da única forma correta que existe: **quebrar linhas**.
