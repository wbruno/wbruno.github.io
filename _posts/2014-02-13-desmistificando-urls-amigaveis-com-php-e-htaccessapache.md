---
id: 2827
title: Desmistificando URLs amigáveis com php e htaccess (apache)
date: 2014-02-13T08:00:09+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=2827
permalink: /php/desmistificando-urls-amigaveis-com-php-e-htaccessapache/
categories:
  - PHP
tags:
  - apache
  - htaccess
---
Boas!!

A quantidade de pessoas que perguntam como fazer URLs amigáveis no forum.imasters é enorme. Seja em WebStandars, SEO ou php, a dúvida é sempre a mesma.

<!--more-->



É simples de fazer. Basta ir com calma e procurar entender tudo o que você está fazendo.

## A reescrita é para o servidor, e não para você

As suas tags de link e a forma com que vc abrirá os seus conteúdos, você mesmo terá que alterar. Então onde você usava:

``` html
<a href="?page=contato">Contato</a>
```
Agora passará a escrever:

``` html
<a href="/contato">Contato</a>
```
E se precisar de mais parâmetros, indique-os:

``` html
<a href="/edit/user/1">Editar usuário</a>
```
Isso significa, que o servidor irá receber a requisição em <var>/contato</var>, ou <var>/edit/user/1</var>, e com a RewriteEngine, irá traduzir para o que vc realmente queria dizer, que era <var>?page=contato</var>, ou <var>?action=edit&model=user&id=1</var>.

Fica muito mais bonito depois de reescrito, mas para isso é necessário que as suas regras traduzam o amigável para a querystring.

## Estude expressões regulares

O arquivo .htaccess que é uma &#8220;configuração&#8221; externa do apache, acessível da sua aplicação, desde que liberado na configuração do servidor, te possibilita a configurar diversas coisas do ambiente. E as RewriteRules fazem ainda mais sentido, e serão mais poderosas se vc souber Expressões Regulares.

## Ahh página em branco, erro 500

São duas as possibilidades, ou a sua hospedagem não suporta configuração via htaccess (muito difícil), ou vc cometeu algum erro de sintaxe, e quebrou o servidor, lembra que o htaccess é um arquivo externo de configuração do apache ? pois é, faça algo errado, que vc terá um 500 na tela.

Não é necessário re-startar o servidor após escrever suas regras, mas cuidado com o cache do teu browser, pois uma regra bem escrita pode parecer ainda não estar funcionando, se o chrome cachear a requisição, e continuar te devolvendo erro.

## Mãos na massa

Comece, e para isso vc precisa &#8220;ligar&#8221; a engine de reescrita:

```RewriteEngine On```

Lembrando que ela já deve estar instalada no apache, a linha acima, apenas &#8220;avisa&#8221; que vc irá utilizá-la. O meu arquivo para saber se está funcionando e receber a requisição será o **teste.php**, com o seguinte conteúdo:

``` php
<?php
var_dump($_GET);
```

O que eu quero é acessar a url <u>/edit/user/1</u>, e receber o seguinte no GET:

```array(3) {
  ["action"]=>
  string(4) "edit"
  ["model"]=>
  string(4) "user"
  ["id"]=>
  string(1) "1"
}
```

Ok, vamos lá.

Primeiro devo identificar as partes da minha URL. <u>/edit/user/1</u> é composto por um grupo de letras, seguido por uma barra, outro grupo de letras, outra barra e um número.

Simples!

A Expressão Regular para isso é: `([a-z]+)\/([a-z]+)\/([0-9]+)`

Básico não ? apenas escapei as barras com barras invertidas, para não quebrar a sintaxe da ER.

O que eu quero realmente receber na aplicação é `teste.php?action=$1&model=$2&id=$3`, sendo cada $n, o número do grupo em sequência ao que foi casado pela ER anterior.

### Sintaxe da regra

Bem simples, é composta por 3 partes:

```RewriteRule <regular expression> <url to translate> [FLAGs]```

Aplicando ao caso acima, fica:

```RewriteRule ^([a-z]+)\/([a-z]+)\/([0-9]+)$ teste.php?action=$1&model=$2&id=$3 [NC,L]```

Adicionei ^ no início da ER, para indicar que a requisição deve **começar** com aquele padrão, e **$** para indicar que ali a ER **acaba**, e não deve casar nada mais diferente disso.

Utilizei as flags [NC] para ignorar sensitive case, então se a url for: <u>http://wbruno.com.br/EdIt/uSeR/1</u> a ER continua funcionando, e [L] para dizer que se a ER casar, essa é a última regra a ser testada, e deve processá-la, e não continuar procurando mais ERs e ver se outra abaixo dela também casa.

E para <u>/contato</u>, a minha ER fica simplesmente:

```RewriteRule ^([a-z]+)\/?$ teste.php?page=$1 [NC,L]```

note que os padrões não são conflitantes, então podem coexistir no mesmo htaccess.

Funcionando:

<http://wbruno.com.br/scripts/edit/user/1>

<http://wbruno.com.br/scripts/fale-comigo>

## Não redirecione tudo para a index

Alguns frameworks e alguns preguiçosos têm a mania de fazer coisas parecidas com isso:

```RewriteRule . /index.php [L] #retirei esse do wordpress :p```

e ai parsear toda a URL do lado da aplicação.

Eu não aconselho, pois vc terá deixado tudo mais lento, uma vez que um trabalho que deveria ser feito no servidor, foi delegado a aplicação, e agora você é dependente de reescrita, e se por algum motivo ela não for suportada na hospedagem, não irá funcionar sem ela.

Dá para entender o motivo do WP utilizar, pois são tantos padrões, e tantas opções de URL amigável que vc pode configurar, que para a app é até mais simples parsear nela, mas na sua, evite usar. Eu pelo menos prefiro trabalhar assim. =)

E ai ? entendeu #comofas?

## Complemento

<a href="http://moz.com/blog/htaccess-file-snippets-for-seos" rel="nofollow">http://moz.com/blog/htaccess-file-snippets-for-seos</a>
