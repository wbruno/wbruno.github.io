---
id: 1811
title: O elemento HTML body nos nossos sites, como melhor aproveitá-lo.
date: 2012-03-01T12:00:23+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1811
permalink: /css/elemento-body-nos-nossos-sites-como-melhor-aproveita-lo/
dsq_thread_id:
  - "2102513888"
categories:
  - CSS
---
Lhes apresento o elemento **body**:

``` html
<body>
<!-- todo o conteudo do site aqui dentro -->
</body>
```
Todos nós conhecemos. Mas será que estamos utilizando _de verdade_ ele ?

O **body** é o elemento no nosso documento responsável por ser o container <u>de tudo</u> que é conteúdo do site.

Diferente do <head>, oque está dentro do <body> é oque fica/ou ficará disponível para visualização do visitante.

As informações que queremos transmitir. Títulos, Textos, Imagens..

Até aqui, todos nós já usamos o body para isso, mas.. e **o que mais** podemos fazer com ele ?

<!--more-->



Pode parecer absurdo falar isso, mas convém lembrar: o body é uma tag html! E como tal, aceita atributos:

<a href="http://www.w3schools.com/tags/tag_body.asp" target="_blank">http://www.w3schools.com/tags/tag_body.asp</a>

Os mais interessantes, são o **id** e a **class**. Vocês já tinham colocado um desses no body de algum site ?

``` html
<body id="home">
```
## Usar o body com um ID

É uma proposta interessante, e nos ajuda a economizar alguns elementos de estruturação de layout de vez em quando.

Por exemplo, aqueles layouts onde a home do site difere por poucas coisas das páginas internas, como: topo mais alto, rodapé inexistente..

Esse tipo de situação, podemos facilmente resolver usando o atributo ID no body.

Sendo a home, estilizamos o topo diferente doque ele seria nas internas:

``` css
body#home #header { height: 200px; }
#header { height: 100px; }
```

A marcação html fica intacta, evitamos, coisas como: **#header_home**..

E isso nos levará a escrever um css mais bonito também. Afinal, fizemos um condicional no css!

## Usar o body com uma ou mais CLASSes

Hum.. na verdade eu comecei explicando o ID, porém hoje em dia, eu prefiro

``` html
<body class="home">
```
do que com ID.

Pelo simples motivo de poder usar mais de uma. Com classes, temos todos os benefícios que citei do ID:

``` css
body.home #header { height: 200px; }
#header { height: 100px; }
```

E é possível colocar mais de uma, veja:

``` html
<body class="cursos html">
```
A motivação disso, é imaginemos um menu dropdown.

``` html
<li>Cursos
      <ul>
         <li>HTML</li>
         <li>CSS</li>
         <li>JavaScript</li>
      </ul>
    </li>
```

Assim cada página interna, teria uma combinação de class para o body diferente:

class=&#8221;cursos html&#8221;, class=&#8221;cursos css&#8221;, class=&#8221;cursos javascript&#8221;..

A vantagem disso, é que a class=&#8221;cursos&#8221;, é comum a todos eles, e no css podemos fazer facilmente um destaque naquele item de menu, se estivermos dentro de um dos filhos!

Mais uma vez, levamos o poder do css à outro nível!

Tendo a class **html**, **css**.. e sabendo que cada página interna terá somente um título H1, podemos por exemplo, fazer o H1 ser azul na página de HTML, ser vermelho na página de css, e ser de qq outra cor por padrão, nas páginas em que não definirmos nada.

``` css
.html h1 { color: #00f; }
.css h1 { color: #f00; }
h1 { color: #000; }
```

A grande sacada disso é não precisarmos adicionar nada mais no html, além das respectivas classes no body.

## O body é pai de todo mundo

Conhecendo o efeito cascata do css, e sabendo que tudo o que o visitante verá está dentro do body do documento, é melhor usar a herança do css para definir os padrões do site, como:

``` css
body { font-size: 12px; font-family: Tahoma, sans-serif; color: #333; }
```

E porque o body ? pq afinal, todos os elementos posteriores herdarão dele, e isso tudo com uma especificidade bem baixa. Então não precisamos brigar para sobrescrever estilos.

Deve ter ficado implícito, mas quero ressaltar com uma ressalva: todos os elementos, menos os de formulário.

Por algum motivo que desconheço, input, select e textarea, não herdam &#8216;naturalmente&#8217; definições de fonte declaradas no body.

``` css
body, input, select, textarea {
    font-size: 12px; font-family: Tahoma, sans-serif; color: #333;
}
```

Com isso, cobrimos todas as tags, e não estragamos as definições padrões como, <small> terá uma fonte menor que o body, <h1> continua com uma fonte maior.. por esse motivo que não uso o seletor global * para esse trabalho.

Ele aplica a todos os elementos, mas de forma &#8220;forçada&#8221;, elemento a elemento. E não por herança como ocorre qndo trabalhamos com o body.

A idéia é brigarmos menos com nós mesmos. E só sobrescrever poucas propriedades.

Isso é ótimo por uma outra questão: não corremos o risco de &#8220;esquecer&#8221; de alguma tag, visto que com uma declaração simples, e aproveitando a herança do css, nós atingimos ela.

Por este motivo não gosto daqueles css resets gigantescos e milagrosos, entretanto isso é assunto para um próximo post.

## O body aceita css!

Sabe aquele fundo do topo com degradê, e aquela linha do header que vai de uma ponta a outra do browser? (100% width), então..

aplica como background do body!

Simples assim. Descartamos a necessidade de um #wrap_header, e jogamos em uma só imagem como background do body, pois ele mesmo já tem de graça para gente, 100% de largura da viewport.

Esse é apenas um exemplo, para tentar &#8220;abrir&#8221; a mente. As possibilidades são muitas.

Às vezes precisamos rever coisas &#8220;óbvias&#8221; ou &#8220;básicas&#8221;, pois podem fazer coisas impressionantes.

Que tal ?
