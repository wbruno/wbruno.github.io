---
id: 3398
title: Entendendo o cURL
date: 2015-06-02T07:00:21+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3398
permalink: /php/entendendo-o-curl/
videourl:
  - ""
categories:
  - PHP
---
Existe uma extensão do php chamada **cURL**, talvez seja a extensão mais útil e menos entendida do php. Diretamente do <a href="http://php.net/manual/en/intro.curl.php" rel="nofollow">manual do php</a> temos que o curl suporta diversos protocolos: http, https, ftp, gopher, telnet, dict, file, e ldap.

Eu mesmo já fiz alguns posts utilizando o cURL aqui no blog. Como o meu contexto é a web, e trabalho frequentemente com o protocolo http, irei me ater a ele.

Pense no cURL como _uma forma de realizar requisições_. Sabe quando você faz download de uma imagem, clica num link para abrir uma página web, ou envia um formulário ? Todas essas coisas são requisições http. Com essa lib nós conseguimos fazer com que a nossa aplicação, nosso programa php server-side, <a href="http://codular.com/curl-with-php" rel="nofollow">faça requisições por nós</a>.

<!--more-->

Muito útil por exemplo para fazer proxy de algum servidor que não suporte CORs, consultar alguma coisa, enviar dados para algum webservice..

Para isso temos que entender como usá-lo. Crie um arquivo chamado **endpoint.php**, com o seguinte conteúdo:

``` php
<?php

var_dump($_SERVER['REQUEST_METHOD'], $_REQUEST);
```

## GET

O GET é certamente o tipo de requisição que mais fazemos na web. O verbo GET significa isso mesmo que você está pensando: pegar alguma coisa.

Iniciaremos com apenas 3 funções, que são as mínimas necessárias para fazer uma requisição GET com cURL: **curl_init()**, **curl_exec()** e **curl_close()**.

Vou executar os exemplos pelo terminal, com o comando **php**

``` bash
$ php get.php
```

Se eu fizer uma requisição inválida, o retorno do curl_exec() será um false.

``` php
<?php
$ch = curl_init("http://foo");
$ret = curl_exec($ch);
curl_close($ch);

var_dump($ret); //false
```

E se quisermos mais informações sobre o erro, elas estarão disponíveis na função <var>curl_error($ch);</var>.

``` php
<?php
$ch = curl_init("http://foo");
$ret = curl_exec($ch);
$err = curl_error($ch);
curl_close($ch);

var_dump($ret, $err);
```

O retorno seria:

``` shell
$ php get.php
bool(false)
string(27) "Could not resolve host: foo"
```

Importante setarmos tudo o que quisermos **antes** de chamar a função <var>curl_close()</var>, pois ela irá realmente &#8220;fechar&#8221; a conexão, invalidando o resource que criamos com a função <var>curl_init()</var>.

E se eu fizer uma requisição válida:

``` bash
ch = curl_init("http://localhost/~wbruno/curl/endpoint.php");
```

O cURL irá retornar os dados que achar lá:

``` bash
$ php get.php
string(3) "GET"
array(0) {
}
bool(true)
```

O true ali, é o resultado do var\_dump() da variavel $ret, que é o retorno do curl\_exec() me informando que tudo ocorreu bem, e a requisição foi feita. O problema desse método que estamos utilizando, é que o **retorno** está sempre sendo &#8220;printado&#8221;, sem que possamos atribui-lo a uma variável.

Para ter esse controle, usaremos uma outra função da lib, chamada **curl_setopt**.

``` php
<?php

$ch = curl_init();
curl_setopt( $ch, CURLOPT_URL, "http://localhost/~wbruno/curl/endpoint.php" );
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true);

$ret = curl_exec($ch);
curl_close($ch);

var_dump($ret);
```

Executando:

``` bash
$ php get.php
string(29) "string(3) "GET"
array(0) {
}
"
```

