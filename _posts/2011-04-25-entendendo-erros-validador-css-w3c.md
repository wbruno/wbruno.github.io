---
id: 582
title: Entendendo erros do validador CSS do w3c
date: 2011-04-25T07:00:53+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=582
permalink: /css/entendendo-erros-validador-css-w3c/
dsq_thread_id:
  - "2103329089"
categories:
  - CSS
tags:
  - validador
  - w3c
---
Já escrevi sobre os [erros do validador w3c](https://wbruno.com.br/html/entendendo-erros-validador-html-w3c/), e expliquei como [entender e resolver para validar](https://wbruno.com.br/html/entendendo-erros-validador-html-w3c-parte-2/), o que ele retorna. Para terminarmos o assunto da validação, vamos para o <a href="http://jigsaw.w3.org/css-validator/" target="_blank">validador de css</a>.

<!--more-->

## Erro 1a: A propriedade blablabla não existe : valor

Digitamos errado. CSS não é uma linguagem CaSE SeNSiTiVe, porém nomes de propriedades inválidos são ignorados, e não validam.

``` css
inPUT{ heiGHtt: 22px; }
```

Para ficar mais bonito e organizado, seletores, e valores sempre em minúsculo, okay ?

## Erro 1b: A propriedade -blablabla não existe : valor

Uso de código proprietário, como os prefixos: **-moz, -khtml, -webkit-&#8230;**. Vem acontecendo muito, com a galera querendo usar o suporte que alguns browsers já estão dando a **css3**.

## Erro 1c: A propriedade blablabla não existe em CSS nível 2.1 mas existe em : valor

De novo, mais um erro ao tentar usar **css3**. O validador foi projetado para css2.1 ainda. Portanto, os valores &#8216;liberados&#8217; de css3, que não existiam em css2.1 não validam.

``` css
box-shadow:rgba(200,200,200,1) 0 4px 18px;
text-shadow:#fff 0 1px 0;
```

## Erro 1d: A propriedade _blablabla não existe : valor

Famigerados hacks para ie. Adição do underline na frente da propriedade.

Não use esse tipo de hack! Antes de pensar em fazer regras especificas para &#8216;tal navegador&#8217;, veja se não é o teu código que está confuso, ou gerando essa diferença.

``` css
_background: ...```

## Erro 2a: Pseudo-elemento ou pseudo classe :blablabla desconhecido

**css3** novamente.. seletores poderosos.. mas ainda não podemos usá-los de forma simples e crossbrowser.

``` css
.elemento:disabled {}
```

## Erro 3a: Erro de parseamento blablabla

Escrito de forma incorreta, ou regra proprietária. Aqui vale ressaltar, que é possível resolver qualquer efeito de layout, usando apenas regras válidas e homologadas pela w3c. Não da mesma forma, porém com o mesmo resultado visual.

## Erro 3b: Erro de parseamento blablabla

``` css
#meuid.umclass {}}
```

Sobrou um fecha chaves ali. Só resta usar o validador para nos indicar a linha, e corrigirmos o problema.

## Erro 3c: Erro de parseamento *blablabla

``` css
*padding-top: 0; ```

Outro hack para IE. Se for a última alternativa, uma folha externa dentro de um comentário condicional, é muito mais elegante e simples de dar manutenção do que esse tipo de hack.

## Erro 4a: Erro de valor : blablabla somente 0 pode ser um(a) length. Você deve declarar uma unidade de medida para o número : valor

&#8216;Esqueci&#8217;, de colocar a unidade de medida:

``` css
input{ height: 22; }
```

## Erro 4b: Erro de valor : blablabla é uma cor inválida 3 ou 6 números hexadecimais são requeridos valor

&#8216;Posso&#8217;, declarar meus elementos como quiser, pois vale lembrar que css também podem ser atrelados a documentos XML. No entanto, os valores devem ser escritos corretamente.

``` css
wb { color: #ff; }
```

## Erro 4c: Erro de valor : blablabla Erro de parseamento valor

&#8216;Esqueci&#8217; os dois pontos, entre o seletor e o valor nessa regra.

``` css
input { height 22px; }
```

## Erro 5a: Erro de parseamento blablabla

Eu costumo fazer isso. Quando quero testar como ficará o elemento &#8216;sem uma propriedade&#8217;, eu quebro a sintaxe dela, colocando um espaço no meio do seletor, invalidando assim aquela linha, já que se restringirá até o ponto e virgula declarado.

``` css
input { hei ght: 22px; }
```

Eu sei que eu poderia usar a sintaxe de comentário do css, para anular dada regra, ou ainda editar em &#8216;tempo real&#8217; com o Firebug, porém as vezes é mais simples e direto esse tipo de intervenção.

Ainda assim, fica a dica de algo que pode ser digitado &#8216;errado&#8217;, e cause esse erro visto aqui.

## Erro 6a: Erro de valor : blablabla tentativa de encontrar um ponto-e-vírgula antes da propriedade. Coloque o ponto-e-vírgula

Se estivermos na ultima regra de um dado seletor, o ponto e vírgula é optativo, porém não vejo o menor sentido em escolher não declará-lo. A &#8216;economia&#8217; de digitação, é tão ínfima, que na minha opinião, vale mais apena, sermos rígidos com a sintaxe, e depois não precisarmos quebrar a cabeça, caso tenhamos que adicionar novas regras embaixo, e alguma delas não funcionar.

``` css
input {
   height: 22px
   color: #fff;
}
```

## Erro 7a: Seletor ID inválido [#blablabla]

``` css
#12id {}
```

os valores dos atributos HTML, como class e IDs, não devem começar com números por exemplo, ou outro caracter inválido.

## Erro 7b: Em CSS1, um nome de classe pode começar com um dígito (&#8220;.55ft&#8221;), a menos que seja uma dimensão (&#8220;.55in&#8221;). Em CSS2, tais ids são parseadas como dimensões desconhecidas (com a finalidade de permitir adições futuras de novas unidades). Para que &#8220;.blablabla&#8221; seja uma classe válida, CSS2 requer que o primeiro dígito seja escapado &#8220;blablabla&#8221; [blablabla]

``` css
.12class {}
```

Mesma coisa do anterior, porém a mensagem agora é mais completa. Comecemos os valores de IDs e classes, com letras.

## Erro 8a: Alerta Algumas cores background-color e color

``` css
input {
background : #000;
color : #000;
} ```

Mesma cor para fonte, e para fundo, ou seja invisível e ilegível. Gera um alert do validador.

Devemos lembrar que nosso documento precisa ser acessível, mesmo que as imagens não carreguem.

Conforme eu lembrar de mais algum, adiciono aqui.

> _O importante não é validar._

O verdadeiro motivo de validarmos nossa folha de estilos, é para descobrirmos falhas e erros que demorariamos mais para encontrarmos a olho nu sozinhos. Muitos desses erros, podem gerar comportamentos inesperados, como não funcionar esta ou a próxima regra..

Usemos os validadores a nosso serviço, para nos auxiliar no desenvolvimento do dia a dia.
