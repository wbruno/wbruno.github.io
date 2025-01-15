---
id: 3005
title: 'Object Oriented CSS - A teoria das classes reutilizáveis - OOCSS'
date: 2013-05-31T07:00:30+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=3005
permalink: /css/object-oriented-css-a-teoria-das-classes-reutilizaveis-oocss/
categories:
  - CSS
tags:
  - boas práticas
  - oo
  - tableless
---
[<img src="/wp-content/uploads/2013/05/css.jpg" alt="css" width="800" height="312" class="aligncenter size-full wp-image-3006" srcset="/wp-content/uploads/2013/05/css.jpg 800w, /wp-content/uploads/2013/05/css-300x117.jpg 300w" sizes="(max-width: 800px) 100vw, 800px" />](/wp-content/uploads/2013/05/css.jpg)

## Por quê ?

A base da teoria oocss é algo que todos nós depois de alguns layouts recortados já devemos ou deveríamos nos ter deparado e notado: **duplicação de estilos**.

Uma sensação de _dejavu_, onde elementos diferentes e não relacionados, começam a declarar alguns **estilos semelhantes**, como cor de fundo, estilo de borda, família ou cor da fonte.. coisas desse tipo.

<!--more-->

O Diego Eis escreveu um ótimo post sobre isso: [OOCSS ou CSS do jeito certo](http://tableless.com.br/oocss-ou-css-do-jeito-certo/#.UaVp-2TwIyA). Então não vou gastar muitas linhas com o motivacional.

## Como fazer

Tente pensar em pequenas funcionalidades úteis para seus elementos. A forma de uso é adicionar classes que definam poucos estilos, e assim formar um todo.


``` html
<a href="" class="btn btn-hire btn-big">Contratar</a>
```
Apenas trocando e combinando as classes dos elementos conseguimos montar um botão com os estilos padrões da classe <var>.btn</var>, da cor que foi padronizada para todos os botões de contrate na classe <var>.btn-hire</var>, e grande, pois é apenas isso que a classe <var>.btn-big</var> faz.

Note que não devemos usar seletores com nomes de tag no nosso css, pois isso trava a implementação, e nos impossibilitaria de por exemplo, fazer isso:


``` html
<input type="submit" class="btn btn-hire btn-big" value="Contratar" />
```
E do ponto de vista conceitual não é nada absurdo termos um <var>input[type=&#8221;submit&#8221;]</var> com os mesmos estilos de uma tag <var><a></var>, pois o importante é a função do elemento. Os 2 levam o visitante a contratar nossos produtos, então precisam ter estilos iguais. E se conseguirmos usar o mesmo css para tal, melhor ainda para nós.

## Outro exemplo

Falar de botões é simples, é um dos exemplos mais básicos quando estamos falando sobre css. Mas imagine que existe um padrão de raio em todos as caixas de conteúdo do nosso site. Ter que codificar isso, já que ainda não temos variáveis nativas no css, não é legal.

Se o designer fizer o site com varias caixinhas de 10px de border-radius, e depois pedir para diminuirmos todas as caixas para 7px, sair editando varios elementos é muito chato e nada prático. Para resolver isso, podemos fazer:

``` css
.radius { border-radius: 10px; }
```

E ai, sair usando nos elementos que tiverem esse estilo:


``` html
<section id="comments" class="radius"></section>
<div id="box-call" class="radius"></div>

<span class="text radius"></span>
```

Isso realmente facilita a manutenção do projeto como um todo.

## Evite seletores com vírgulas

Sair colocando vírgulas nos seletores, é uma forma de não duplicar linhas do css:

```#comments,
#box-call,
.text {
    /**/
}
```

Mas não é legal para a manutenção do sistema. Se algum outro elemento for utilizar esses estilos desse bloco acima, teríamos que sair procurando onde do nosso css fizemos esses seletores com vírgula, para incluir mais uma vírgula e o novo seletor.

É muito mais interessante fazer a classe <var>.radius</var>, e apenas utilizar ela no html desse novo elemento.

## Bom senso

Crie suas classes utilitárias conforme você for precisando delas, não infle o seu projeto com coisas que &#8220;talvez&#8221; vc precise, que &#8220;talvez&#8221; vc vá usar algum dia. Modularize os estilos que realmente forem ser reutilizados.

Sei que incomoda criar &#8220;classes funcionais&#8221;, aquelas como <var>.link-gray</var>, ou <var>.font16</var>, mas vamos usar o bom senso galera. Pense bem e só some classes que valem a pena serem somadas.

Não é nada inovador, e como eu disse no começo do post, já sabemos fazer isso faz tempo.

Ainda assim, é bacana relembrarmos e revermos alguns conceitos, pois devemos sempre buscar melhorar e aperfeiçoar nossas técnicas. Só assim produziremos códigos com mais qualidade e com melhor manutenção.
