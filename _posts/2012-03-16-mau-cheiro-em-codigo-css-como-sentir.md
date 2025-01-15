---
id: 1875
title: 'Mau cheiro em código css - Como sentir'
date: 2012-03-16T10:53:32+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1875
permalink: /css/mau-cheiro-em-codigo-css-como-sentir/
categories:
  - CSS
tags:
  - boas práticas
---
Não quero falar apenas como &#8220;melhorar&#8221; o seu código.

Muitos já escreveram sobre, e você já deve estar cansado de ouvir as mesmas coisas:

-> Use algum CSS reset;

-> Ordem alfabética (?) [eu prefiro ordenar por &#8216;_tipo&#8217;_];

-> Use regras resumidas(agrupamento): margin-top: 10px; margin-bottom: 5px;.. seria melhor: margin: 10px 0 5px;

-> Comente para organizar;<!--more-->



-> Identar elementos encaixados (?) [particularmente não sou muito fãn disso] [<a href="http://tableless.com.br/6-estrategias-para-melhorar-a-organizacao-do-seu-css-2/" target="_blank">fonte</a>]

-> Dividir de forma lógica, algo como: estrutura, classes utilitárias, módulos&#8230;

-> Um único padrão de nomenclatura \[camelCase, dash-case, underscore, ou&#8230;\] (seja consistente);

-> Escolha bons nomes; (meu post anterior fala um pouco sobre isso)

-> Uma Regra = Uma linha … Múltiplas regras = Múltiplas linhas; [<a href="http://www.webdesignblog.com.br/desenvolvimento/10-dicas-para-escrever-melhor-seu-css/" target="_blank">fonte</a>]

-> Indice [um comentário no início mostrando os grupos de seletores que vc usou];

-> Mais de uma folha de estilos [se o site for &#8220;grande&#8221; isso vale a pena] [<a href="http://algoritmizando.com/desenvolvimento/como-escrever-um-css-melhor/" target="_blank">fonte</a>]

E outras tantas parecidas, derivadas, e com nomes diferentes dessas acima.

Quero falar sobre o **mau cheiro**. Sobre quando é que o seu código deve lhe parecer &#8220;estranho&#8221;, &#8220;incorreto&#8221; apesar de funcionar.

Afinal é necessário identificar que algo está errado para poder corrigir

## Quando você notar duplicação de código:

Por exemplo, você possui uma área parecida com isto:

``` css
#box_telefone {
   background: #fff; border-radius: 10px;
   float: left;
   width: 100px; height: 50px;
}
#box_email {
   background: #fff; border-radius: 10px;
   float: left;
   width: 200px; height: 75px;
   margin: 20px;
   color: #ddd;
}
```

Ambos são &#8220;caixas&#8221; no layout, e possui estilos(formatações básicas) semelhantes. Eu sugiro fazer algo assim:

``` css
.box { background: #fff; border-radius: 10px; }
.fleft { float: left; }
#box_telefone {
   width: 100px; height: 50px;
}
#box_email {
   width: 200px; height: 75px;
   margin: 20px;
   color: #ddd;
}
```

Note que também retirei o float dos seletores, e fiz uma &#8220;classe utilitária&#8221; para ele.

Dessa forma posso sei lá, usar o #box_telefone na esquerda na home, e na direita na página de contato.

Existem técnicas e &#8220;boas horas&#8221; para separar, vá com cuidado.

## Quando tiver muitos seletores com vírgulas

Algo assim:

``` css
#box_telefone,
#box_email { /* .. */ }
```

Isso &#8220;tende&#8221; a crescer. Tende a sair do controle. Então se você precisar de mais uma caixa com estilos parecidos, vai lá e adiciona outro seletor com vírgula ai.

Nesse caso, aplique a dica de cima. Vale mais a pena criar classes &#8220;modulares&#8221;, do que ir listando IDs para um mesmo conjunto de regras.

## Quando a cascata CSS não estiver sendo utilizada

Um outra forma de evitar duplicação de código css, é aproveitar bem a cascata css. Coisas como: definir o <var>font-family</var> para o seletor <var>body</var>, que então os demais elementos herdarão dele.

Mas não definir tag por tag, pois quando você precisar sobrescrever, ficará brigando por especificidade.

Use a cascata, porém tente ser genérico. Bem pouco específico, ou nada(se não, não é cascata).

## Quando um efeito/posicionamento estiver lhe dando muito trabalho

Se você entender corretamente o boxmodel, e souber utilizar todas as propriedades css, conhecendo tudo o que elas fazem(de acordo com as especificações), então aquele posicionamento que está te dando mais trabalho, te fazendo usar 10-15 regras, pode estar errado.

É bem sutil isso. Mas existem várias formas de se fazer uma mesma coisa.

Se você começar a fazer uma que não está dando certo, e for ficando cada vez mais complexo, então repense e tente fazer de outra forma.

Às vezes basta mudar um pouco o outro elemento que estava antes na marcação, ou posicionar de uma outra maneira este problemático, e tudo se resolve.

Posso dizer que quanto mais complicado ficar a sua estratégia para resolver, mais chances você tem de encontrar incompatibilidade entre os browsers.

A minha regra aqui é:

> Deve primeiro fazer sentido para você mesmo.

Digo isso, pois muitos desenvolvedores saem jogando propriedades, &#8220;até dar certo&#8221;. Na base do chute. Não é assim que se desenvolve &#8220;bem&#8221;.

Consigo me lembrar destas por hora. Conhece mais alguma forma ?

Me conte nos comentários.
