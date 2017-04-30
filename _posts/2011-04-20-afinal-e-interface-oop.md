---
id: 824
title: 'Afinal o que é Interface ? [oop]'
date: 2011-04-20T06:55:50+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=824
permalink: /php/afinal-e-interface-oop/
dsq_thread_id:
  - "2102551453"
categories:
  - PHP
tags:
  - oo
---
[<img src="http://wbruno.com.br/wp-content/uploads/2011/04/elephpant-elephant-php-logo_big.png" alt="" title="elephpant-elephant-php-logo_big" width="150" height="96" class="alignright size-full wp-image-496" />](http://wbruno.com.br/wp-content/uploads/2011/04/elephpant-elephant-php-logo_big.png)Vou partir do princípio de que se você chegou até aqui, já tem algum conhecimento em Orientação a Objetos, já esboçou as tuas primeiras classes, e já tem alguma experiência na criação de sistemas.

> _Interfaces são contratos._

Na minha ótica, o paradigma dos objetos, foi criado para resolver basicamente duas coisas: Padronização e Encapsulamento. Os outros problemas que OO também resolve, já possuiam soluções anteriores. [reutilização, organização&#8230;]

As **interfaces** existem por isso, para ajudar a defender o primeiro pilar.
  
Estou falando &#8216;por cima&#8217;, para simplificar e me focar no conceito que quero expor.
  
<!--more-->


  
Imaginemos que nosso sistema faz um CRUD, e possui um módulo de Agenda, razoável, termos um model que seja parecido com isso:

<pre name="code" class="php">&lt;?php

class Agenda
{
	public function insere_agenda(){
		//implementação
	}
	public function atualiza_agenda(){
		//implementação
	}
	public function excluir_agenda(){
		//implementação
	}
}</pre>

Bacana.. Recebemos então uma solicitação que nos pede para criarmos outro &#8216;módulo&#8217;, para galerias de fotos. Novamente, vamos lá e fazemos:

<pre name="code" class="php">&lt;?php

class Galeria
{
	public function insere_galeria(){
		//implementação
	}
	//...
}</pre>

bem parecidos, porém diferentes nas implementações.
  
Nosso &#8216;controlador&#8217;, que usará os objetos instanciados apartir de Galeria, ou Agenda, sabe que precisa usar:

<pre name="code" class="php">$galeria = new Galeria();
$galeria->insere_galeria();</pre>

ou

<pre name="code" class="php">$agenda = new Agenda();
$agenda->insere_agenda();</pre>

Mas e se um outro programador, for dar continuidade nesse trabalho, é complicado ele ter a paciência de[<img src="http://wbruno.com.br/wp-content/uploads/2011/04/E_Agora_Blog7-300x269.jpg" alt="" title="E_Agora_(Blog)[7]" width="300" height="269" class="alignleft size-medium wp-image-828" srcset="http://wbruno.com.br/wp-content/uploads/2011/04/E_Agora_Blog7-300x269.jpg 300w, http://wbruno.com.br/wp-content/uploads/2011/04/E_Agora_Blog7.jpg 400w" sizes="(max-width: 300px) 100vw, 300px" />](http://wbruno.com.br/wp-content/uploads/2011/04/E_Agora_Blog7.jpg) estudar todas as nossas classes, identificar o &#8216;padrão&#8217; que usamos, e então implementar agora o módulo de &#8216;Notícias&#8217;&#8230; esse &#8216;outro programador&#8217;, pode até ser nós mesmos, daqui um tempo.

Evoluimos a cada &#8216;passagem de tempo&#8217;, impossível termos de cabeça todos os códigos, de todos os nossos projetos. Pode ser que não nos lembremos o que fizemos &#8216;lá atrás&#8217;.

Documentar é importante, mas um código bem escrito é ainda mais.
  
Assim que esse &#8216;novo programador&#8217;, for implementar o módulo de Notícias, ele terá que se perguntar: &#8216;E agora, oque preciso fazer?&#8217;.

Aqui é onde mora o perigo. Ele pode detonar &#8216;o nosso padrão'(que já estava errado), e fazer algo completamente bizzarro:

<pre name="code" class="php">&lt;?php
class Noticia
{
	public function cadastra(){}
	public function Muda(){}
	public function manda_pRo_liXo(){}
}</pre>

e ai ? a culpa não é só dele.
  
O nosso sistema por si só, não _&#8216;deixava claro&#8217;_, como as coisas deveriam ser, ou seja, **não implementamos direito** um dos pilares do OO.

É aqui que entram as <a href="http://php.net/manual/en/language.oop5.interfaces.php" target="_blank">interfaces</a>. A forma de pensar tem que mudar.
  
Afinal, **Galeria::insere_galeria();**, **Agenda::insere_agenda()**, e **Noticia::cadastra();**, não são &#8216;semelhantes entre si&#8217; ?

Queremos que os próximos a programarem no nosso sistema, saibam o que devem fazer, e &#8216;como devem fazer&#8217;. Podemos então, obrigar que os próximos depois da gente, sejam mais consistentes.

<pre name="code" class="php:firstLine[7]">interface iModel
	{
		public function insert();
		public function update();
		public function delete();
	}</pre>

A nomenclatura já está bem melhor também.
  
Pessoalmente, não vejo sentido no insere_blablabla(); mas coloquei ali, pq vejo muito disso por ai.

Então, daqui para frente, nossas classes precisam apenas **implementar** essa interface.
  
Isso mesmo **implementar**. A interface define apenas a **assinatura** dos nossos métodos. A implementação fica a cargo de cada classe em específico.

Aqui então, vemos surgir o conceito de &#8216;poliformismo&#8217;. Coisas iguais com comportamentos diferentes, ou coisas diferentes com comportamentos iguais.
  
Mas como isso é pano para manga, voltemos as nossas interfaces, que não são nada mais do que: &#8216;coisas&#8217; que vemos, que nos permitem trabalhar com elas. A beleza da programação, está em não precisarmos saber como os métodos foram/serão implementados, porém podemos usá-los, acreditando que eles cumpram o papel para o qual foram designados.

Não raramente fazemos isso. Posso dizer que toda vez que você usa uma função nativa da linguagem, vc está acreditando que ela faz oque vc precisa, sem saber exatamente como ela faz.

Nossas classes agora são assim:

<pre name="code" class="php:firstLine[13]">class Agenda implements iModel
	{

	}
	class Galeria implements iModel
	{

	}</pre>

Todas irão implementar a nossa interface, e por isso, precisam obrigatoriamente fazer isso corretamente, se não, alguns erros serão lançados:

> Fatal error: Class Agenda contains 3 abstract methods and must therefore be declared abstract or implement the remaining methods (iModel::insert, iModel::update, iModel::delete) in C:\Program Files\Apache Software Foundation\Apache2.2\htdocs\index.php on line 17 

Somos obrigados a:

<pre name="code" class="php:firstLine[13]">class Agenda implements iModel
	{
		public function insert(){
			//implementação
		}
		public function update(){
			//implementação
		}
		public function delete(){
			//implementação
		}
	}</pre>

E o **mesmo** para todas as classes que implementarem essa interface.
  
O nosso &#8216;novo programador&#8217;, que vai criar lá, o módulo de Notícias, agora, apenas precisa ler a **iModel**, e implementar a class Noticia, com base nessa interface.

Se nosso chefe chegar agora, pedir um módulo de &#8216;Artigos&#8217;, então sabemos por onde começar, e temos algo para nos basear. Tá lindo até aqui, mas não para por ai.

É ainda mais poderoso que isso. O php apesar de ser &#8216;de tipagem fraca&#8217;, nos dá um suporte muito importante a <a href="http://www.php.net/manual/pt_BR/language.oop5.typehinting.php" target="_blank">typehinting</a>. Nossas models, **usarão** um banco de dados(ou não), mas **não são**, &#8216;o banco&#8217; em si.

Por isso que não faz sentido, que nossas models, herdem coisas de uma class Db.
  
Se é para usar, vamos usar:

<pre name="code" class="php:firstLine[7]">interface iModel
	{
		public function insert( iDb $db );
		public function update( iDb $db );
		public function delete( iDb $db );
	}</pre>

Agora, outro erro foi disparado:

> Fatal error: Declaration of Agenda::insert() must be compatible with that of iModel::insert() in C:\Program Files\Apache Software Foundation\Apache2.2\htdocs\index.php on line 14 

Basta adequarmos nossas classes, a essa nova realidade.

<pre name="code" class="php:firstLine[15]">public function insert( iDb $db ){}</pre>

Okay, mas e oque isso quer dizer?
  
Que os nossos métodos: <u>esperam receber</u> um objeto &#8216;iDb&#8217;. E quem é esse iDb ?

[conheço pdo, tente por favor extrair o conceito, e não apenas a implementação que estou expondo].

<pre name="code" class="php:firstLine[1]">interface iDb
	{
		public function query();
	}
	class MySql implements iDb
	{
		public function query();
	}
	class PostGre implements iDb()
	{
		public function query();
	}</pre>

Usamos para o banco MySQL dessa forma:

<pre name="code" class="php:firstLine[44]">$db = new MySql();
	$galeria = new Galeria();

	$galeria->insert( $db );</pre>

Como também poderiamos usar com a nossa class para o banco de dados Postgre:

<pre name="code" class="php:firstLine[44]">$db = new PostGre();</pre>

Ou seja, ganhamos uma flexibilidade aqui.
  
Ambos, tanto postgre, qnto mysql, possuem em comum a interface iDb. Por isso, que os métodos da class Galeria, que esperam receber um objeto iDb, aceita tanto instancias de **PostGre**, qnto de **MySql**.

Mas não podemos, fazer:

<pre name="code" class="php:firstLine[1]">class Storage
	{
		public function query(){}
	}
	$db = new Storage();
	$galeria = new Galeria();
	$galeria->insert( $db );//mandando um objeto Storage, que não implementa iDb</pre>

Será lançado um erro. Afinal, o método iModel::insert() espera receber um iDb, e não foi isso que mandamos para ele.

Nossas classes especificas, assinaram os contratos com as interfaces.
  
Na prática, temos a garantia de que podemos usar os métodos **insert(), update()** e **delete**, com exatamente esses nomes, e passando um objeto **iDb**, que sabemos que podemos usar o método **query()**;

<pre name="code" class="php:firstLine[27]">public function insert( iDb $db )
		{
			$sql = "INSERT INTO ...";
			return $db->query( $sql );
		}</pre>

Essa consistência é importante. Não importa se é MySQL, Postgre, SQL Server.. todos implementando **iDb**, temos a garantia de que o método **query()** existe, e pode ser usado.

Quando usar Abstract, e quando usar interface, é uma outra discussão.
  
Coloquei a forma com que vejo, com base em tudo o que já estudei, pesquisei e li. É isso, comentem a vontade, por favor. Me ajudará a saber sobre oque devo escrever.

Dissertar por aqui, é uma rica fonte de aprendizado para mim também. Bons estudos a todos nós.