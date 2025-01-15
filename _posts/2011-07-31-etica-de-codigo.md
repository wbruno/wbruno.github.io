---
id: 1231
title: Ética de código
date: 2011-07-31T16:12:56+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1231
permalink: /php/etica-de-codigo/
categories:
  - PHP
tags:
  - boas práticas
---
Bom, hora de começar. A minha proposta foi <a href="https://wbruno.com.br/html/sobre-vc-quer-ler-qual-sua-duvida-js-php-oo-sql-css/" target="_blank">escrever sobre oque vc quer ler</a>.

Este então, é o primeiro post em resposta aos comentários.

<!--more-->

## Use a tag completa de abertura [short open tags]

Isso, tão simples quanto o título.

Prefira usar **<?php** do que usar **<?**.

Afinal, por que depender de uma configuração extra do servidor, quando estamos falando de apenas 3 caracteres a mais?

E nas futuras versões da linguagem (assim como prometido pelos canais oficiais), essa diretiva não será mais configurável ?

Não precisa reescrever todos os teus scripts(se bem que seria bom para você [ctrl+h]), mas de hoje em diante use somente a completa:

``` php
<?php```

## Prefira usar echo em vez de print

Se temos 2 funções(estruturas da linguagem) que fazem exatamente a mesma coisa, então vamos escolher uma delas.

E usar apenas uma. Não tem pq deixar nossos scripts inconsistentes, hora usar uma, hora usar outra.

Já está mais do que provado, que echo é mais rápido que o print.

Use echo.

## Métodos devem retornar coisas

``` php
public function exemplo(){
  echo '....';
}
```

não é majoritário, mas e se eu precisar usar o resultado desse método **exemplo()**, com esse echo ai dentro, eu não consigo.

pois não será mais &#8216;capturável&#8217;. Programe teus códigos de maneiras que eles sejam expansíveis e reaproveitáveis.

## Não se acostume com register_globals

Não faz sentido. O próprio manual oficial dos desenvolvedores alerta sobre isso.

**register_globals**, é uma diretiva da linguagem, que sei lá por que raios foi inventada.

Pode causar diversas dores de cabeça, comportamentos super inesperdados(e difíceis de debugar), além de abrir brechas de segurança no teu sistema.

Desative, use em off.

Não é &#8216;por que existe&#8217;, que deve ser usado. Existem coisas ruins, e nem por isso usamos.

&#8220;Todos os cogumelos são comestíveis, alguns apenas uma vez&#8221;

## Use aspas duplas para delimitar valores de atributos html

Ufa! Isso é arbitrário, e eu decidi usar assim. Escolha minha, e repasso a vocês.

``` html
<a href="link.html" class="link preto" id="link">Clique aqui</a>
```
Hum.. e por que <u>eu escolhi</u> as duplas ?

Vamos ver, os controles de formulários por exemplo:

``` html
<input type="text" name="nome" value="Joana D'arc" />
```
Notou &#8216;a aspa simples&#8217; ali ? [tenho uma amiga com esse nome]

Por outro lado, não existe nenhuma pessoa que tenha uma aspas duplas no nome dela. Mas _apóstrofes_ sim.

Temos o tratamento que vamos fazer, como addslashes(), mas é muito melhor poder receber o dado, do que perder horas debugando, para descobrir que se tivéssemos usado aspas duplas, não teríamos passado por aquilo.

Então, por convenção, uso em tudo. Qualquer atributo html, será delimitado por aspas duplas.

Só dei um exemplo, okay ?

## Indente seu código

Todo mundo fala|deveria recomendar isso. Porém, e **como** você deve fazer isso?

Cara, é questão de gosto. Mas algumas coisas não mudam. Por exemplo, vamos nos ater as linguagens que surgiram com base(possuem estrutura semelhante) na Linguagem C.

Como <a href="http://www.oracle.com/technetwork/java/codeconvtoc-136057.html" target="_blank">Java</a> javascript, php..

### Indentar é necessário

Sim, é melhor olhar para um código organizado, do que para um não.

Você não vai perder tempo se fazer isso. Mas certamente ganhará muito tempo, se precisar reler.

Já encontrei bugs em códigos antigos, e de outros programadores, apenas por indentar eles.

Comece por isso. O importante é a iniciativa.

Com o costume, indentar fará parte de você, e será tão natural, que não precisará pensar, gastar tempo, e não irá te atrapalhar em nada.

### Pule linha depois de ponto e vírgula(;)

Terminou um &#8216;comando&#8217;? pule linha:

``` php
echo 'Oi';
var_dump( $_POST );
```

Melhor de ler do que:

``` php
echo 'Oi';var_dump( $_POST );
```

certo ?

