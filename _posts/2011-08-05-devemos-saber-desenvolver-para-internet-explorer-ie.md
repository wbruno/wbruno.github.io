---
id: 1234
title: 'Devemos saber desenvolver para internet explorer [ie]!'
date: 2011-08-05T03:29:27+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1234
permalink: /css/devemos-saber-desenvolver-para-internet-explorer-ie/
dsq_thread_id:
  - "2102368267"
categories:
  - CSS
---
Quero explicar aos &#8216;mais novos&#8217;, o porquê **devemos** saber desenvolver FrontEnd para esse famigerado navegador.

Mais especificamente, para o motor de renderização no qual ele se baseia.

<!--more-->



Beleza, o Firefox é lindo, o Chrome é uma maravilha, mas é preciso deixarr claro o que é: **obrigação** do desenvolvedor(nós), e o que é: que o browser deveria de fato fazer.

## Corrigir marcação

É um recurso muito interessante, poupa os visitantes de ver muitos sites quebrados. Pois diversos browsers modernos, através de complicadas rotinas, corrigem literalmente uma marcação HTML incorreta. Os motores praticamente adivinham o que o desenvolvedor queria fazer, e faz por eles!

Olha que beleza, podemos ser preguiçosos e ruins, que o FF vai dar um jeito e corrigir!

Balela, se toca! caia na real!

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Box Model</title>
<style type="text/css">
* { margin: 0; padding: 0; }
</style>
</head>
<body>
  <div id="main">
    <h1>Titulo

  </div>
  <p>continua normal</p>
</body>
</html>
```

Problema: não fechei a tag h1. O FF fechou pra mim. O IE não.

[<img src="/wp-content/uploads/2011/08/ff2.jpg" alt="" title="ff2" width="160" height="227" class="alignleft size-full wp-image-1245" />](/wp-content/uploads/2011/08/ff2.jpg)

[<img src="/wp-content/uploads/2011/08/ie2.jpg" alt="" title="ie2" width="270" height="219" class="alignright size-full wp-image-1244" />](/wp-content/uploads/2011/08/ie2.jpg)

<p style="clear: both;">
  Isso é obrigação sua! Faça correto! Não seja dependente de um workaround de terceiros. Aqui que entra a maravilha. O internet explorer não corrije, não arruma teus erros(na maioria das vezes)!
</p>

É praticamente como a sua mãe: vai te apontar todos os teus erros, apontando bruscamente o que vc fez, detonando todo o resto do documento.

Eu pessoalmente acho isso ótimo. Aqui começamos a destinguir os bons dos ruins(devs). O mínimo do mínimo é fazer uma marcação consistente, e válida. Obrigação sua.

## Atributo incorreto

Erro tosco, absurdo de sintaxe HTML!

``` js
<div id="main">
    <h1 id="titulo>Titulo</h1>

  </div>
  <p>continua normal</p>
```

Visualização:

[<img src="/wp-content/uploads/2011/08/ff3.jpg" alt="" title="ff3" width="128" height="233" class="alignleft size-full wp-image-1250" />](/wp-content/uploads/2011/08/ff3.jpg)[<img src="/wp-content/uploads/2011/08/ie3.jpg" alt="" title="ie3" width="140" height="174" class="alignright size-full wp-image-1249" />](/wp-content/uploads/2011/08/ie3.jpg)

<p style="clear: both;">
  IE fudeo tudo. FF corrigiu. Quem tá errado ? O FF e nós mesmos. Afinal fizemos errado.
</p>

> _Na minha opinião, o IE está certo, pois mostrou errado algo que fizemos errado._

## Box Model

Cara, essa eu acho absurda. Exemplo rápido:

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Box Model</title>
<style type="text/css">
* { margin: 0; padding: 0; }
#main {
  width: 400px;
  height: 70px;
  background: #ff0;
}
.content {
  width: 200px;
  height: 100px;
  background: #f0f;
}
</style>
</head>
<body>
  <div id="main">
    <div class="content"></div>
  </div><!-- /main -->
</body>
</html>
```

Explicando o que eu fiz: **.content** é filha da **#main**

Porém, notem que o height da filha é maior que o height da mãe. (erro de lógica isso)

Aqui que o &#8216;bug do ie&#8217; é explicado: _o ie trata height como min-height_

[<img src="/wp-content/uploads/2011/08/ff-300x198.jpg" alt="" title="ff" width="290" height="191" class="alignright size-medium wp-image-1238" srcset="/wp-content/uploads/2011/08/ff-300x198.jpg 300w, /wp-content/uploads/2011/08/ff.jpg 447w" sizes="(max-width: 290px) 100vw, 290px" />](/wp-content/uploads/2011/08/ff.jpg)

[<img src="/wp-content/uploads/2011/08/ie-300x159.jpg" alt="" title="ie" width="290" height="152" class="alignleft size-medium wp-image-1239" />](/wp-content/uploads/2011/08/ie.jpg)

<p style="clear: both;">
  Notem como no Firefox, acontece oque pedimos: a #main (que é mãe), com menos altura que a filha.<br /> Ridículo! Erramos, deveria estar errado! Não foi bug do ie, foi bug do desenvolvedor !
</p>

## Value de input centralizado verticalmente

``` html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Box Model</title>
<style type="text/css">
input {
  height: 40px;
}
</style>
</head>
<body>
  <input type="text" name="" />
</body>
</html>
```

E ai ? pq o FF fez bonitinho e mandou pro centro ?

eu não disse nada pra ele. Não informei um line-height de mesmo valor do height.

São pequenas coisas. Mas que podem nos dar grandes dores de cabeça. O único intuito desse post, é te fazer refletir.

Não estou defendendo o ie. Só quero expor, que muitos dos erros e das dores de cabeça que enfrentamos todos os dias, provém dos nossos próprios erros. E não da engine do navegador.

> _Culpe a si mesmo, antes de culpar os outros!_
