---
id: 1595
title: Afinal, o que são funções ?
date: 2012-01-02T12:18:12+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1595
permalink: /php/afinal-sao-funcoes/
categories:
  - PHP
---
[Função](http://pt.wikipedia.org/wiki/Fun%C3%A7%C3%A3o)
  
&#8220;Funções descrevem relações matemáticas entre dois objetos, x e f(x) = y&#8221;.
  
&#8220;Onde o objeto x é o **argumento** da função f, e y é o objeto dependente de x&#8221;.

&#8220;Sejam A e B conjuntos não vazios, qualquer relação de A e B, que associa cada elemento de A a um único elemento de B, chamamos de função de A em B&#8221;.

Ops.. blog errado ?
  
<!--more-->


  
Não não! Aqui eu falo sobre programação, e não por descuido comecei falando matematicamente.
  
Em programação também temos o conceito de funções.

E nesse nosso mundo também, enviamos argumentos, e obtemos um resultado:

<pre name="code" class="php">echo ola( 'Bruno' ); // "Olá, Bruno!"
echo ola( 'uiLL' ); // "Olá, uiLL!"</pre>

Cada valor que eu envio para a função **ola()**, me retorna uma saída diferente.

Usamos funções em programação, para &#8220;encapsular&#8221; rotinas. Seria muito chato se tivéssemos que repensar/reescrever uma certa coisa, cada vez que fossemos querer usá-la.

Por exemplo:

<pre name="code" class="php">&lt;?php
$id = isset( $_GET['id'] ) ? $_GET['id'] : null;
$ctrl = isset( $_GET['ctrl'] ) ? $_GET['ctrl'] : null;
</pre>

Por menor que seja, **qualquer duplicação** de código deve nos incomodar.
  
Em vez de ficar colocando os ifs ternários, um embaixo do outro, para quantas variaveis da query string eu quiser resgatar, eu posso melhorar o script assim:

<pre name="code" class="php">&lt;?php
function getGet( $key ){
    return isset( $_GET[ $key ] ) ? $_GET[ $key ] : null;
}
$id = getGet('id');
$ctrl = getGet('ctrl');;
</pre>

Ganhamos bastante com isso. Imagine que eu vá aplicar um filtro, em todas as variaveis que receber, até para evitar alguns injections:

<pre name="code" class="php">&lt;?php
function getGet( $key ){
    return isset( $_GET[ $key ] ) ? filter( $_GET[ $key ] ) : null;
}
function filter( $str ){
    $str = addslashes( $str );//aqui vem a implementação do filtro
    return str_replace( '#', '', $str );
}
$id = getGet('id');
$ctrl = getGet('ctrl');;
</pre>

Bem limpo ne?!
  
Só alterei a função getGet(), e adicionei a filter() nela. Bem melhor doque:

<pre name="code" class="php">&lt;?php
$id = isset( $_GET['id'] ) ? filter( $_GET['id'] ) : null;
$ctrl = isset( $_GET['ctrl'] ) ? filter( $_GET['ctrl'] ) : null;
</pre>

ou então:

<pre name="code" class="php">&lt;?php
$id = isset( $_GET['id'] ) ? addslashes( str_replace( '#', '', $_GET['id'] ) ) : null;
$ctrl = isset( $_GET['ctrl'] ) ? addslashes( str_replace( '#', '', $_GET['ctrl'] ) ) : null;
</pre>

## return ou echo ?

Vou criar uma função para saber quanto é 10% de qualquer valor. (poderia ser algo bem mais complicado).

<pre name="code" class="php">&lt;?php
function dezPorcento( $val ){
    echo $val*0.1;
}</pre>

E então posso usar essa function sempre que eu precisar:

<pre name="code" class="html">&lt;strong>Economize: &lt;?php dezPorcento(1000); ?> na compra da TV&lt;/strong>
&lt;strong>Economize: &lt;?php dezPorcento(25); ?> na compra desse pen drive&lt;/strong>
</pre>

Mas e se eu precisar desse mesmo resultado em &#8220;varios locais&#8221; ?

<pre name="code" class="html">&lt;strong>TV: de 1000 por apenas: &lt;?php echo 1000-dezPorcento(1000); ?>&lt;/strong>
</pre>

o &#8220;echo&#8221; que coloquei no meio da função, já me impediria de fazer essa conta. Pois já fiz a saída do dado. E não tenho mais como &#8220;reutilizar&#8221;.

O correto seria:

<pre name="code" class="php">&lt;?php
function dezPorcento( $val ){
    return $val*0.1;
}</pre>

Dessa forma sim, consigo fazer a conta.
  
Note que, em vias de regra, **sempre use return** em suas funções.(salvos alguns casos especiais)

Funções nos ajudam a organizar o código, a reutilizar rotinas(evitam duplicação), a subdividir problemas(podemos usar várias funções para resolver um problema grande, qnto menor cada função, mais reutilizável ela será).