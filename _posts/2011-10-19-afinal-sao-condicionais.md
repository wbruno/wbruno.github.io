---
id: 1515
title: Afinal, o que são condicionais ?
date: 2011-10-19T17:35:00+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1515
permalink: /php/afinal-sao-condicionais/
categories:
  - PHP
---
Recebi uma sugestão de post, no mínimo curiosa..

[<img src="/wp-content/uploads/2011/10/Screen-shot-2011-10-19-at-3.56.26-PM.png" alt="" title="Screen shot 2011-10-19 at 3.56.26 PM" width="573" height="377" class="aligncenter size-full wp-image-1516" srcset="/wp-content/uploads/2011/10/Screen-shot-2011-10-19-at-3.56.26-PM.png 573w, /wp-content/uploads/2011/10/Screen-shot-2011-10-19-at-3.56.26-PM-300x197.png 300w" sizes="(max-width: 573px) 100vw, 573px" />](/wp-content/uploads/2011/10/Screen-shot-2011-10-19-at-3.56.26-PM.png)

Caramba.. como assim ?

<!--more-->

## O que realmente são

Condicionais são **estruturas de controle** do <u>fluxo</u> dos nossos programas.

A grosso modo, se uma certa **condição** for satisfeita, então o bloco de código relativo e encadeado a essa condição deve ser executado.

``` php
<?php
date_default_timezone_set('America/Sao_Paulo');

if( date('G')>6 && date('G')<=12 )
   echo 'Olá, ainda está de dia !';
else if( date('G')>12 && date('G')<=18 )
    echo 'Caramba! Olha que horas são! já devo lhe dizer Boa Tarde!';
else if( date('G')>18 && date('G')<=23 )
    echo 'Tá de noite!';
else if( date('G')>23 && date('G')>=6 )
    echo 'Ta de "madrugada" ainda.. vai dormir!';
```

Dependendo da hora do dia(no servidor), será exibida uma mensagem ao visitante.

``` php
<?php
while( true ){
    echo 'Eu gosto de SODA Limonada!';
}
```

hehe, famoso loop infinito.. sim, eu realmente adoro Soda.

## Parece simples

Mas não é tão simples assim.. por mais que estejamos acostumados a programar, existem alguns &#8220;erros&#8221; que podem ser cometidos.

## DRY! DIE!

A primeira forma incorreta de usar condicionais, na verdade não é ditada apenas no uso dessas estruturas, mas sim <a href="https://wbruno.com.br/php/boas-praticas-de-programacao-filosofias-de-desenvolvimento/" target="_blank">como um todo nessa ciência</a>.

Não se repita!

Vale para tudo no desenvolvimento, porém com condicionais é ainda um pouco mais gritante:

``` php
<?php
    if( isset( $_GET['user'] ) && $_GET['action']=='editar' )
    {
        //faz outra coisa
    }
    else if( isset( $_GET['user'] ) && $_GET['action']=='excluir' )
    {
        //faz algo
    }
    else if( isset( $_GET['user'] ) && $_GET['action']=='inserir' )
    {
        //faz algo
    }
    //.. continua..
```

Assim que batermos o olho no código, nossos olhos de programadores devem ser capazes de fazer mais ou menos isso aqui:

[<img src="/wp-content/uploads/2011/10/Screen-shot-2011-10-19-at-4.35.43-PM.jpg" alt="" title="Screen-shot-2011-10-19-at-4.35.43-PM" width="624" height="230" class="aligncenter size-full wp-image-1531" srcset="/wp-content/uploads/2011/10/Screen-shot-2011-10-19-at-4.35.43-PM.jpg 624w, /wp-content/uploads/2011/10/Screen-shot-2011-10-19-at-4.35.43-PM-300x110.jpg 300w" sizes="(max-width: 624px) 100vw, 624px" />](/wp-content/uploads/2011/10/Screen-shot-2011-10-19-at-4.35.43-PM.jpg)

Ou seja, &#8220;borrei mentalmente&#8221; o que variava alí, e encherguei uma duplicação de código, uma repetição de um teste.

A resposta, para evitar essa repetição, é reagrupar logicamente os testes. Estou demonstrando esse caso simples, para exemplificar, e também ser mais fácil de mostrar aqui no post. O <del datetime="2011-10-19T18:44:03+00:00">correto</del>melhor seria:

``` php
<?php
    if( isset( $_GET['user'] )
    {
        if( $_GET['action']=='editar' )
        {
            //faz outra coisa
        }
        else if( $_GET['action']=='excluir' )
        {
            //faz algo
        }
        else if( $_GET['action']=='inserir' )
        {
            //faz algo
        }
    }//fecha if get user
    //.. continua..
```

bem mais legível ne?!

Rapidamente conseguimos dizer que todas as ações, dependem da existência do parâmetro user na superglobal $_GET.

O resultado é o mesmo do primeiro código, só que agora está muito melhor em performance e legibilidade.

## Não ser capaz de pensar no inverso

As estruturas de testes estão diretamente ligadas a lógica. As vezes é muito difícil testarmos uma coisa, e passamos horas e horas tentando.

Mais fácil seria inverter, e testar primeiro o contrário.

As minhas entradas possíveis são: bla, ble, bli, blo e blu.

O meu programa precisa fazer algo se entrar bla, ble, bli OU blo. E outra coisa se entrar blu.

O primeiro rascunho seria:

``` php
<?php
if( $ext=='bla' || $ext=='ble' || $ext=='bli' || $ext=='blo'  ){
    //tal coisa
}
else { //blu
    //outra coisa
}
```

O seguinte resulta na mesma coisa:

``` php
<?php
if( $ext=='blu'  ){
    //outra coisa
}
else { //bla, ble, bli ou blo
    //tal coisa
}
```

O código ficou bem mais simples ne?!

Primeiro resolvi a excessão e depois apliquei ao restante. Esse tipo de situação é mais frequente do que imaginamos.

O indicativo que podemos resolver pensando o contrário, é qndo estivermos nos diante de uma condicional absurdo e complexo. Quase sempre, existe uma forma mais simples de resolver.

## Não enchergar os padrões

Podemos patinar e ficar horas tentando escrever complexos testes, se não formos capazes de identificar padrões nos testes, e até quem sabe, utilizarmos uma Expressão Regular para simplificar as coisas.

``` php
<?php
if( $q=='Localweb' || $q=='Loucaweb' || $q=='Lokaweb' || $q=='LokaWeb' ){
    //se o visitante queria digitar Locaweb, mas errou algum pedaço..
    echo 'Você tentou digitar Locaweb, mas digitou: '.$q;
}
```

Existem as mais diversas e loucas variações para as tentativas, porém todos concordam que começa com L, e termina com web.

Além disso, case insensitive não deve importar, pois seria absurdo testarmos todas as possibilidades.

Uma expressão regular tira isso de letra:

``` js
/l[a-z]+web/i```

Depois vá refinando.

Citei algumas aplicações com if(), porém o mesmo princípio pode ser aplicado a switch case(prefira esse do que uma cadeia de if/elses), while()&#8230; enfim, essas estruturas condicionais que testam algo, para então fazer tal coisa.

E você ? tem mais alguma dica ? ou situação inusitada/complicada com condicionais ?
