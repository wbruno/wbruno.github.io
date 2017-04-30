---
id: 786
title: Problemas com acentuação no AJAX, como resolver
date: 2011-04-19T06:20:39+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=786
permalink: /ajax/problemas-acentuacao-ajax-como-resolver/
dsq_thread_id:
  - "2100730355"
categories:
  - AJAX
tags:
  - firefox
---
Depois do [primeiro post](http://www.wbruno.com.br/2011/04/14/como-debugar-ajax-firebug/), agora, nosso retorno é:

[<img src="/wp-content/uploads/2011/04/req.jpg" alt="" title="req" width="692" height="267" class="aligncenter size-full wp-image-788" srcset="/wp-content/uploads/2011/04/req.jpg 692w, /wp-content/uploads/2011/04/req-300x115.jpg 300w" sizes="(max-width: 692px) 100vw, 692px" />](/wp-content/uploads/2011/04/req.jpg)

## Problemas com acentos ����

Necessário aqui, é entender como funcionam as coisas. No browser, está sendo exibido � no lugar do acento.

Porém no console do **Firebug**, tá certinho.

Voltando para a primeira aba:

<small><br /> Cabeçalhos de Resposta<br /> <strong>Content-Type</strong> text/html; charset=iso-8859-1</small>

<!--more-->



Vamos _forçar_ esse charset:

<pre name="code" class="php">&lt;?php
	header ('Content-type: text/html; charset=iso-8859-1');
	echo 'Beleza, chegou até aqui!';</pre>

Okay, funciona.. basta mantermos o padrão. Se definirmos usar ISO, então usemos ISO em tudo.

Na codificação do arquivo, nos headers que vamos enviar ao navegador, na tabela do banco de dados, na meta tag do documento html..

## Problemas com acentos [ 2 ] &#8211; Ã Ã£..

[<img src="/wp-content/uploads/2011/04/erro23.jpg" alt="" title="erro2" width="546" height="242" class="aligncenter size-full wp-image-807" srcset="/wp-content/uploads/2011/04/erro23.jpg 546w, /wp-content/uploads/2011/04/erro23-300x132.jpg 300w" sizes="(max-width: 546px) 100vw, 546px" />](/wp-content/uploads/2011/04/erro23.jpg)

Nesse momento é que a galera costuma se enrolar. E fica procurando fazer milagres com os **utf8_encode|decode()**. Só &#8216;precisamos&#8217; disso, qndo temos algo &#8216;realmente&#8217; em uma codificação diferente. Como é o caso de estarmos trabalhando com banco de dados.

Aqui, não era necessário:

<pre name="code" class="php:firstLine[3]">$arr = Array('nome'=>utf8_encode('Jéssicão'), 'blog'=>'wbruno.com.br');</pre>

Porém, aqui já é:

<pre name="code" class="php:firstLine[1]">&lt;?php
	header ('Content-type: text/html; charset=utf-8');

	$db = new mysqli('localhost','root','123','test');//o php não é o foco
	$query = $db->query( 'SELECT id, nome FROM usuario WHERE id = 2' );
	if( $query->num_rows )
		echo $query->fetch_object()->nome;//echo utf8_encode( $query->fetch_object()->nome );</pre>

Pois a nossa tabela:

<pre name="code" class="sql">CREATE TABLE IF NOT EXISTS `usuario` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nome` varchar(50) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=3 ;</pre>

Está em ISO.

## Assinatura BOM ï»¿ {#bom}

<pre name="code" class="php">&lt;?php
	header ('Content-type: text/html; charset=iso-8859-1');
	echo 'Beleza, chegou até aqui!';</pre>

Se o arquivo estiver em UTF com assinatura BOM:

[<img src="/wp-content/uploads/2011/04/req2.jpg" alt="" title="req2" width="252" height="107" class="aligncenter size-full wp-image-789" />](/wp-content/uploads/2011/04/req2.jpg)

Se quisermos usar UTF8 mesmo, precisamos codificar os arquivos nesse content type.

### No Notepad++

[<img src="/wp-content/uploads/2011/04/notepadutf.jpg" alt="" title="notepadutf" width="360" height="179" class="aligncenter size-full wp-image-794" srcset="/wp-content/uploads/2011/04/notepadutf.jpg 360w, /wp-content/uploads/2011/04/notepadutf-300x149.jpg 300w" sizes="(max-width: 360px) 100vw, 360px" />](/wp-content/uploads/2011/04/notepadutf.jpg)

### No Dreamweaver

<small>apesar de eu não gostar desse programa, pode ajudar algumas pessoas, deixar aqui como resolver nele</small>

[<img src="/wp-content/uploads/2011/04/dreamut.png" alt="" title="dreamut" width="637" height="383" class="aligncenter size-full wp-image-793" srcset="/wp-content/uploads/2011/04/dreamut.png 637w, /wp-content/uploads/2011/04/dreamut-300x180.png 300w" sizes="(max-width: 637px) 100vw, 637px" />](/wp-content/uploads/2011/04/dreamut.png)Basta salvar o arquivo, desmarcando esta opção.

## jSON é UTF8 por definição

Vale lembrar disso. Então se vamos trabalhar todo o documento html em ISO, e precisamos de jSON, temos que corrigir em algum momento a codificação, para não termos problemas.

<pre name="code" class="php">&lt;?php
	header ('Content-type: text/html; charset=iso-8859-1');

	$arr = Array('nome'=>'Bruno','site'=>'wbruno.com.br');
	echo json_encode( $arr );</pre>

**index.html**

<pre name="code" class="javascript:firsLine[24]">if (xmlHttp.readyState == 4){
			var json = eval('(' + xmlHttp.responseText + ')');
			id('response').innerHTML = json.nome;
		}</pre>

De novo, sem nenhum erro no console, tudo aparentemente correto no xhr, porém &#8216;não funciona&#8217;!!

É aquilo que eu já disse, javascript tem erros silenciosos. Nesse caso, como <a href="http://json.org/json-pt.html" target="_blank">jSON é utf-8 por definição</a>, e mandamos ele com um cabeçalho ISO, não temos uma &#8216;saída válida&#8217;.

O correto, é forçarmos a saída do json em utf. Note que estamos trabalhando apenas em cima, dos dados recebidos. Para os dados enviados, é outra história.

Ainda é possível fazer uma combinação com oque expus, do tipo header+utf8_encode()+bd.. Mas acho que já deu para <a href="http://elmicox.blogspot.com/2006/06/ajax-acentuao-soluo-final-1-linha-de.html" target="_blank">entender o conceito</a>. A única coisa que discordo do Micox, é que &#8216;não precisamos necessariamente&#8217;, forçar o cabeçalho ISO sempre. Dá para trabalhar bem com tudo em UTF8, sem quebras nos acentos.

<pre name="code" class="php">&lt;?php
	header ('Content-type: text/html; charset=utf-8');

	$db = new mysqli('localhost','root','123','test');//o php não é o foco
	$query = $db->query( 'SELECT id, nome FROM usuario WHERE id = 2' );
	if( $query->num_rows )
		echo utf8_encode( $query->fetch_object()->nome );</pre>

Eu acho que:

> _Toda &#8216;fórmula mágica&#8217; em programação é burra e falha_

(Não existem)|(Não deveriam existir) fórmulas mágicas, nem &#8216;soluções definitivas&#8217;&#8230; procure <a href="http://www.w3.org/International/O-HTTP-charset" target="_blank">entender os motivos, pesquise pelas causas</a>.

## Acentos em entities &#8211; &eacute; &atilde; &#8230;

Deselegante, porém lógico que funciona!

<pre name="code" class="php:firstLine[8]">echo htmlentities( $query->fetch_object()->nome );</pre>

Nesse caso, estamos transportanto apenas texto puro:

[<img src="/wp-content/uploads/2011/04/erro32.jpg" alt="" title="erro3" width="460" height="76" class="aligncenter size-full wp-image-810" srcset="/wp-content/uploads/2011/04/erro32.jpg 460w, /wp-content/uploads/2011/04/erro32-300x49.jpg 300w" sizes="(max-width: 460px) 100vw, 460px" />](/wp-content/uploads/2011/04/erro32.jpg)Não importa como vamos trazer a string, não importam os cabeçalhos que o servidor está nos devolvendo, oque está vindo, é texto puro, <u>sem nenhum caracter especial</u>.

Porém, vamos trafegar mais informações do que das outras formas [strings maiores].

Consulta rápida:

**ASP:**

<pre name="code" class="php">&lt;% Response.Charset="ISO-8859-1" %></pre>

**PHP:**

<pre name="code" class="php">&lt;?php header("Content-Type: text/html; charset=ISO-8859-1",true); ?></pre>

**JSP:**

<pre name="code" class="php">&lt;%@ page contentType="text/html; charset=ISO-8859-1" %></pre>

**HTML**

<pre name="code" class="html">&lt;meta http-equiv="content-type" content="text/html; charset=ISO-8859-1" /></pre>

Bom, acho que é isso. Quis escrever sobre, para dar embasamento para os meus demais posts, e porque eu já passei por essas situações, e já bati muito a cabeça para conseguir resolver.

Vamos estudando e entendendo como funcionam as coisas ! Bons estudos a todos nós.
