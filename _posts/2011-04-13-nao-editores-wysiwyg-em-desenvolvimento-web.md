---
id: 720
title: Não use editores WYSIWYG em desenvolvimento web !
date: 2011-04-13T07:00:12+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=720
permalink: /opiniao/nao-editores-wysiwyg-em-desenvolvimento-web/
dsq_thread_id:
  - "2101515150"
categories:
  - Opinião
---
[<img src="http://wbruno.com.br/wp-content/uploads/2011/04/logodream-150x150.png" alt="" title="logodream" width="150" height="150" class="alignright size-thumbnail wp-image-726" srcset="http://wbruno.com.br/wp-content/uploads/2011/04/logodream-150x150.png 150w, http://wbruno.com.br/wp-content/uploads/2011/04/logodream-300x300.png 300w, http://wbruno.com.br/wp-content/uploads/2011/04/logodream.png 512w" sizes="(max-width: 150px) 100vw, 150px" />](http://wbruno.com.br/wp-content/uploads/2011/04/logodream.png)Faço parte do lado _xiita_ da força. Sempre vejo pessoas perguntando sobre editores, especialmente sobre o DreamWeaver. Resolvi escrever aqui no blog.(pois este é o meu espaço, e posso mostrar opiniões que foram interpretadas como ofenças no fórum). Fiz uma busca [dessa vez foi superficial], e achei <a href="http://revolucao.etc.br/archives/web-standards-e-as-ferramentas-de-desenvolvimento/" target="_blank">este texto</a>, bem interessante.

Ta aí um cara que eu respeito.
  
<!--more-->


  
Descrição do site da Adobe:

> ### <a href="http://www.adobe.com/br/products/dreamweaver.html?promoid=BOZQX" target="_blank">O que é o Dreamweaver?</a>
> 
> _O Adobe® Dreamweaver® CS5.5 é o software de criação e edição líder da Web que fornece recursos em nível visual e de código para criar sites baseados em padrões e designs para desktops, smartphones, tablets e outros dispositivos._

Para mim, o **DW**, é um <u>deserviço</u> para a comunidade de desenvolvedores.
  
Aqueles que usam esse software em [Modo Code], vão querer me crucificar. Mas para esses eu apenas pergunto:

> _E por que não outro IDE [de verdade], no lugar do DreamWeaver ?_

[<img src="http://wbruno.com.br/wp-content/uploads/2011/04/ides_best-e12663621372631.png" alt="" title="ides_best-e1266362137263" width="448" height="194" class="aligncenter size-full wp-image-730" srcset="http://wbruno.com.br/wp-content/uploads/2011/04/ides_best-e12663621372631.png 448w, http://wbruno.com.br/wp-content/uploads/2011/04/ides_best-e12663621372631-300x129.png 300w" sizes="(max-width: 448px) 100vw, 448px" />](http://wbruno.com.br/wp-content/uploads/2011/04/ides_best-e12663621372631.png)

Prefiro me manter como purista e radical, do que ser &#8216;moderado&#8217;, sobre esse assunto.

[<img src="http://wbruno.com.br/wp-content/uploads/2011/04/Notepad++-150x150.png" alt="" title="Notepad++" width="150" height="150" class="alignleft size-thumbnail wp-image-728" srcset="http://wbruno.com.br/wp-content/uploads/2011/04/Notepad++-150x150.png 150w, http://wbruno.com.br/wp-content/uploads/2011/04/Notepad++.png 256w" sizes="(max-width: 150px) 100vw, 150px" />](http://wbruno.com.br/wp-content/uploads/2011/04/Notepad++.png)Falo para aqueles que estão começando e optaram por um editor desse tipo, para aqueles que &#8216;gostam&#8217; do [Modo Visual], e para aqueles que nunca se questionaram, se deveriam ou não tentar outro editor.

Ninguém navega na internet, nem visita sites através do &#8216;visualizador&#8217;. O que é mostrado ali, não condiz com a realidade dos browsers. Inútil &#8216;fazer aparecer certo&#8217; no visualizador do DW, se o que realmente importa é como vai ficar no ie, no firefox, no chrome..

Os códigos gerados são porcos, feios e sujos. Seja para javascript, para php, para HTML, ou qualquer outra linguagem que nem quero ver o DW tentar fazer. Repito aqui: _códigos devem ser escritos para humanos_.

Recursos demais, atrapalham o teu desenvolvimento pessoal como programador. Conheço pessoas tão acostumadas com o autocompletar dos editores, que sem isso se perdem, e nem conseguem fazer coisas simples.

Não devemos ser &#8216;escravos&#8217; de nenhuma ferramenta, e nem de nenhum recurso. Para mim, desenvolvedores devem ser capazes de trabalhar, até sem highlight. Sempre digitei todas as minhas tags na mão, inclusive o fechamento delas. Não dependo desse recurso.

[<img src="http://wbruno.com.br/wp-content/uploads/2011/04/coda_icon.png" alt="" title="coda_icon" width="164" height="156" class="alignleft size-full wp-image-732" />](http://wbruno.com.br/wp-content/uploads/2011/04/coda_icon.png)O coda, possui um autocomplete, que as vezes me atrapalha.

Já fiz freela presencial para uma agência, onde o único editor que eles tinham na máquina era o famigerado DW. Usei, sem problemas, apesar de não gostar. Para mim era peso em demasia, já que não uso efetivamente nem 10% dos botões dele.

No caso dessa agência em particular, usavam o DW em modo código, mas quando algum projeto estava &#8216;muito apertado&#8217;, eles tinham a coragem de mudar para o Visual, fazer e entregar, tudo de &#8216;forma rápida&#8217;, visando a &#8216;produtividade&#8217;.

Neste instante, eles adotaram a metodologia dos CQPs [[Caras que Programam](http://www.wbruno.com.br/2011/03/29/diferenca-entre-cara-programa-um-programador/)]. Só que de uma forma ainda pior: era o editor que estava programando por eles !

Não existe só o DreamWeaver de Editor &#8220;Oque vc vê, é oque vc tem&#8221;. FrontPage, e até o Word, te possibilitam &#8216;criar sites&#8217;. Porém não usamos isso mais hoje em dia, pois não vale a pena &#8216;entregar logo&#8217;, se num futuro não distante, teremos que dar manutenção no monstro que o &#8216;WYS'(Visual) criou pra gente.

É a mesma questão do [uso de frameworks](http://www.wbruno.com.br/2011/04/04/nao-jquery-nao-aprenda-qualquer-framework-antes-de/). Depende do teu nível de conhecimento.
  
Aprenda bem e entenda antes de usar. Não seja dominado, nem dependente, e nem escravo.