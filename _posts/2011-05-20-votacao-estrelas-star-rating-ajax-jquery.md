---
id: 974
title: 'Votação com estrelas [ star rating ] &#8211; Ajax jQuery'
date: 2011-05-20T07:00:13+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=974
permalink: /ajax/votacao-estrelas-star-rating-ajax-jquery/
dsq_thread_id:
  - "2101217564"
categories:
  - AJAX
---
Não vou explicar muito detalhadamente o HTML e CSS, pois está tudo bem simples.

Apenas para dar um contexto, usei alguns produtos, e embaixo de cada um deles, existem 5 estrelas cinza.

[<img src="/wp-content/uploads/2011/05/votacao.jpg" alt="" title="votacao" width="433" height="373" class="aligncenter size-full wp-image-975" srcset="/wp-content/uploads/2011/05/votacao.jpg 433w, /wp-content/uploads/2011/05/votacao-300x258.jpg 300w" sizes="(max-width: 433px) 100vw, 433px" />](/wp-content/uploads/2011/05/votacao.jpg)

<!--more-->



O comportamento será o seguinte:

> _Ao clicar em alguma estrela, ela e as anteriores a ela, deverão &#8216;acender'(ficar de outra cor). Clicando novamente, na última estrela escolhida, a pontuação será zerada, tornando todas as estrelas cinzas._

E além disso:

> _Se já estiver registrada alguma pontuação, ao clicar em uma estrela de menor valor, as estrelas &#8216;ativas&#8217; depois dessa, devem ser &#8216;desmarcadas&#8217;._

Okay, conforme prometi, o HTML+CSS, é mínimo e simples:

<pre name="code" class="html">&lt;html>
&lt;head>
&lt;style type="text/css">
* { margin: 0; padding: 0; list-style: none; }
.stars {
	width: 100px;
	height: 20px;
	margin: 5px auto 0 auto;
}
#produtos .stars li {
	background: url('star_groups.jpg') no-repeat;
	display: block;
	height: 20px;
	width: 20px;
	cursor: pointer;
	float: left;
}
#produtos .stars li.active {
	background-position: left -45px;
}
#produtos {
	width: 450px;
	margin: 20px auto 0 auto;
}
#produtos li {
	float: left;
	width: 150px;
	height: 200px;
	color: #1B57A3;
	text-align: center;
}
#produtos p {
	text-decoration: underline;
	font: 12px Arial, Verdana, sans-serif;
}
#sql {
	font: bold 20px Arial;
	color: #f00;
	text-align: center;
	clear: both;
}
&lt;/style>

&lt;/head>
&lt;body>
	&lt;ul id="produtos">
		&lt;li>
			&lt;img src="MacBook.jpg" alt="" />
			&lt;p>MacBook&lt;/p>
			&lt;ol class="stars">&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;/ol>
			&lt;input type="hidden" name="id_produto[]" value="15" />
		&lt;/li>
		&lt;li>
			&lt;img src="iMac.jpg" alt="" />
			&lt;p>iMac&lt;/p>
			&lt;ol class="stars">&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;/ol>
			&lt;input type="hidden" name="id_produto[]" value="12" />
		&lt;/li>
		&lt;li>
			&lt;img src="iPhone.jpg" alt="" />
			&lt;p>iPhone&lt;/p>
			&lt;ol class="stars">&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;/ol>
			&lt;input type="hidden" name="id_produto[]" value="5" />
		&lt;/li>

		&lt;li>
			&lt;img src="iPod_Nano.jpg" alt="" />
			&lt;p>iPod Nano&lt;/p>
			&lt;ol class="stars">&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;/ol>
			&lt;input type="hidden" name="id_produto[]" value="7" />
		&lt;/li>
		&lt;li>
			&lt;img src="iPod_Classic.jpg" alt="" />
			&lt;p>iPod Classic&lt;/p>
			&lt;ol class="stars">&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;/ol>
			&lt;input type="hidden" name="id_produto[]" value="9" />
		&lt;/li>
		&lt;li>
			&lt;img src="HP_LP3065.jpg" alt="" />
			&lt;p>HP_LP3065&lt;/p>
			&lt;ol class="stars">&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;li>&lt;/li>&lt;/ol>
			&lt;input type="hidden" name="id_produto[]" value="22" />
		&lt;/li>
	&lt;/ul>&lt;!-- /produtos -->

	&lt;div id="sql">&lt;/div>
&lt;/body>
&lt;/html>
</pre>

Optei por deixar cada estrela como um LI, filho da Lista Ordenada **.stars**, pela simplicidade da marcação, e do javascript que vamos desenvolver.

Além disso, usei um input hidden dentro do container de cada produto, para sabermos qual o ID daquele produto no nosso banco de dados.

<pre name="code" class="javascript">&lt;script type="text/javascript" src="http://code.jquery.com/jquery-1.6.1.min.js">&lt;/script>
&lt;script type="text/javascript">
$(document).ready(function(){
	$('.stars li').click(function(){
		var $this = $( this );
		var ol = $this.parent('ol');
		var rating = $this.index()+1;
		var id_produto = ol.parent('li').find("input[name='id_produto[]']").val();


		if( $this.hasClass('active') && !$this.next('li').hasClass('active') ){
			$( ol ).find('li').removeClass('active');
			rating = 0;
		}
		else{
			$( ol ).find('li').removeClass('active');
			for( var i=0; i&lt;rating; i++ ){
				$( ol ).find('li').eq( i ).addClass('active');
			};
		}

		$.ajax({
			type: "POST",
			url: "retorno-votacao.php",
			data: "id_produto="+id_produto+"&voto="+rating,
			success: function( data ){
				$('#sql').html( data );
			}
		});
	});
});
&lt;/script>
</pre>

O script server-side, é a parte mais simples:

<pre name="code" class="php">&lt;?php

if( $_SERVER['REQUEST_METHOD']=='POST' ){
	$id_produto = (int)getPost('id_produto');
	$voto = (int)getPost('voto');

	$sql = "INSERT INTO voto (`id_produto`, `voto`, `ip`, `data`) VALUES ( {$id_produto}, {$voto}, '{$_SERVER['REMOTE_ADDR']}', NOW() )";
	echo $sql;
}


function getPost( $key ){
	return isset( $_POST[ $key ] ) ? filter( $_POST[ $key ] ) : null;
}
function filter( $str ){
	return addslashes( $str );//a cargo do leitor
}
</pre>

Veja que faço o INSERT na tabela \`voto\` a cada requisição que recebo.

Nesse ponto, as tuas regras de negócio devem ditar o tratamento que deve ser feito. Se cada cliente só pode votar uma vez em cada produto, se ele pode mudar o voto dele..

## <a href="http://www.wbruno.com.br/scripts/votacao-estrelas.php" target="_blank">Demonstração Online</a>
