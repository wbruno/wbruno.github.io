---
id: 1084
title: 'Listar categorias e subcategorias &#8211; php e mysql'
date: 2011-06-16T07:00:39+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1084
permalink: /sql/listar-categorias-subcategorias-php-mysql/
dsq_thread_id:
  - "2100881609"
categories:
  - SQL
---
Não raramente fazemos sites com categorias e subcategorias.

Onde a relação é de 1:N, ou seja, uma subcategoria, tem apenas uma categoria &#8216;mãe&#8217;, por assim dizer, mas várias subcategorias, podem ter a mesma mãe.
  
<!--more-->


  
Nesse caso, qndo estamos começando a programar, a resposta direta que implementamos, é algo parecido com isso:

<pre name="code" class="php">&lt;?php
	$mysqli = new mysqli('localhost','root','123', 'netropole');
	
	$sql = "SELECT categoria.id AS id_categoria, categoria.nome AS nome_categoria 
			FROM categoria 
			ORDER BY nome_categoria";
			
	$query = $mysqli->query( $sql )or die( $mysqli->error );
	
	echo '&lt;ul>'.PHP_EOL;
	
	$prev_cat = '';
	while( $dados = $query->fetch_object() )
	{
		echo '&lt;li>&lt;strong>'.$dados->nome_categoria.'&lt;/strong>'.PHP_EOL."\t".'&lt;ul>'.PHP_EOL;
		
		$sql2 = "SELECT subcategoria.id AS id_subcategoria, subcategoria.nome AS nome_subcategoria 
			FROM subcategoria WHERE subcategoria.id_categoria = {$dados->id_categoria} 
			ORDER BY nome_subcategoria";
		$query2 = $mysqli->query( $sql2 )or die( $mysqli->error );
		while( $dados2 = $query2->fetch_object() )
		{
			echo "\t\t".'&lt;li>'.$dados2->nome_subcategoria.'&lt;/li>'.PHP_EOL;
		}
		echo "\t".'&lt;/ul>'.PHP_EOL.'&lt;/li>'.PHP_EOL;
	}
	echo '&lt;/ul>';
</pre>

Fazemos uma query interna, para cada categoria, buscando uma sub daquela categoria.
  
Com isso, tivemos que usar um loop encaixado. (Hurgh!!)

Porém, fazendo um JOIN na query, e usando simples condicionais, podemos fazer o mesmo com apenas uma consulta ao banco, e apenas um loop:

<pre name="code" class="php">&lt;?php
	$mysqli = new mysqli('localhost','root','123', 'netropole');

	$sql = "SELECT categoria.id AS id_categoria, categoria.nome AS nome_categoria,
		subcategoria.id AS id_subcategoria, subcategoria.nome AS nome_subcategoria
			FROM categoria
			INNER JOIN subcategoria
			ON categoria.id = subcategoria.id_categoria
			ORDER BY nome_categoria, nome_subcategoria";

	$query = $mysqli->query( $sql )or die( $mysqli->error );

	echo '&lt;ul>'.PHP_EOL;

	$prev_cat = '';
	while( $dados = $query->fetch_object() )
	{
		if( $prev_cat!=$dados->nome_categoria )
		{
			if( $prev_cat!='' ) echo "\t".'&lt;/ul>'.PHP_EOL.'&lt;/li>'.PHP_EOL;

			echo '&lt;li>&lt;strong>'.$dados->nome_categoria.'&lt;/strong>'.PHP_EOL."\t".'&lt;ul>'.PHP_EOL;
			$prev_cat = $dados->nome_categoria;
		}
		echo "\t\t".'&lt;li>'.$dados->nome_subcategoria.'&lt;/li>'.PHP_EOL;
	}
	echo "\t".'&lt;/ul>'.PHP_EOL.'&lt;/li>'.PHP_EOL.'&lt;/ul>';
</pre>

DUMP completo do SQL usado:

<pre name="code" class="sql">-- phpMyAdmin SQL Dump
-- version 3.1.2
-- http://www.phpmyadmin.net
--
-- Servidor: localhost
-- Tempo de Geração: Jun 20, 2011 as 12:31 AM
-- Versão do Servidor: 5.1.31
-- Versão do PHP: 5.2.8

SET SQL_MODE="NO_AUTO_VALUE_ON_ZERO";

--
-- Estrutura da tabela `categoria`
--

