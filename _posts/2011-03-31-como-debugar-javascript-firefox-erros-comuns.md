---
id: 432
title: 'Como debugar JavaScript com o Firefox ? &#8211; erros comuns'
date: 2011-03-31T09:11:00+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=432
permalink: /javascript-puro/como-debugar-javascript-firefox-erros-comuns/
dsq_thread_id:
  - "2101203753"
categories:
  - Javascript
tags:
  - firefox
---
[<img src="/wp-content/uploads/2011/03/firefox_ie-150x150.jpg" alt="" title="firefox_ie" width="150" height="150" class="alignright size-thumbnail wp-image-433" />](/wp-content/uploads/2011/03/firefox_ie.jpg)Notei uma coisa bem interessante no relatório do Google Analytics: mais da metade dos meus visitantes navegam com o Firefox. Até seco, sem nenhum plugin ele é ótimo.

E aqui começa a minha dica: &#8220;Pelo menos para FrontEnd prefira a Raposa&#8221;.

(conheço ótimas ferramentas de outros navegadores DragonFly, FireBugLite.. mas não é a idéia falar delas agora).

Posso dizer que javascript é uma linguagem de _&#8216;erros silenciosos&#8217;_.

Não é como o php, onde os erros disparam **Notice, Warning, Fatal Error**&#8230; na tela, indicando exatamente a linha e motivo.

Ou então o asp, que trunca por completo a exibição, e te mostra apenas aqueles códigos de difícil entendimento.

<!--more-->



JavaScript e CSS são sutis. Ou simplesmente não funciona, ou para de funcionar de repente, ou apresenta um comportamento inesperado.

Para quem está começando isso é o caos, e alguns tomam até birra da linguagem, quando na verdade apenas não sabem usar as ferramentas corretas.

[<img src="/wp-content/uploads/2011/03/firefox1.jpg" alt="" title="firefox1" width="188" height="68" class="alignleft size-full wp-image-436" />](/wp-content/uploads/2011/03/firefox1.jpg)

Eu mesmo ( e acredito que boa parte dos desenvolvedores ) comecei meus primeiros **alert()**&#8216;s, no famigerado Internet Explorer.

O console de erros do IE, sempre foi ruim.

## O console de erros

Já [Resolvi] vários tópicos no subfórum de js do iMasters, apenas contando sobre a exitência do **Ctrl + Shif + J**.

[<img src="/wp-content/uploads/2011/03/firefox2.jpg" alt="" title="firefox2" width="338" height="249" class="aligncenter size-full wp-image-437" srcset="/wp-content/uploads/2011/03/firefox2.jpg 338w, /wp-content/uploads/2011/03/firefox2-300x221.jpg 300w" sizes="(max-width: 338px) 100vw, 338px" />](/wp-content/uploads/2011/03/firefox2.jpg)

Vou listar os **erros mais comuns**, que vejo o pessoal cometendo, e mostrar como solucioná-los.

Feliz, feliz, alegre e pimpão, tentamos escrever nosso primeiro alert:

``` html
<html>
<head>
<script type="text/javascript">
  ae( oi );
</script>
```

Salva o código, abre no navegador, aperta F5 e **nada**. Frustante&#8230;

<h2 style="margin-top: 30px">
  Erro: 1a &#8211; blablabla is not defined
</h2>

Vamos lá, <u>não funcionou</u>. Os mais experientes já devem ter notado o motivo, mas grande parte dos iniciantes, e até nós mesmos, num momento de correria, podemos deixar passar esse tipo de erro.

**Ctrl + Shift + J** e:

[<img src="/wp-content/uploads/2011/03/firefox3.jpg" alt="" title="firefox3" width="676" height="197" class="aligncenter size-full wp-image-438" srcset="/wp-content/uploads/2011/03/firefox3.jpg 676w, /wp-content/uploads/2011/03/firefox3-300x87.jpg 300w" sizes="(max-width: 676px) 100vw, 676px" />](/wp-content/uploads/2011/03/firefox3.jpg)

