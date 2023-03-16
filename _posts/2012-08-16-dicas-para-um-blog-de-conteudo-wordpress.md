---
id: 2484
title: Dicas iniciais para um blog de conteúdo em WordPress
date: 2012-08-16T07:00:28+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2484
permalink: /wordpress/dicas-para-um-blog-de-conteudo-wordpress/
categories:
  - WordPress
---
## Blog de conteúdo

São _&#8220;dicas inciais&#8221;_ para um blog de conteúdo, assim como esse meu. Por que vc pode começar o teu blog com elas, antes mesmo de começar a escrever os posts.

Estou lhes contando sobre a minha experiência como blogueiro na plataforma wordpress. Muitas das dicas que vou dar aqui, são baseadas no que eu fiz de certo e errado. Sempre há tempo de corrigir e melhorar. Vamos lá!

<!--more-->



[<img src="/wp-content/uploads/2012/08/wordpress-300x300.jpeg" alt="Blog de conteúdo" title="Blog de conteúdo" width="300" height="300" class="alignright size-medium wp-image-2493" srcset="/wp-content/uploads/2012/08/wordpress-300x300.jpeg 300w, /wp-content/uploads/2012/08/wordpress-150x150.jpeg 150w, /wp-content/uploads/2012/08/wordpress.jpeg 500w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2012/08/wordpress.jpeg)

<p style="font-size: 22px">
  Começando ou otimizando um blog de conteúdo na plataforma WordPress
</p>

Eu fico mais motivado quando sei que o meu blog desperta interesse.

Hoje em dia, nem pense em começar um site que seja, ou um blog de conteúdo, sem antes de tudo, instalar alguma ferramenta para monitorar o comportamento dos teus visitantes.

[<img src="/wp-content/uploads/2012/08/google-analytics.png" alt="Google Analytics" title="google-analytics" width="300" height="225" class="alignleft size-full wp-image-2485" />](/wp-content/uploads/2012/08/google-analytics.png)

## Analytics instalado como plugin

Eu uso o <a href="http://wordpress.org/extend/plugins/google-analyticator/" rel="external nofollow">Google Analyticator</a>, mas pode ser qualquer algum outro que lhe permita incluir o código de rastreamento do Google Analytics, sem ter que mexer nos arquivos do tema, e menos ainda no core do wordpress.

Já fiz da forma errada. E ai, durante uma alteração de skin, fiquei quase um dia inteiro sem mandar para o analytics os dados das visitas.

Colocando o analytics como um plugin, alterações de tema, serão transparentes e não te deixarão um buraco nas estatísticas.

## Evitando conteúdo duplicado

Isso é bem básico, e se aplica a qualquer coisa que esteja hospedada na web: não deixe que os robôs de busca, indexem um mesmo conteúdo seu, por diversas URLs diferentes.

O erro mais comum, é deixar <var>www.site.com.br</var>, e <var>site.com.br</var> apontando ambos diretamente, sem nenhum ser redirect do outro.

Escolha um (eu prefiro sem o www), e mande um 301 da outra url.

<pre name="code" class="php">RewriteCond %{HTTP_HOST} ^www\.wbruno\.com\.br$
RewriteRule (.*) http://wbruno.com.br/$1 [R=301,L]```

## Otimize o seu tema

Faça-o carregar rápido. O importante é o conteúdo.

Estamos em uma disputa contra outros produtores de textos. O visitante não vai escolher o seu feed, só por que a sua página é mais bonita, mas se ela carregar mais rápido, isso pode ajudá-lo a não ir embora.

Estou usando o <a href="http://wordpress.org/extend/plugins/wp-super-cache/" rel="external nofollow">WP Super Cache</a>, para ajudar na performance das páginas(economizando consultas ao banco mysql).

Além desse tema simples e responsivo em html5.

O visitante precisa se sentir bem, gostar de ler. Essa é a meta: prender o visitante.

[<img src="/wp-content/uploads/2012/08/250px-IPhone_4S_No_shadow-172x300.png" alt="Otimize para mobile seu blog" title="250px-IPhone_4S_No_shadow" width="172" height="300" class="alignleft size-medium wp-image-2535" srcset="/wp-content/uploads/2012/08/250px-IPhone_4S_No_shadow-172x300.png 172w, /wp-content/uploads/2012/08/250px-IPhone_4S_No_shadow.png 250w" sizes="(max-width: 172px) 100vw, 172px" />](/wp-content/uploads/2012/08/250px-IPhone_4S_No_shadow.png)

Um tema otimizado, irá ajudar até os seus visitantes que acessam de uma rede 3g de um tablet ou smartphone.

## Acesso mobile

Algumas pessoas realmente lêem através do celular/tablet&#8230; Isso é bom, na verdade, isso é fantástico.

Ainda mais se você também puder aproveitar essa mobilidade para &#8220;não se esquecer&#8221; de postar.

Instale um aplicativo no seu smartphone, e faça um draft daquele assunto que lhe veio a cabeça. Super simples, basta ativar o <var>XML-RPC</var> em Settings -> Writing.

## Alguma forma de controlar os spams

Um dos meus &#8220;pagamentos&#8221;, são os comentários que os leitores fazem nos meus posts.

Entretanto, também tem robôs por ai, tentando espalhar spams, e eles vão ficar enchendo o seu saco, tentando comentar no teu blog.

Estou usando o <a href="http://andrey.sorvin.ru/tag/invisible_captcha/" rel="nofollow external">Invisible Captcha</a>.

## Responda os comentários!

Dessa forma, você criará um vínculo do leitor com o seu blog. Se ele for respondido, se sentirá &#8220;importante&#8221;. Ele irá voltar para ler a resposta, e acompanhar as respostas dos outros.

Nem que seja apenas um comentário de elogio, agradeça. Lembre-se que os comentários também adicionam &#8220;conteúdo&#8221; ao documento. As vezes quando pesquisamos no google, a resposta do que queremos está nos comentários, e não no post em si.

## Divulgue!

Use facebook, twitter, google plus, orkut.. divulgue!

Se está na web, então alcance o teu público alvo. Espalhe o conteúdo. O plugin <a href="http://wordpress.org/extend/plugins/really-simple-facebook-twitter-share-buttons/" rel="nofollow external">Really Simple Share</a> é muito bom em colocar botões das redes sociais em cada um dos teus posts.

## Muitas URLs lixo na SERP

Este é um dos _problemas_ atuais da &#8220;não otimização&#8221; deste blog.

Tenho publicado, um pouco mais de 200 posts. Porém uma busca no google por:

[<img src="/wp-content/uploads/2012/08/Captura-de-Tela-2012-08-15-às-23.51.45.png" alt="" title="Captura de Tela 2012-08-15 às 23.51.45" width="600" height="131" class="aligncenter size-full wp-image-2548" srcset="/wp-content/uploads/2012/08/Captura-de-Tela-2012-08-15-às-23.51.45.png 600w, /wp-content/uploads/2012/08/Captura-de-Tela-2012-08-15-às-23.51.45-300x65.png 300w" sizes="(max-width: 600px) 100vw, 600px" />](/wp-content/uploads/2012/08/Captura-de-Tela-2012-08-15-às-23.51.45.png)retorna mais de 900 resultados.

Ok, fui indexado.. bem indexado. Muito indexado. Mas será que isso é realmente bom ?

Qual é a relevância dessas 700 URLs que não levam diretamente para um certo post ?

Paginação dos posts, paginação das categorias, paginação das tags.. aghr!

Algumas coisas são até repetidas entre si. Estou considerando um &#8220;problema&#8221;. Então vou colocar um noindex, para que o robô saiba que não precisa se preocupar com esse conteúdo das paginações.

Eu quero o googlebot focado nos posts. Quero que o meu conteúdo prevaleça.

Não sou uma loja virtual. Então as minhas categorias não tem tanta importância na SERP.

[<img src="/wp-content/uploads/2012/08/calendario.png" alt="" title="calendario" width="300" height="298" class="alignright size-full wp-image-2534" srcset="/wp-content/uploads/2012/08/calendario.png 300w, /wp-content/uploads/2012/08/calendario-150x150.png 150w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2012/08/calendario.png)

## O conteúdo é REI

Qual é a frequência que você gostaria que o seu visitante retornasse ao teu blog ?

E o google bot ? Seria muito bom se os teus leitores, e o robô de busca, lessem o conteúdo do blog, todo dia.. ne?!

Realmente seria, mas você posta todo dia ? Você tem bons conteúdos ?

O googlebot é um &#8220;conjunto de algorítmos&#8221; muito ocupado e com coisas muito mais interessantes a fazer, do que ficar procurando novidades onde não há. Ele não vai voltar todos os dias ao teu site, se você não tiver algo realmente interessante a dizer.

## Escolha bons títulos e boas categorias

Uma estrutura interessante de permalinks para se usar é: <var>categoria/nome-do-post</var>.

Eu ainda estou usando a data antes do nome do post na url, mas não deixe de forma alguma a forma default ?p=15(não amigável).

Os seus posts precisam ser encontrados. Escreva como vc procuraria se quisesse ler sobre aquilo.

Melhor um título: &#8220;Como funcionam as Expressões Regulares&#8221;, do quem um título: &#8220;Leia sobre REGEX&#8221;.

## É isso

Algumas das dicas que dei aqui, não se aplicam apenas ao mundo do WordPress. Procure a solução equivalente da tua plataforma, ou aplique alguma dessas dicas, no teu site institucional, loja virtual, também tá valendo.

Nunca se esqueça de fazer bem o básico.

Qual sua experiência com conteúdo ? possui um blog de conteúdo ? comente ai&#8230; **let me know**!!
