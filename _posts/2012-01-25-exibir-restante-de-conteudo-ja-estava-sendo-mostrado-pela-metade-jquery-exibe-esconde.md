---
id: 1754
title: 'Exibir restante de conteúdo, que já estava sendo mostrado pela &#8220;metade&#8221;- jQuery exibe-esconde'
date: 2012-01-25T07:00:07+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1754
permalink: /jquery/exibir-restante-de-conteudo-ja-estava-sendo-mostrado-pela-metade-jquery-exibe-esconde/
dsq_thread_id:
  - "2100819413"
categories:
  - jQuery
---
Boas,

A idéia aqui, foi chegar próximo do efeito de &#8220;Exibir mais&#8221; do youtube:
  
Escondido:
  
[<img src="http://wbruno.com.br/wp-content/uploads/2012/01/more-300x103.png" alt="" title="more" width="300" height="103" class="aligncenter size-medium wp-image-1755" srcset="http://wbruno.com.br/wp-content/uploads/2012/01/more-300x103.png 300w, http://wbruno.com.br/wp-content/uploads/2012/01/more.png 656w" sizes="(max-width: 300px) 100vw, 300px" />](http://wbruno.com.br/wp-content/uploads/2012/01/more.png)

A mostra:
  
[<img src="http://wbruno.com.br/wp-content/uploads/2012/01/less-300x135.png" alt="" title="less" width="300" height="135" class="aligncenter size-medium wp-image-1756" srcset="http://wbruno.com.br/wp-content/uploads/2012/01/less-300x135.png 300w, http://wbruno.com.br/wp-content/uploads/2012/01/less.png 642w" sizes="(max-width: 300px) 100vw, 300px" />](http://wbruno.com.br/wp-content/uploads/2012/01/less.png)

Ok ?
  
Uma parte do conteúdo fica a mostra, e clicando no botão aparece o restante.

O primeiro passo é resolver o efeito no **css**. Todos os efeitos são apenas css. O javascript manipulando css. jQuery só entra para facilitar essa manipulação, porém é importante ressaltar, que toda a lógica e o efeito em si, ficou no css.

Depois de conseguir resolver tanto o estado aberto, qnto o fechado, usando apenas css e html, sem nenhuma linha de js, fazer o comportamento fica super simples.

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;style type="text/css">
* { margin: 0; padding: 0; }
p { margin-bottom: 10px; }
.content { margin: 0 auto; width: 500px; }
#panel { position: relative; width: 500px; margin: 0 auto; }
#content { }
.hidden { height: 100px; overflow: hidden; }
#toggle { width: 488px; height: 20px; padding: 5px;
	background: #fff; border: 1px solid #ccc; cursor: pointer;
	text-align: center;
}
&lt;/style>
&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
jQuery(document).ready(function(){
	jQuery('#toggle').click(function(){
		jQuery('#panel').toggleClass('hidden');							  
	});	
});
&lt;/script>
&lt;/head>
&lt;body>
	&lt;div id="panel" class="hidden content">
		&lt;div id="content">
			&lt;p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec sed gravida dolor. Fusce aliquam, urna sit amet 
            luctus adipiscing, massa sem venenatis dui, quis accumsan mi orci eu orci. Mauris nec massa non mi iaculis tincidunt 
            eget a lectus. Curabitur suscipit, magna vel laoreet volutpat, sem mauris placerat risus, nec pretium mauris orci non dui.&lt;/p>
            
			&lt;p>Cras in massa dapibus leo tincidunt molestie nec ut sem. Aenean sit amet ipsum risus. Class aptent taciti sociosqu 
            ad litora torquent per conubia nostra, per inceptos himenaeos. Cras vitae erat at magna volutpat consequat ut a justo. 
            Mauris dapibus dolor at orci placerat congue. Praesent facilisis sodales molestie. Quisque eget lacus eget justo aliquet
             sagittis. Duis sed elit id dui semper feugiat. Vivamus risus magna, facilisis at hendrerit sit amet, accumsan nec felis.&lt;/p>
             
			&lt;p>Nunc massa tellus, fringilla ut tincidunt consequat, ultricies eget nunc. &lt;/p>
         &lt;/div>&lt;!-- /content -->
	&lt;/div>&lt;!-- /panel -->
	&lt;div id="toggle" class="content">toggle&lt;/div>
&lt;/body>
&lt;/html>
</pre>

## [Demonstração](http://wbruno.com.br/scripts/mostra_metade.html)