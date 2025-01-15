---
id: 484
title: Como debugar AJAX com o FireBug ?
date: 2011-04-14T06:55:12+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=484
permalink: /ajax/como-debugar-ajax-firebug/
dsq_thread_id:
  - "2102942588"
categories:
  - AJAX
tags:
  - firefox
---
[<img src="/wp-content/uploads/2011/04/firebug-large.png" alt="" title="firebug-large" width="264" height="211" class="alignleft size-full wp-image-485" />](/wp-content/uploads/2011/04/firebug-large.png)Esse post, é complemento do [Como debugar JavaScript com o Firefox?](https://wbruno.com.br/javascript-puro/como-debugar-javascript-firefox-erros-comuns/).

A maioria das dúvidas que vejo _&#8216;[sobre AJAX](https://wbruno.com.br/ajax/o-que-e-ajax-e-o-que-nao-e/)&#8216;_, na verdade são **sobre Javascript**. Então se você se deparar com **qualquer erro** no console, vá para o outro post, e depois volte.

Vou usar o <a href="http://getfirebug.com/" target="_blank">Firebug</a>, para rastrear nossas requisições AJAX, e então explicar como pode ser simples o desenvolvimento dessa metodologia.

Não gosto nenhum pouco de <a href="http://pt.wikipedia.org/wiki/AJAX_%28programa%C3%A7%C3%A3o%29" target="_blank">copiar definições</a>, então quando eu precisar fazer <a href="http://www.w3.org/TR/XMLHttpRequest/" target="_blank">algo do tipo</a>, apenas jogo o <a href="http://pt.wikipedia.org/wiki/JavaScript" target="_blank">link no meio do texto</a>, e espero que você que estiver lendo, <a href="http://www.devmedia.com.br/post-9498-Desmistificando-o-AJAX-Parte-I.html" target="_blank">clique, leia</a> oque eu quis lhe mostrar, e volte. Ou não, o legal é a opção. Se você não quiser clicar, apenas continue lendo, e eu não te encho de &#8216;[Mais do Mesmo](http://pt.wikipedia.org/wiki/Mais_do_Mesmo)&#8216;.

<!--more-->



Comecemos do simples. O meu foco será ajax, por isso farei tudo com javascript puro, sem plugins, libs ou frameworks. Se você entender o conceito por trás, vendo por de baixo dos panos como estou mostrando, então estará apto a aplicar o mesmo com qualquer falicitador.

**index.html**

``` html
<html>
<head>
  <title>teste</title>
<script type="text/javascript">
function id( el ){
  return document.getElementById( el );
}
function getHTTPObject(){
  if(window.XMLHttpRequest){
    return new XMLHttpRequest();
  }else if(window.ActiveXObject){
    var prefixes = ["MSXML2", "Microsoft", "MSXML", "MSXML3"];
    for(var i = 0; i < prefixes.length; i++){
      try {
        return new ActiveXObject(prefixes[i] + ".XMLHTTP");
      } catch (e) {}
    }
  }
}
var xmlHttp = getHTTPObject();
function envia( file ){
  xmlHttp.open( "GET", file, true );
  xmlHttp.onreadystatechange = function(){
    if (xmlHttp.readyState == 4){
      id('response').innerHTML = xmlHttp.responseText;
    }
  }
  xmlHttp.send( null );
}
window.onload = function(){
  id('enviar').onclick = function(){
    envia( 'process.php' );
  }
}
</script>
</head>
<body>
  <input type="button" name="enviar" id="enviar" value="Enviar xhr" />

  <p id="response"></p>
</body>
</html>
```

**processa.php**

``` php
<?php
  echo 'Beleza, chegou até aqui!';
```

De proprósito, &#8216;errei&#8217;, o nome do arquivo, coloquei <u>process.php</u>, mas na verdade se chama <u>processa.php</u> [terminando com a letra A].

``` js
envia( 'process.php' );
```

Abro o projeto no servidor, clico no botão, e:

[<img src="/wp-content/uploads/2011/04/erro1.jpg" alt="" title="erro1" width="434" height="181" class="aligncenter size-full wp-image-750" srcset="/wp-content/uploads/2011/04/erro1.jpg 434w, /wp-content/uploads/2011/04/erro1-300x125.jpg 300w" sizes="(max-width: 434px) 100vw, 434px" />](/wp-content/uploads/2011/04/erro1.jpg)

## Não funcionou, não fez o que queríamos

[<img src="/wp-content/uploads/2011/04/295qo1-150x98.png" alt="" title="295qo1" width="150" height="98" class="alignleft size-thumbnail wp-image-753" />](/wp-content/uploads/2011/04/295qo1.png)

Erro na tela. Bem simples, e fácil de entender.

Não encontrou o arquivo. Dentre os possíveis motivos, eu poderia ter errado o caminho, o nome do arquivo, não ter me atentado ao CaSe SEnSiTIVe, o arquivo realmente ainda não ter sido criado&#8230;

Só apareceu dessa forma, porque eu pedi:

``` js
id('response').innerHTML = xmlHttp.responseText;
```

Mas nem sempre, é tão simples. Se eu não tivesse colocado o retorno completo dentro dessa DIV, teria sido muito mais _silencioso_. Só nos resta debugar o código.

## Acessar diretamente

Uma forma, é acessar diretamente o arquivo que tentamos chamar. Indo no browser, e jogando a URL lá, crua..

<u>http://localhost/process.php</u>

Bem intuitivo. Esse princípio, demonstra bem que a única mágica do ajax, é &#8216;ir e voltar&#8217; sem refresh. Todo o resto já estamos muito acostumados a lidar.

Mas não é tão prático assim, e ficar acessando várias URLs, pode nos deixar confusos, pois temos que levar em conta o caminho apartir do nosso script.

## Usar alert()s

Nessas horas o **alert()**, é o &#8216;canino fiel'(melhor amigo), dos programadores js.

``` js
if (xmlHttp.readyState == 4){
      alert( xmlHttp.responseText );
      //id('response').innerHTML = xmlHttp.responseText;
    }
```

No alert, vemos:

[<img src="/wp-content/uploads/2011/04/erro22.jpg" alt="" title="erro2" width="516" height="240" class="aligncenter size-full wp-image-751" srcset="/wp-content/uploads/2011/04/erro22.jpg 516w, /wp-content/uploads/2011/04/erro22-300x139.jpg 300w" sizes="(max-width: 516px) 100vw, 516px" />](/wp-content/uploads/2011/04/erro22.jpg)

O mesmo, porém tivemos que &#8216;caçar&#8217; mais, e nem sempre é tão simples assim, podemos nos perder, e gastamos preciosos minutos colocando alert()s em tudo quanto é canto.

## Finalmente, com o Firebug

Nesse momento, é o Firebug que vai nos salvar.

Apertemos F12, aba Rede, depois xhr:

[<img src="/wp-content/uploads/2011/04/firebug.jpg" alt="" title="firebug" width="729" height="143" class="aligncenter size-full wp-image-754" srcset="/wp-content/uploads/2011/04/firebug.jpg 729w, /wp-content/uploads/2011/04/firebug-300x58.jpg 300w" sizes="(max-width: 729px) 100vw, 729px" />](/wp-content/uploads/2011/04/firebug.jpg)Basta dispararmos novamente nossa requisição, clicando no nosso input, e vemos o erro no Firebug:

[<img src="/wp-content/uploads/2011/04/firebug2.jpg" alt="" title="firebug2" width="770" height="343" class="aligncenter size-full wp-image-755" srcset="/wp-content/uploads/2011/04/firebug2.jpg 770w, /wp-content/uploads/2011/04/firebug2-300x133.jpg 300w" sizes="(max-width: 770px) 100vw, 770px" />](/wp-content/uploads/2011/04/firebug2.jpg)Só por esta aba, já temos toda a informação que precisamos, porém as outras, resposta e html, nos dão uma idéia mais detalhada e visual respectivamente do que obtivemos.

Corrigimos o nome do arquivo

``` js
envia( 'processa.php' );
```

No próximo post, vou mostrar mais algumas situações, e a ajuda que o Firebug nos dá.

Comentem. Me digam o que estão achando, me servirá de guia, para saber sobre o que devo escrever.

Até lá! =)
