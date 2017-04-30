---
id: 1404
title: Como recortar Email Marketing
date: 2011-09-22T23:32:03+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1404
permalink: /html/como-recortar-email-marketing/
dsq_thread_id:
  - "2102208496"
categories:
  - HTML
---
Tarefa chata !
  
Desenvolver Email Marketing envolve recorrer a uma estruturação em <table>, que a tempos deixamos para trás.
  
<!--more-->


  
Pois é, não adianta seguir padrões web, fazer Tableless, ou querer usar bastante css. Simplemente não vai funcionar.
  
[<img src="http://wbruno.com.br/wp-content/uploads/2011/09/clients-email-300x197.jpg" alt="" title="clients-email" width="300" height="197" class="alignleft size-medium wp-image-1405" srcset="http://wbruno.com.br/wp-content/uploads/2011/09/clients-email-300x197.jpg 300w, http://wbruno.com.br/wp-content/uploads/2011/09/clients-email.jpg 452w" sizes="(max-width: 300px) 100vw, 300px" />](http://wbruno.com.br/wp-content/uploads/2011/09/clients-email.jpg)Se no desenvolvimento de sites, nossos vilões são os browsers do mercado, e as diferenças de renderização, bugs e versões dos mesmos, num Email Marketing, a dor de cabeça dos Desenvolvedores FrontEnd, são os clients de email.

Outlook 2007, Outlook 2003 (mais uma vez a Micro$oft complicando a nossa vida, com versões diferentes de um mesmo software, e a incompabilidade/incosistência deles), gmail(um dos mais chatos para desenvolver emm), hotmail&#8230; e por ai vai.

Felizmente, algumas técnicas são conhecidas, mais ou menos como um &#8216;caminho das pedras&#8217;. Seguindo dicas simples, é possível gastarmos menos tempo nisso, e entregar um código HTML bastante satisfatório no quesito cross-client.
  
Sobre a compatibilidade, veja: <a href="http://www.campaignmonitor.com/css/" target="_blank">Guide to CSS support in email</a>.

Vamos lá, algumas regras:

### Durante o design da peça:

## Não use background-image

Como vc pode ver na tabela do link acima, background-image, não funciona nos clients de emails mais usados atualmente: hotmail, outlook, gmail.. portanto, não use. Peça para o designer fazer o layout, pensando que onde tiver **texto**, o fundo precisa ser cor sólida.
  
background-color funciona bem, e vamos usar a moda antiga:

<pre name="code" class="html">&lt;td bgcolor="#000"></pre>

### No início do recorte:

Use a ferramenta **slice** do Photoshop. Pense em recortes <u>horizontais</u>.

## O atributo rowspan é problemático

Por isso que eu disse para pensar em linhas. Não faça rowspans. Nem perca tempo. Irá quebrar.
  
Use e abuse dos **colspans**, mas o row nunca!

## Nem pense em margin e padding

<pre name="code" class="html">style="margin: yypx; padding: yypx;"</pre>

Vai funcionar nos teus navegadores enqnto vc estiver testando, porém nos clients de email não.

A regra agora, é fazer todo o espaçamento e divisão entre blocos, com fatias de imagem.
  
Para isso, o &#8216;Save for web&#8217; do Photoshop, marcando a opção: &#8216;HTML and images&#8217;, é o que temos para agilizar o processo.
  
Lembre-se de fazer os teus slices o mais folgados possível. Deixando espaço para a direita e para baixo, prevendo uma futura diferença de fontes entre sistemas operacionais. 

### Começando a mexer no html:

## Declare width e height em todas as TDs

Depois de exportar com o photoshop, preciso sair colocando altura, lagura e alinhamento vertical em todas as células da tabela.

## Declare align=&#8221;top&#8221;

Em todas as imagens. Isso vai evitar um espaçamento entre uma linha e outra em clients como o gmail.
  
Em alguns textos, é interessante usarmos align=&#8221;bottom&#8221; e middle em nossas TDs. Tudo bem, podemos usar. Mas mantenha as TDs de imagens com o valor top.

## Declare display: block em imagens de uma linha

Aquelas imagens que pegam a largura toda da tabela. Aquela nossa TR que só tem uma TD dentro dela, com uma única imagem.
  
CSS inline novamente. Declare display: block; nessas imagens.

### Colocando texto, onde deve ser texto:

## Abuse da tag font

Eu nem lembrava mais dessa tag.. mas para recorte de EMM, é melhor garantir que vai funcionar na maioria dos clients, e o mais perfeito possível. 

<pre name="code" class="html">&lt;font>&lt;/font></pre>

Não vamos cair na tentação de usar um <p>, <span>.. ou tags do tipo. Dificil prevermos quais serão as definições padrão do box model dessas tags. A tag <font> funciona bem. Façamos todos os nossos textos com ela.

## CSS inline

Isso! Não temos &#8216;reaproveitamento&#8217; de código fazendo email marketing. Note que a tag link e style, não funcionam no hotmail e gmail respectivamente. Portanto, 

<pre name="code" class="html">style=""</pre>

neles !

## A família de propriedades css font funciona bem

Em testes que fiz, tentando usar o size da tag <font>, nunca ficava bom. Vale lembrar que o sistema operacional entra como variavel nesse desenvolvimento também. Uma font 12px Tahoma, no MAC fica de uma forma e no Windows, de uma outra completamente diferente(espaçamento de letras, anti-alising..).

Então, aqui usamos css inline. 

## Links! Links!

Afinal de pouco adiantaria nossos emails marketings, se estes não tiverem links.
  
Para links em textos, devemos usar livremente a tag de âncora <a></a>, porém naqueles botõezinhos e banners que o designer fez, não vale a mesma regra. Melhor aqui é usar imagem mapeada!
  
Isso mesmo. Use #map. Se você tentar usar algo como:

<pre name="code" class="html">&lt;a href="">&lt;img src="..." />&lt;/a></pre>

Você terá problemas com isso.

## Será que isso é tudo?

Talvez não, mas posso garatir que ao menos é o suficiente para os clients de email mais conhecidos e utilizados.
  
Se ainda assim, você estiver com dúvidas, e precisar de mais dicas, este texto: <a href="http://www.campaignmonitor.com/design-guidelines/" target="_blank">http://www.campaignmonitor.com/design-guidelines/</a>(inglês), é a minha última dica.

## É trabalhoso

Realmente é. E o ínicio do recorte, em que temos que colocar largura, altura, valign em todas as TDs, align=&#8221;top&#8221;, em todas as imagens, display: block; em todas as imagens que estão sozinhas em uma só linha, e colocar o caminho completo em todos os atributos src=&#8221;&#8221; das nossas imagens, é um tanto quanto repetitivo, e braçal.

Por isso, desenvolvi essa <a href="http://wbruno.com.br/scripts/gerador_emm.php" target="_blank">ferramenta para recorte de Email Marketing</a>. Lógico que não faz milagre, mas com umas Expressões Regulares e php, faço essa parte braçal, de entrar com o HTML:

<pre name="code" class="html">&lt;tr>
    	&lt;td>&lt;img src="images/img1.jpg" width="40" height="20" alt="">&lt;/td>
    	&lt;td>&lt;img src="images/img2.jpg" width="56" height="13" alt="">&lt;/td>
&lt;/tr>
</pre>

E sair:

<pre name="code" class="html">&lt;tr>
    	&lt;td width="40" height="20" valign="top">&lt;img src="http://wbruno.com.br/images/img1.jpg" width="40" height="20" alt="" align="top">&lt;/td>
    	&lt;td width="56" height="13" valign="top">&lt;img src="http://wbruno.com.br/images/img2.jpg" width="56" height="13" alt="" align="top">&lt;/td>
	&lt;/tr>
</pre>

Ou seja, a parte chata resolvida.
  
Dai resta apenas trocar os slices onde deve ter texto, por texto mesmo formatado segundo as dicas acima.
  
É isso. Espero que ajude vocês.