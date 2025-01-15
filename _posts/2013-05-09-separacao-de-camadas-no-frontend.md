---
id: 2928
title: Separação de camadas no FrontEnd
date: 2013-05-09T09:57:53+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=2928
permalink: /css/separacao-de-camadas-no-frontend/
categories:
  - CSS
  - HTML
  - Javascript
tags:
  - boas práticas
  - tableless
---
Separar a VIEW do MODEL e não misturar as regras de negócio com os CONTROLERs há muito tempo já fazem parte das preocupações e boas práticas adotadas pelos programadores back end, mas e dos desenvolvedores frontend ?

A separação de camadas onde cada componente possui uma responsabilidade bem definida, também deve ser preocupação dos desenvolvedores frontend. As vezes as coisas ficam um pouco confusas, e então frequentemente vemos projetos em que está tudo misturado, trocado e até mal aplicado.

<!--more-->



A princípio precisamos definir a responsabilidade de cada uma das camadas principais, e depois detalhar cada uma delas.

## Conteúdo

A camada responsável pela apresentação do conteúdo é representada pelo HTML. Esta é a linguagem criada para tal, possui tags semânticas, e aquelas velhas coisas como: <var>blink</var>, <var>marquee</var>, ou até mesmo <var>font</var> foram depreciadas, para que parássemos de <cite>formatar</cide> diretamente no html.</p>

<h3>
  Imagem ou background
</h3>

<p>
  Ilustrações que apresentem um conteúdo ao usuário e que passem alguma informação, devem ser marcadas com a tag <var>img</var> e obrigatoriamente devem possuir um alt que as descreva.<br /> Já aquelas que existem apenas por conceitos estéticos de layout, são melhores colocadas como background através de CSS.
</p>

<h2>
  Apresentação
</h2>

<p>
  A camada de apresentação é responsabilidade do CSS. Esta é a linguagem ideal para tal, e cada dia mais ganha novas ferramentas, e melhor suporte dos diversos browsers.
</p>

<p>
  Hoje em dia apenas com css3, conseguimos rotacionar imagens, fazer fadeIn e fadeOut suaves, cantos arredondados(negros dias em que só era possível com diversas imagens nos cantos dos elementos), degradês e uma outra infinidade de coisas, que além de diminuir a quantidade de imagens que precisamos para chegar a tal efeito, também diminuíram a quantidade de código javascript.
</p>

<h2>
  Comportamento
</h2>

<p>
  Não por acaso deixei par comentar da camada de comportamento por último. Esta camada aqui, é responsabilidade da linguagem javascript. Deve ser adicionada ao projeto, injetando os comportamentos de forma não obstrutiva, ou seja, se não houver suporte ou falhar por qualquer motivo o javascript da página, o site precisa continuar acessível, navegável.
</p>

<h3>
  Acessível
</h3>

<p>
  Se for fazer um site com navegação ajax, lembre-se de só fazer isso depois que o site já funcionar perfeitamente sem javascript. Ou então aquele carousel de imagens e slideshow, onde usamos overflow, só ative e esconda o conteúdo quando o javascript for iniciado e então o acesso à informação for feito pelo usuário através das setas que você criou.
</p>

<p>
  A camada de comportamento é responsável por tudo aquilo o usuário vai interagir. E existe para melhorar a experiência, como verificar se um email ou id de usuário é válido sem precisar recarregar a página.
</p>

<h3>
  Cálculos
</h3>

<p>
  Frequentemente precisamos calcular algo que depende de alguma entrada do usuário. Lembre-se que o conteúdo é responsabilidade do HTML, então pegue as informações dinamicamente via DOM, e então calcule no javascript. Sem escrever tags com js, mas apenas injetar as informações na marcação.
</p>

<h2>
  Conclusão
</h2>

<p>
  Tudo flui melhor quando cada camada está bem separada e definida no projeto. Isso não deveria ser novidade para ninguém, mas não custa nada relembrar. =)
</p>