Vale sempre lembrar clicar no &#8216;Limpar&#8217;, antes de executarmos a nossa página, para assim, não nos depararmos com erros antigos, ou de outros sites.

Queríamos, que aparecesse um alert() na tela, com a palavra <u>oi</u>, mas nada aconteceu.

O interpretador, acusou que <u>oi</u> não foi definido, ou seja, ele procurou por **algo**, chamado <u>oi</u>, e não encontrou.

Ora, se queríamos a _palavra_ <u>oi</u>, e isso deve nos remeter a **string**, deveriamos ter usado aspas.

``` js
ae( 'oi' );
```

Agora funciona.

<h2 style="margin-top: 30px">
  Erro: 1b &#8211; blablabla is not defined
</h2>

``` js
alerts( 'oi' );
```

[<img src="/wp-content/uploads/2011/03/firefox4.jpg" alt="" title="firefox4" width="624" height="45" class="aligncenter size-full wp-image-439" srcset="/wp-content/uploads/2011/03/firefox4.jpg 624w, /wp-content/uploads/2011/03/firefox4-300x21.jpg 300w" sizes="(max-width: 624px) 100vw, 624px" />](/wp-content/uploads/2011/03/firefox4.jpg)

Mesmo erro, idêntico. Agora, vendo o **blablabla is not defined**, sabemos que o **blablabla**, foi uma function que tentamos usar, mas que não existe.

<h2 style="margin-top: 30px">
  Erro: 1c &#8211; escrito de forma incorreta
</h2>

Lembremos que **JaVaSCrIPt** é **CaSE SeNSiTiVe**, então não podemos fazer:

``` js
alerT( 'oi' );//com o T em maiúsculo.
```

O erro vai ser o mesmo, existe a function nativa **alert()**, mas não a **Alert()**, nem a **ALERT()**&#8230;

Essa mesma regra se aplica a variaveis, objetos..

<h2 style="margin-top: 30px">
  Erro: 1d &#8211; $ is not defined
</h2>

Esse acontece muito, pois a lib precisa ser incorporada ao documento, antes de qualquer código que seja escrito com a sintaxe do jQuery.

$() é a função chave e básica da lib. Com outros FWs, acontecem erros semelhantes.

É o mesmo problema do **Erro 1b**, mas aqui geralmente acontece ou porque não fizeram o download do arquivo, ou o caminho para a lib no atributo src=&#8221;&#8221; da tag <script> está incorreto.

Erros triviais, de sintaxe.

<h2 style="margin-top: 30px">
  Erro 2a: &#8211; missing } after function body
</h2>

``` html
<script type="text/javascript">
  function w(){
    //faz qq coisa
  </script>
```

Deveria ser evidente..

Esquecemos de fechar a function, erro de sintaxe.

``` html
<script type="text/javascript">
  function w(){
    //faz qq coisa
  }
  </script>
```

<h2 style="margin-top: 30px">
  Erro 3a: &#8211; Valor do atributo type inválido
</h2>

``` html
<script type="Javascript">
  alert( 'Oi' );
  </script>
```

Já vi isso acontecer. Não aparece nada no console, mas não funciona nenhuma rotina dentro dessas tags.

o valor do atributo type esté incorreto. Deve ser **text/javascript**, isso e somente isso.

<h2 style="margin-top: 30px">
  Erro 3b: &#8211; Declarar atributo language
</h2>

``` html
<script language="Javascript">
```

Simplesmente é desnecessário hoje em dia.