Agora, vemos que o retorno do curl_exec() foi o conteúdo que o cURL buscou, e não mais um booleano dizendo &#8220;se deu ou não&#8221;. Isso porque utilizamos o **CURLOPT_RETURNTRANSFER**, okay ?

Um exemplo de GET que já fiz com cURL foi [Buscando uma hashtag no search do twitter](http://wbruno.com.br/php/buscando-uma-hash-tag-search-twitter/). Veja como agora tudo faz sentido lá no script, e é bem simples de entender.

Note a sintaxe da função <a href="http://php.net/manual/en/function.curl-setopt.php" rel="nofollow">curl_setopt</a>:

**curl_setopt(<resource>, <option>, <boolean>);**

No terceiro argumento você pode ver tanto true,false ou 1,0.. depende da mania do programador que escreveu, mas ambas as formas significam a mesma coisa: ter ou não tal opção do cURL.

## Response header

Bom, mas nem sempre estamos interessados apenas no retorno (no body do response), mas podemos também querer as meta informações. Para isso, utilizaremos o <var>$info = curl_getinfo($ch);</var>.

``` php
<?php

$ch = curl_init();
curl_setopt( $ch, CURLOPT_URL, "http://localhost/~wbruno/curl/endpoint.php" );
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true);

$ret = curl_exec($ch);
$info = curl_getinfo($ch);
curl_close($ch);

var_dump($info);
```

O retorno do <var>curl_getinfo</var> é um array com informações sobre a resposta, e não o corpo da resposta em si:

``` bash
$ php get.php
array(26) {
  ["url"]=>
  string(42) "http://localhost/~wbruno/curl/endpoint.php"
  ["content_type"]=>
  string(9) "text/html"
  ["http_code"]=>
  int(200)
  ["header_size"]=>
  int(168)
...
  ["local_ip"]=>
  string(9) "127.0.0.1"
  ["local_port"]=>
  int(54098)
}
```

Precisamos disso para por exemplo saber [se um site está ou não no ar](http://wbruno.com.br/php/verificar-com-php-se-o-site-esta-online-no-ar/).

## Follow location

As vezes, ao fazer uma requisição para um site, o site pode ter um redirect, que nos leva para outro endereço, e ai teríamos que fazer uma segunda requisição para aquele endereço, já que o cURL sozinho &#8220;não seguiria&#8221; o redirecionamento.

Então, se fizéssemos uma requisição GET a http://locaweb.com.br, teríamos como resultado o 301 (redirecionamento permanente)

``` bash
$ php get.php
string(246) "<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.locaweb.com.br/default.html">here</a>.</p>
</body></html>
"
```

Felizmente a lib do php possui uma opção para isso <var>curl_setopt( $ch, CURLOPT_FOLLOWLOCATION, 1 );</var> que nos permite receber o resultado mesmo que a requisição sofra um redirect, logo, fazendo assim a requisição:

``` php
<?php

$ch = curl_init();
curl_setopt( $ch, CURLOPT_URL, "http://locaweb.com.br" );
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt( $ch, CURLOPT_FOLLOWLOCATION, true );

$ret = curl_exec($ch);
$info = curl_getinfo($ch);
curl_close($ch);

var_dump($ret);
```

O retorno agora será o html da homepage da Locaweb.

``` bash
$ php get.php
string(78775) "<!DOCTYPE html>
<html dir="ltr" lang="pt-BR">
...</html>
```

Beleza?

Algumas outra opções que podemos usar ainda com GET no cURL são:

**CURLOPT_CONNECTTIMEOUT** - segundos tentando conectar, falha caso não volte antes.

**CURLOPT_TIMEOUT** - segundos até &#8220;falhar&#8221; caso não volte antes do definido.

**CURLOPT_USERAGENT** - você pode &#8220;fingir&#8221; que é um navegador, por exemplo.

Ainda não falei dos outros métodos POST, PUT e DELETE, mas fica para o próximo post, okay ?