Afinal de contas, temos o ponto e vírgula ali, para terminar aquele comando.

Fica assim então: teve que colocar ponto e vírgula, quebre a linha.

### Sou fãn do TAB

Alguns usam padrões (para mim bizzaros), como &#8216;4 espaços&#8217;. Cara, usa TAB e pronto.

Mas como ?

A indentação horizontal, serve para indicar aos seus olhos como a estrutura é, em questão de &#8216;dependência&#8217;.

Falando de HTML por exemplo, usamos a horizontal, para nos dizer de forma simples: quem é filho de quem.

Olhe só:

``` html
<div id="main">
  <ul>
    <li><a href="link1.html">Link 1</a></li>
    <li><a href="link1.html">Link 1</a></li>
  </ul>
</div>
```

Entendeu ?Só de bater o olho, já sei que tenho um UL filho de uma div#main.

Sendo o LI filho da UL.

### Use comentários realmente significantes

É importante escrever códigos claros, mas nem por isso devemos deixar de comentar.

Existem comentários para todas as linguagens. Use.

``` html
<div id="main">

</div><!-- /main -->
```
Identificando o &#8216;término&#8217; do elemento assim, ganho tempo quando preciso procurar algo.

Não precisa comentar toda a marcação. Eu adoto isso apena em trechos importantes e apenas quando fecho eles.

O início já tá marcado com o ID, ou CLASS. Comenta o fechamento e já tá de bom tamanho.

Assim, quando vc olhar para algo como isso:

``` html
</div>
</div>
</div>
```
Será muito mais simples de saber &#8216;quem fecha quem&#8217;.

### Use o bom senso

Não precisa comentar tudo, por exemplo, não vou comentar isso:

``` php
echo 'Oi';//comando de saída da string Oi```

E nem vou comentar e indentar isso:

``` html
<ul>
    <li>
      <a href="link1.html">Link 1</a>
    </li><!-- /fechando primeiro list item -->
    <li>
      <a href="link1.html">Link 1</a>
    </li>

<!-- /fechando segundo list item -->
```
certo ? era muito simples, posso deixar apenas:

``` html
<ul>
    <li><a href="link1.html">Link 1</a></li>
    <li><a href="link1.html">Link 1</a></li>
```
Afinal, não prejudiquei a visibilidade.

Já que a estrutura era ridicularmente simples. Poupei linhas, sem tornar meu código menos legível.

Quando usar um ou outro ? R: bom senso.

## Use mysqli, abandone mysql_ agora

Pronto. A extensão mysql_ vai acabar. A mysqli é mais rápida. Use.

Prefira a versão orientada, lógico.

### Não superestime

Sério.. eu sei que meus sistemas nunca migrarão de banco de dados.

Só vão usar o SGDB MySQL. Então não tenho nenhum motivo para usar PDO, que iria abstrair os acessos aos dados.

Não tenho, logo, não uso. É questão de briefing. Se a dúvida existir, então considere começar usando PDO.

Mas se não existe, então não infle teu sistema com código inútil.

Existe um grande antagonismo aqui. Depois discutimos melhor.

## Quando|Como usar chaves?

Cara, é o mesmo da indentação horizontal. As chaves existem para delimitar quando uma rotina acabou.

Por exemplo:

``` php
<?php
  if( $var == true )
  {
    while( $dados = $query->fetch() )
    {
      $li .= '';
    }
  }
```

Analise bem. Eu abri a chave embaixo do IF, no mesmo nível horizontal: um TAB.

Poderia ser na frente:

``` php
<?php
  if( $var == true ){
```

Lógico que poderia.

Mas escolha o teu estilo, e siga ele.

Olhe agora o fechamento do IF.

termina no mesmo nível horizontal que abri: um TAB.

Mesma coisa para o while.

Isso facilita a leitura. Quando eu bater os olhos, vou procurar na vertical onde termina esse meu bloco de código.

Se estivesse assim:

``` php
<?php
  if( $var == true )
  {
    while( $dados = $query->fetch() )
    {
      $li .= '';
      }
    }
```

meus olhos continuariam, até tentar achar um }, que estivesse no mesmo nível, para que eu entedesse onde estou de fato fechando o bloco condicional.

E note como o segundo } parece estar fechando o while, enquanto o verdadeiro fechamento do while(), está largado ali, sem nenhum motivo.

E assim cara, se vc já sabe de tudo isso. Parabéns!

Continue fazendo bons códigos. Existem aqueles que não sabem, ou tem dúvidas.

Escrevo para estes também, que apesar das dúvidas querem melhorar, querem aprender.

Ninguém sabe tudo, muito menos eu. Aqui eu apenas compartilho um pouco da minha experiência.

Até mais.