Incrível ver como a galera usa sem saber o motivo. O atributo **language**, era usado bem antigamente, para indicar a versão do javascript, em que o script foi codificado. [1.2, 1.0.. 1.5&#8230;]. Hoje em dia, todos os browsers modernos, até o ie6(apesar das diferenças de interpretação), suportam a versão 1.5 da linguagem.

Então o **language** é completamente desnecessário. Existem documentos da w3c, falando da depreciação desse atributo.

Apenas o **type**, é suficiente e obrigatório (ainda não levo em conta HTML5)

<h2 style="margin-top: 30px">
  Erro 4a: &#8211; missing ) after argument list
</h2>

``` js
alert( 'Oi' ;
```

Aqui vemos o quão eficiente é o console do Firefox:

[<img src="/wp-content/uploads/2011/03/firefox12.jpg" alt="" title="firefox12" width="622" height="93" class="aligncenter size-full wp-image-447" srcset="/wp-content/uploads/2011/03/firefox12.jpg 622w, /wp-content/uploads/2011/03/firefox12-300x44.jpg 300w" sizes="(max-width: 622px) 100vw, 622px" />](/wp-content/uploads/2011/03/firefox12.jpg)

Que mensagem linda! Fácil de entender, e aponta exatamente onde está o problema.

``` js
alert( 'Oi' );
```

<h2 style="margin-top: 30px">
  Erro 5a: &#8211; missing ; before statement
</h2>

Pois é, apesar de não ser obrigatório na sintaxe, esquecer de &#8216;_terminar os comandos_&#8216;, pode gerar falhas.

Por isso, que sempre que termino um comando, coloco um ponto e vírgula.

[<img src="/wp-content/uploads/2011/03/firefox13.jpg" alt="" title="firefox13" width="622" height="93" class="aligncenter size-full wp-image-448" srcset="/wp-content/uploads/2011/03/firefox13.jpg 622w, /wp-content/uploads/2011/03/firefox13-300x44.jpg 300w" sizes="(max-width: 622px) 100vw, 622px" />](/wp-content/uploads/2011/03/firefox13.jpg)

``` html
alert( 'Oi' )alert( 'Oi2' )```

e não é nenhuma situação tão especial assim. Basta imaginar, que passamos o nosso script por um minify que removeu os espaços.

Se tivéssemos sidos rígidos com a sintaxe, mesmo não sendo obrigatório, não teríamos esse problema.

<h2 style="margin-top: 30px">
  Erro 5b: &#8211; missing ; after for-loop initializer
</h2>

O console é muito bom, mas não é cigano.

``` js
for( var prop iN caixa )
```

o mesmo ocorre para **for( var prop i caixa )**

[<img src="/wp-content/uploads/2011/03/firefox14.jpg" alt="" title="firefox14" width="619" height="92" class="aligncenter size-full wp-image-449" srcset="/wp-content/uploads/2011/03/firefox14.jpg 619w, /wp-content/uploads/2011/03/firefox14-300x44.jpg 300w" sizes="(max-width: 619px) 100vw, 619px" />](/wp-content/uploads/2011/03/firefox14.jpg)

erramos a sintaxe, o console apontou, mas também ele não tem como <u>adivinhar exatamente</u> o que queríamos fazer.

Achou que estávamos tentando a sintaxe completa do for, por isso reclamou do ;

``` js
for( var prop in caixa )
```

<h2 style="margin-top: 30px">
  Erro 6a: &#8211; Usando document.write em um lugar nada a ver
</h2>

``` html
<head>
  <script type="text/javascript">
  function escreve()
  {
    document.write( 'Lugar nada a ver' );
  }
  </script>
</head>
<body>
  <input type="button" name="escreve" value="escreve" onclick="escreve();" />
</body>
```

Nada no console, mas gera um comportamento super esquisito. Escreve, mas some o botão, a página fica carregando infinitamente..

Não faz sentindo nenhum usar o document.write assim. Veja que esse método nativo da linguagem, tenta dar o output, no mesmo lugar que vc o chamar.

Chamei uma função no evento do botão, e ai o .write, tentou escrever &#8216;no meu botão&#8217;. Não faz o menor sentido.

Use qualquer um dos outros métodos que &#8216;escrevem&#8217;, e direcione o output para outro lugar.

<h2 style="margin-top: 30px">
  Erro: 7a(Alerta) &#8211; elemento referenciado pelo ID/NAME
</h2>

``` html
<div id="teste"></div>
  <script type="text/javascript">
    teste.innerHTML = 'wbruno';
  </script>
```

[<img src="/wp-content/uploads/2011/03/firefox5.jpg" alt="" title="firefox5" width="718" height="166" class="aligncenter size-full wp-image-440" srcset="/wp-content/uploads/2011/03/firefox5.jpg 718w, /wp-content/uploads/2011/03/firefox5-300x69.jpg 300w" sizes="(max-width: 718px) 100vw, 718px" />](/wp-content/uploads/2011/03/firefox5.jpg)

Okay, até funciona. Mais isso pode ocasionar bizarrices no nosso script.

Note que coloquei as tags <script>, após o elemento.

Se eu tivesse colocado elas **antes** de declará-lo, ai aconteceria o erro 1a, pois navegador não acharia nada chamado <u>teste</u>

<h2 style="margin-top: 30px">
  Erro: 7b &#8211; elemento referenciado pelo ID/NAME
</h2>

Aparece frequentemente em rotinas envolvendo formulários.

``` html
<form name="form1">
    <input type="text" name="nome" value="wBruno" />
  </form>
  <script type="text/javascript">
    alert( document.form1.nome.value );
  </script>
```

..

Vamos fazer melhor, declarar um atributo ID único pro elemento, e usar o standard **getElementById()**

``` html
<form>
    <input type="text" name="nome" id="nome" value="wBruno" />
  </form>
  <script type="text/javascript">
    alert( document.getElementById('nome').value );
  </script>
```

<h2 style="margin-top: 30px">
  Erro: 8a &#8211; blablabla is null
</h2>

``` html
<script type="text/javascript">
    document.getElementById('pergunta1').innerHTML = 'wbrunO';
  </script>
</head>
<body>
  <div id="pergunta1">Pergunta1</div>
```

Salvamos, Ctrl+Shift+J, clicamos no Limpar, F5, e:

[<img src="/wp-content/uploads/2011/03/firefox6.jpg" alt="" title="firefox6" width="622" height="51" class="aligncenter size-full wp-image-441" srcset="/wp-content/uploads/2011/03/firefox6.jpg 622w, /wp-content/uploads/2011/03/firefox6-300x24.jpg 300w" sizes="(max-width: 622px) 100vw, 622px" />](/wp-content/uploads/2011/03/firefox6.jpg)

Uê, ta tudo certo. Usamos o método correto, declaramos nosso ID, único, e nos voltou um erro pior ainda!

O problema, foi que **não esperamos**, o elemento existir, ou seja, o DOM carregar, e tentamos usá-lo.

Daí, o getElementById(), retornou um null, e esse null não possui nenhuma propriedade, por isso o erro.

<h2 style="margin-top: 30px">
  Erro 8b &#8211; blablabla is null
</h2>

``` js
var pergunta1 = document.getElementById('pergunta1');
  pergunta1.innerHTML = 'wbrunO';
```

[<img src="/wp-content/uploads/2011/03/firefox7.jpg" alt="" title="firefox7" width="622" height="51" class="aligncenter size-full wp-image-442" srcset="/wp-content/uploads/2011/03/firefox7.jpg 622w, /wp-content/uploads/2011/03/firefox7-300x24.jpg 300w" sizes="(max-width: 622px) 100vw, 622px" />](/wp-content/uploads/2011/03/firefox7.jpg)

Mesmo erro, porém agora não está tão fácil de notar de onde vem, e precisamos rastrear, até encontrar onde criamos o &#8216;algo&#8217;, chamado pergunta1.

Para esperar o documento carregar, ou o elemento existir, podemos fazer:

``` js
window.onload = function(){
    document.getElementById('pergunta1').innerHTML = 'wbrunO';
  }
```

, ou seja, esperar que o evento .onload do objeto window dispare a nossa function.

<h2 style="margin-top: 30px">
  Erro 8c &#8211; blablabla is null
</h2>

``` html
<script type="text/javascript">
  window.onload = function(){
    for( var i=1; i<=4; i++ ){
      document.getElementById('pergunta'+i).innerHTML = 'wbrunO';
    }
  }
  </script>
</head>
<body>
  <div id="pergunta1">Pergunta1</div>
  <div id="pergunta2">Pergunta2</div>
  <div id="pergunta3">Pergunta3</div>
</body>
```

Executou sem problemas, fez o que deveria, mas é sempre bom olhar o console, mesmo que &#8216;esteja tudo aparentemente bem&#8217;.

[<img src="/wp-content/uploads/2011/03/firefox8.jpg" alt="" title="firefox8" width="622" height="51" class="aligncenter size-full wp-image-443" srcset="/wp-content/uploads/2011/03/firefox8.jpg 622w, /wp-content/uploads/2011/03/firefox8-300x24.jpg 300w" sizes="(max-width: 622px) 100vw, 622px" />](/wp-content/uploads/2011/03/firefox8.jpg)

Erro de lógica, tento chegar até um &#8216;pergunta4&#8217;, mas só existe até o pergunta3. Precisa corrigir a condição de parada do loop.

<h2 style="margin-top: 30px">
  Erro 9a: &#8211; Não tem erro, apenas não funciona!
</h2>

``` html
<script type="text/javascript">
  window.onload = function(){
    document.getElementById('pergunta1').innerHTML = 'wbrunO';
  }
  </script>
</head>
<body>
  <div id="pergunta1">Pergunta1</div>
  <div id="pergunta1">Pergunta2</div>
  <div id="pergunta1">Pergunta3</div>
```

Acreditando ter aprendido a lição, o [CQP](http://www.wbruno.com.br/2011/03/29/diferenca-entre-cara-programa-um-programador/) foi lá, e <u>duplicou o ID</u>.

Rodando o script cima, vemos que o texto da primeira DIV foi substituido, mas das outras não. [comportamento inesperado]

Pois é, não pode. Em um documento, cada ID deve ser um identificador único.

Não mostrou erro no console, porém esse tipo de erros, podemos pegar no <a href="http://validator.w3.org/" target="_blank">validador w3c</a>.

<h2 style="margin-top: 30px">
  Erro 10a:(Alerta) &#8211; Declaração ignorada
</h2>

Fizemos algo errado. Esse erro é muito sutil, mas pode infernizar bastante. Por isso que sempre é bom, já começarmos nossos scripts com um DOCTYPE

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <script type="text/javascript">
  window.onload = function(){
    document.getElementById('caixa').style.backgroundColor = '#f0f';
    document.getElementById('caixa').style.height = '140';
  }
  </script>
</head>
<body>
  <div id="caixa">Texto</div>
</body>
</html>
```

[<img src="/wp-content/uploads/2011/03/firefox9.jpg" alt="" title="firefox9" width="622" height="48" class="aligncenter size-full wp-image-444" srcset="/wp-content/uploads/2011/03/firefox9.jpg 622w, /wp-content/uploads/2011/03/firefox9-300x23.jpg 300w" sizes="(max-width: 622px) 100vw, 622px" />](/wp-content/uploads/2011/03/firefox9.jpg)

Precisamos lembrar que a declaração da **unidade de medida**, é obrigatória quando usamos DTD.

O erro não aparecia antes do DTD, mas o problema não é o DTD, foi termos esquecido de colocar o <u>px</u> ali.

Correto:

``` js
document.getElementById('caixa').style.height = '140px';
```

<h2 style="margin-top: 30px">
  Erro 11a: &#8211; setting a property that has only a getter
</h2>

Violando encapsulamento? oO Sim meus caros, javascript tem um &#8216;Q&#8217; de orientação a objetos.

``` html
document.getElementById('caixa').offsetTop = '40%';
```

[<img src="/wp-content/uploads/2011/03/firefox10.jpg" alt="" title="firefox10" width="622" height="48" class="aligncenter size-full wp-image-445" srcset="/wp-content/uploads/2011/03/firefox10.jpg 622w, /wp-content/uploads/2011/03/firefox10-300x23.jpg 300w" sizes="(max-width: 622px) 100vw, 622px" />](/wp-content/uploads/2011/03/firefox10.jpg)

… exatamente oque está dizendo, **.offsetTop**, é apenas um getter, logo não podemos atribuir nada a essa propriedade.

<h2 style="margin-top: 30px">
  Erro 12a: &#8211; Usando atributos que o objeto não possui
</h2>

Não disparou nenhum erro pra mim, mas dá para usarmos coisas que não existem.

``` html
<script type="text/javascript">
  window.onload = function(){
    document.getElementById('caixa').value = 'hein?!';
  }
  </script>
</head>
<body>
  <div id="caixa">Texto</div>
```

O atributo .value, é próprio dos elementos de formulário do html, e não das DIVs.

Simplesmente não aconteceu nada.

Para descobrirmos o que existe ou não naquele objeto, podemos fazer:

``` html
<script type="text/javascript">
  window.onload = function(){
    var caixa = document.getElementById('caixa');
    for( var prop in caixa )
      document.getElementById('caixa').innerHTML += prop+'<br />';
  }
  </script>
</head>
<body>
  <div id="caixa"></div>
```

A saída é bem extensa e interessante.

<h2 style="margin-top: 30px">
  Erro 13a: &#8211; queríamos somar, mas juntou
</h2>

Outro erro comportamental.

``` html
<html>
<head>
  <script type="text/javascript">
  function id( el ){
    return document.getElementById( el );
  }
  window.onload = function(){
    id('calcular').onclick = function(){
      id('resultado').value = id('valor').value + id('valor2').value;
    }
  }
  </script>
</head>
<body>
  <form action="" method="post">
    Valor: <input type="text" name="valor" id="valor" value="55" /><br />
    Valor2: <input type="text" name="valor2" id="valor2" value="11" /><br />
    Resultado: <input type="text" name="resultado" id="resultado" /><br />

    <input type="button" name="calcular" id="calcular" value="Calcular" />
  </form>
</body>
</html>
```

55 mais 11 igual 5511.

O navegador entendeu como string, e concatenou as duas strings. Esperávamos que saisse 66, mas saiu &#8217;55&#8217;+&#8217;11&#8217;

as funções **parseInt()** e **parseFloat()**, estão ai para nos ajudar.

``` js
id('resultado').value = parseInt( id('valor').value) + parseInt( id('valor2').value );
```

<h2 style="margin-top: 30px">
  Erro 14a: &#8211; blablabla is not a function
</h2>

``` js
var t = 0;
t();
```

Um pouco complicado de reproduzir.. e existem várias situações onde podemos ver esse erro.

Ali no caso, eu tinha uma variavel, e tentei usar ela como se fosse uma função.

<h2 style="margin-top: 30px">
  Erro 15a: &#8211; useless set(Timeout|Interval) call ( missing quotes around argument?)
</h2>

[<img src="/wp-content/uploads/2011/03/a.jpg" alt="" title="a" width="562" height="46" class="aligncenter size-full wp-image-822" srcset="/wp-content/uploads/2011/03/a.jpg 562w, /wp-content/uploads/2011/03/a-300x24.jpg 300w" sizes="(max-width: 562px) 100vw, 562px" />](/wp-content/uploads/2011/03/a.jpg)

O código foi:

``` js
function atrasada(){
  alert( 'Demorei 1 segundo para ser chamada' );
}
window.setTimeout( atrasada(), 1000 );
```

Veja que deveriamos ter omitido os parênteses, ou então, ter colocado a função **atrasada()**, entre aspas. Pois dessas 2 formas, não estariamos &#8216;já disparando&#8217; a função.

=) Por enquanto é isso galera.

Conforme eu for lembrando, adiciono aqui.
