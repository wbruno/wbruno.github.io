---
id: 895
title: 'Nem só de <div> vive um desenvolvedor FrontEnd'
date: 2011-05-17T07:00:07+00:00
author: wbruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=895
permalink: /opiniao/nem-so-de-div-vive-um-desenvolvedor-frontend/
dsq_thread_id:
  - "2104736074"
categories:
  - Opinião
---
Pois é meus caros!

Não é _&#8216;tão novidade assim&#8217;_, mas as vezes parece!

Okay, abandonamos(nem todos), o recorte de layouts em <table>, (sabemos|deveriamos saber) que **tableless** é um termo perigoso se for mal interpretado&#8230;. **menos** tabelas, não quer dizer, nunca usar. A tag de tabela do HTML possui utilidade. Existem lugares e momentos corretos para usá-las.

Cada <td> é uma célula, <tr>são as linhas, os <th> são as células de título, o <tbody> é o corpo dos dados tabulares, contém os dados propriamente ditos, o <thead> deve delimitar o cabeçalho&#8230; o <tfooter>&#8230;

Enfiim, ainda as usamos. Nos perguntamos se devemos ou não usar a tag <table> e as filhas desta.

Porém, e as <div>s ?

<!--more-->



Você nunca se perguntou se deveria ou não usar uma div ? Naquele contexto ?

Nunca parou para pensar, &#8216;se fazia sentido&#8217; ?

Repita estes questionamentos com a tag <span>.

É fácil usar essas tags sem semântica. Entretanto não tinha mesmo nenhuma semântica aquele lugar onde enfiamos elas ?

Alguns códigos que vejo, me dão vontade de clamar por um movimento **DivLess**.

``` html
<div id="menu">
    <ul>
         <li>..```

Tirando raros casos, e efeitos &#8216;complicados&#8217;, precisava da div ? Não poderia ter feito simplesmente e apenas:

``` html
<ul id="menu">
     <li>..```

hein?!

Ou então

``` html
<div id="logo"><img src="....```

> _Quase tão feio quanto fazer um website inteiro com table, é desperdiçar marcação HTML vazia de semântica._

A tag <img /> aceita e muito bem o atributo ID.

Para alguns pode parecer absurdo, porém já vi:

``` css
span.bold { font-weight: bold; }
```

Para os que não entenderam o que eu quis dizer, ou não acham isso um soco no próprio estômago, lhes digo: é absurdo ! Esse tipo de declaração deve soar absurda.

O <br /> é outra tag muito mal usada.

Representa uma quebra, deve ser usada para tal, e não para &#8216;dar espaçamento&#8217;.

Espaço é estilização, logo, <u>margin</u>, <u>padding..</u> são as formas corretas de configurar um espaçamento.

As tags são HTML, ou seja, estão na camada de conteúdo, e não de apresentação. Devem ser usadas para informar o que aquele conteúdo representa, e não para _espaçar_, ou <span style="color: #f0f;">colorir </span>, por exemplo. Por este motivo que a tag <font> foi <del datetime="2011-05-13T22:16:53+00:00">banida</del> depreciada.

Não devemos misturar as camadas.

Olhe para o teu conteúdo, e deixe que ele te responda o que ele é. O próprio conteúdo, deve lhe dizer qual tag é a mais apropriada.

É uma frase de alguém, um depoimento, respostas de uma entrevista, uma citação de um cliente ? que tal a tag <cite> ?

Melhor do que um <span> com uma class, certo ?

Lá no rodapé, ou no formulário de contato, precisa colocar o endereço e telefone. Hum&#8230; tag <address>, que tal ?

Um disclaimer, pos scriptum, merece menos atenção do visitante. Jogue um <small> !

E as tags <sub>, e <sup> ? melhor do que se matar com regras no css, para fazer um <span chegar naquele efeito.

Só nisso, economizamos declarações de classes, percebeu ?

Dava para fazer tudo que falei só com <div> e <span>, na verdade, dá para fazer um site inteiro, com tudo apenas usando um desses dois, porém não é praticável, certo ?

A primeira consequência são diversas linhas a mais no css, e diversas declarações de atributos, classes, ids..

Olhe por outro lado agora.

No primeiro momento, deixamos nosso conteúdo nos contar o que ele era, para sabermos qual tag usar.

Agora olhemos o código pronto, sem ler o conteúdo das strings, apenas vendo as tags. Aqui, nossas tags devem ser capazes de nos contar que tipo de informação elas carregam, e o que elas estão fazendo ali na página.

Perceba a &#8216;loucura&#8217; disso.

Pense, reflita. =)

## <a href="http://pt.wikibooks.org/wiki/Web_para_curiosos/A_web_do_lado_cliente/Linguagens_de_marca%C3%A7%C3%A3o/(X)HTML/Referencias_da_linguagem/Elementos" target="_blank">Lista de TAGS HTML</a>