CREATE TABLE IF NOT EXISTS `categoria` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nome` varchar(100) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=10 ;

--
-- Extraindo dados da tabela `categoria`
--

INSERT INTO `categoria` (`id`, `nome`) VALUES
(1, 'Carros, peças e Acessórios'),
(2, 'Casa e Escritório'),
(3, 'Restaurantes, Alimentos e Bebidas'),
(4, 'Diversão, Lazer, Entretenimento'),
(5, 'Educação, Cultura, Meios de Comunicação'),
(6, 'Informática e Serviços Gráficos'),
(7, 'Moda e Beleza'),
(8, 'Animais de Estimação e Pet Shops'),
(9, 'Clínicas, Hospitais e Consultórios Médicos');

-- --------------------------------------------------------

--
-- Estrutura da tabela `subcategoria`
--

CREATE TABLE IF NOT EXISTS `subcategoria` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `id_categoria` int(11) NOT NULL,
  `nome` varchar(100) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=68 ;

--
-- Extraindo dados da tabela `subcategoria`
--

INSERT INTO `subcategoria` (`id`, `id_categoria`, `nome`) VALUES
(1, 1, 'Aluguel de automóveis'),
(2, 1, 'Pneus'),
(3, 1, 'Carretas'),
(4, 1, 'Consórcios'),
(5, 1, 'Engates'),
(6, 1, 'Vidro de Segurança'),
(7, 1, 'Embreagens'),
(8, 1, 'Filtro de Ar'),
(9, 1, 'Martelinho de Ouro'),
(10, 2, 'Assessoria do Lar'),
(11, 2, 'Avaliadores'),
(12, 2, 'Corretor de Imóveis'),
(13, 2, 'Imobiliárias'),
(14, 2, 'Conserto de Fogões'),
(15, 2, 'Almofadas'),
(16, 2, 'Piscinas'),
(17, 2, 'Grama'),
(18, 3, 'Açougues'),
(19, 3, 'Castanhas'),
(20, 3, 'Cereais'),
(21, 3, 'Frutos do Mar'),
(22, 3, 'Laticínios'),
(23, 3, 'Mel'),
(24, 3, 'Bares e Café'),
(25, 3, 'Cyber Café'),
(26, 4, 'Agências de Casamento'),
(27, 4, 'Artigos de Carnaval'),
(28, 4, 'Cinemas'),
(29, 4, 'Games'),
(30, 4, 'Boliche'),
(31, 4, 'Museus'),
(32, 4, 'Teatros'),
(33, 4, 'Músicos'),
(34, 5, 'Curso de Artesanato'),
(35, 5, 'Escola de Futebol'),
(36, 5, 'Cursos Livres'),
(37, 5, 'Aluguel de Livros'),
(38, 5, 'Bibliotecas'),
(39, 5, 'Uniformes'),
(40, 6, 'Impressoras'),
(41, 6, 'Notebooks'),
(42, 6, 'Projetores'),
(43, 6, 'VOIP'),
(44, 6, 'Acabamentos Gráficos'),
(45, 6, 'Artigos de Carnaval'),
(46, 6, 'Impressão Digital'),
(47, 7, 'Clínicas de Estética'),
(48, 7, 'Bronzeamento Artificial'),
(49, 7, 'Fraldas'),
(50, 7, 'Botas'),
(51, 7, 'Bonés'),
(52, 7, 'Camisetas'),
(53, 7, 'Loja de Malhas'),
(54, 8, 'Canis'),
(55, 8, 'Acupuntura em animais'),
(56, 8, 'Veterinárias'),
(57, 8, 'Pet Shop'),
(58, 8, 'Rações'),
(59, 8, 'Taxi Dog'),
(60, 8, 'Passeadores de cães'),
(61, 9, 'Clínica de Massagem'),
(62, 9, 'Clínica de Psicologia'),
(63, 9, 'Clínica de Reabilitação'),
(64, 9, 'Ultra-Som'),
(65, 9, 'Farmácias e Drogarias'),
(66, 9, 'Lenstes de Contato'),
(67, 9, 'Dentistas');

-- --------------------------------------------------------
</pre>

é isso ^^

Okay, talvez já existam tutoriais parecidos por ai, e eu mesmo já escrevi esse script no Fórum.iMasters respondendo dúvidas de usuarios, porém eu quis deixar registrado aqui, nesse meu &#8216;repositório&#8217;.

Até a próxima.