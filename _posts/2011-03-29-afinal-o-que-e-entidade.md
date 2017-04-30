---
id: 392
title: Afinal, o que é uma Entidade ?
date: 2011-03-29T07:15:46+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=392
permalink: /sql/afinal-o-que-e-entidade/
dsq_thread_id:
  - "2100962833"
categories:
  - SQL
---
Antes de mais nada, não vou começar falando de SQL como todo mundo por ai faz [ copiando trechos da <a href="http://pt.wikipedia.org/wiki/Sql" target="_blank">Wikipedia</a> ]. Se você está lendo meu blog, então vc sabe o que é SQL, sabe para que serve, e até provavelmente já trabalha com essa linguagem. Okay, vamos prosseguir.

Um conceito importante e interessante, mas que é fatalmente sonegado aos programadores, é o <a href="http://pt.wikipedia.org/wiki/Entidade_(inform%C3%A1tica)" target="_blank">conceito de <strong>entidade</strong></a> [Basta tentar pesquisar por este termo, e notar como é escasso o conteúdo].

O resultado, são sistemas <a href="http://pt.wikipedia.org/wiki/Modelagem_de_dados" target="_blank">mal modelados</a>, <a href="http://pt.wikipedia.org/wiki/Normaliza%C3%A7%C3%A3o_de_dados" target="_blank">não normalizados</a>, em que a aplicação tenta resolver diversos problemas da estrutura. Onde qualquer novo requisito, gera um grande transtorno, pois a análise para criação do modelo, não foi feita corretamente, de modo a deixar a estrutura robusta e expansível.

<!--more-->


  

  
Um exercício rápido:

> _Volante, Pára-choque, Retrovisores, Câmbio, Chassis, Rodas, Motor, Portas&#8230;_

E ai, o que lhe veio a mente ? Qual objeto do nosso mundo, agrega essas partes que citei ?
  
Espero que a sua resposta seja &#8216;um carro&#8217;. Faz parte do senso comum.

Mais uma vez:

> _Galhos, Folhas, Raíz, Tronco, Copa, Calotas.._

Uma árvore certo ? só as &#8216;Calotas&#8217; que parecem não estar no lugar correto, pois não combinam com os outros itens, e não conseguimos imaginar que as calotas, devam pertencer a nossa árvore.



Melhor mover as Calotas para o Carro ali de cima, no senso comum, para se encaixar melhor em uma normalidade aceitável.

Ao iniciar o levantamento de informações, o processo é mais ou menos parecido com esse.
  
O Carro, e a Árvore são as nossas **entidades** e cada um dos itens que citei, são os **atributos** particulares dessas entidades.
  
A idéia é saber a quem deve pertencer cada atributo, e sermos capazes de definirmos as entidades do nosso sistema.



**Formalmente:**

<p style="margin-bottom: 30px;">
  Uma entidade possui atributos.<br /> Os atributos são as características, e não devem conter um grupo de informações.<br /> Não existem entidades com menos de 2 atributos, logo, cada entidade, é em si, um grupo de atributos.
</p>

Talvez esteja confuso até aqui, mas trazendo de forma livre para a nossa realidade, cada Entidade é uma tabela, e cada Atributo é cada uma das colunas dessas tabelas.

O ponto que quero levantar, é a compreensão do conceito.
  
Se tenho que fazer um cadastro de usuário, preciso pensar o que a <u>entidade usuário</u> significa para o meu sistema, e o que preciso saber dela ou não.

<pre name="code" class="sql">CREATE TABLE `test`.`usuario` (
   `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY ,
   `nome` VARCHAR( 50 ) NOT NULL
) ENGINE = InnoDB;
</pre>

Até aqui bem simples. A nossa entidade usuario possui um _\`nome\`_, e um _\`id\`_, que é um identificador único desse objeto no nosso modelo.

Agora o cliente nos informa que ele precisa saber dos usuarios dele, pelo menos:
  
-> um telefone residencial, e
  
-> um celular.

Num primeiro momento, a nossa reação é adicionarmos essas informações à entidade usuario, pois o telefone e o celular pertencem respectivamente, a cada usuário nosso.

<pre name="code" class="sql">ALTER TABLE `usuario` ADD `telefone` VARCHAR( 14 ) NOT NULL ,
ADD `celular` VARCHAR( 14 ) NOT NULL </pre>

[<img src="http://wbruno.com.br/wp-content/uploads/2011/03/tab.png" alt="" title="tab" width="609" height="120" class="aligncenter size-full wp-image-394" srcset="http://wbruno.com.br/wp-content/uploads/2011/03/tab.png 609w, http://wbruno.com.br/wp-content/uploads/2011/03/tab-300x59.png 300w" sizes="(max-width: 609px) 100vw, 609px" />](http://wbruno.com.br/wp-content/uploads/2011/03/tab.png)

Porém, nosso chefe, vem e nos informa que agora ele precisa também do Telefone Comercial do nosso usuário, e quem sabe talvez um Telefone de Contato.. é nesse momento, que o nosso modelo pode naufragar ou não.

Adicionar mais essas 2 colunas a tabela, seria um erro, no ponto de vista da modelagem de negócios, pois estaríamos novamente, subestimando a aplicação. E se lá pra frente, o cara resolver incluir o Pager (ainda usam isso? hahauhaua), ou Nextel do camarada ?

Nesta hora, deveria começar a ficar claro que essa expansão, clama por uma nova entidade na nossa modelagem.

<pre name="code" class="sql">ALTER TABLE `usuario` DROP `telefone` , DROP `celular` ;
</pre>

Estrutura da nova entidade:
  
[<img src="http://wbruno.com.br/wp-content/uploads/2011/03/tab2.png" alt="" title="tab2" width="603" height="122" class="aligncenter size-full wp-image-396" srcset="http://wbruno.com.br/wp-content/uploads/2011/03/tab2.png 603w, http://wbruno.com.br/wp-content/uploads/2011/03/tab2-300x60.png 300w" sizes="(max-width: 603px) 100vw, 603px" />](http://wbruno.com.br/wp-content/uploads/2011/03/tab2.png)
  
Dados cadastrados:
  
[<img src="http://wbruno.com.br/wp-content/uploads/2011/03/reg.png" alt="" title="reg" width="269" height="194" class="aligncenter size-full wp-image-395" />](http://wbruno.com.br/wp-content/uploads/2011/03/reg.png)

Portanto, se precisamos de mais formas de contato, como o Nextel, basta adicionarmos um registro a essa tabela, e isso pode ser facilmente feito na nossa aplicação, sem a necessidade de alterarmos a estrutura do modelo.

<pre name="code" class="sql">INSERT INTO `test`.`contato` (`id`, `nome`) VALUES (NULL, 'Nextel');</pre>

A única questão não respondida ainda, é como vincular os dados do usuário a esta nossa nova entidade. Fazemos então, outra tabela, já bem normalizada, da seguinte forma:

<pre name="code" class="sql">CREATE TABLE `test`.`contato_usuario` (
    `id_usuario` INT NOT NULL ,
    `id_contato` INT NOT NULL ,
    `descricao` VARCHAR( 70 ) NOT NULL
) ENGINE = InnoDB;
</pre>

Essa nossa nova tabela, será responsável por fazer a ligação entre as nossas entidades.
  
[<img src="http://wbruno.com.br/wp-content/uploads/2011/03/reg2.png" alt="" title="reg2" width="360" height="143" class="aligncenter size-full wp-image-397" srcset="http://wbruno.com.br/wp-content/uploads/2011/03/reg2.png 360w, http://wbruno.com.br/wp-content/uploads/2011/03/reg2-300x119.png 300w" sizes="(max-width: 360px) 100vw, 360px" />](http://wbruno.com.br/wp-content/uploads/2011/03/reg2.png)

A relação entre as tabelas é evidente, e o nosso JOIN, para resgatar esses dados fica:

<pre name="code" class="sql">SELECT `usuario`.`id` AS `id_usuario` , `usuario`.`nome` AS `nome_usuario` ,
  `contato`.`nome` AS `nome_contato` , `contato_usuario`.`descricao`
    FROM `usuario`
        INNER JOIN `contato_usuario` ON `usuario`.`id` = `contato_usuario`.`id_usuario`
        INNER JOIN `contato` ON `contato`.`id` = `contato_usuario`.`id_contato`
</pre>

Saída:
  
[<img src="http://wbruno.com.br/wp-content/uploads/2011/03/reg3.png" alt="" title="reg3" width="426" height="134" class="aligncenter size-full wp-image-404" srcset="http://wbruno.com.br/wp-content/uploads/2011/03/reg3.png 426w, http://wbruno.com.br/wp-content/uploads/2011/03/reg3-300x94.png 300w" sizes="(max-width: 426px) 100vw, 426px" />](http://wbruno.com.br/wp-content/uploads/2011/03/reg3.png)

Continuando, surgem novos atributos:

> _data de nascimento, cidade natal, email, estado civil.._

Precisamos dividir esses atributos nas nossas entidades.
  
data de nascimento, cidade natal e estado civil, cabem muito bem na entidade usuario.
  
Já o email, podemos colocar na entidade contato, concorda ?

Se lá pra frente, precisarmos de um &#8216;email_secundario&#8217;, para proteção do sistema, onde o usuário poderá resgatar a senha dele na nossa aplicação, bastará novamente, inserirmos um registro na entidade contato, sem a menor alteração do modelo que criamos.

Esse particionamento que fizemos tem o seu custo. Maior complexidade do modelo, queda de performance(afinal, agora consultamos 3 tabelas, e não apenas uma), em contrapartida com os ganhos que essa modelagem trouxe a estrutura da nossa aplicação.
  
Analise bem os requisitos do seu sistema antes de implementá-lo. Não tome todo e qualquer tutorial como lei, ou verdade absoluta.

Dump completo do SQL usado:

<div class="spoler">
  <pre name="code" class="sql">
-- phpMyAdmin SQL Dump
-- version 3.3.8.1
-- http://www.phpmyadmin.net
--
-- Servidor: localhost
-- Tempo de Geração: Mar 29, 2011 as 02:54 AM
-- Versão do Servidor: 5.5.8
-- Versão do PHP: 5.3.4

SET SQL_MODE="NO_AUTO_VALUE_ON_ZERO";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8 */;

--
-- Banco de Dados: `test`
--

-- --------------------------------------------------------

--
-- Estrutura da tabela `contato`
--

CREATE TABLE IF NOT EXISTS `contato` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nome` varchar(40) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=5 ;

--
-- Extraindo dados da tabela `contato`
--

INSERT INTO `contato` (`id`, `nome`) VALUES
(1, 'Telefone Residencial'),
(2, 'Telefone Comercial'),
(3, 'Celular'),
(4, 'Nextel');

-- --------------------------------------------------------

--
-- Estrutura da tabela `contato_usuario`
--

CREATE TABLE IF NOT EXISTS `contato_usuario` (
  `id_usuario` int(11) NOT NULL,
  `id_contato` int(11) NOT NULL,
  `descricao` varchar(70) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Extraindo dados da tabela `contato_usuario`
--

INSERT INTO `contato_usuario` (`id_usuario`, `id_contato`, `descricao`) VALUES
(1, 2, '(11) 1234-5678'),
(1, 4, '55*11*1111'),
(2, 1, '(12) 4321-8765'),
(2, 2, '(11) 8765-4321'),
(2, 4, '55*22*2222');

-- --------------------------------------------------------

--
-- Estrutura da tabela `usuario`
--

CREATE TABLE IF NOT EXISTS `usuario` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nome` varchar(50) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=latin1 AUTO_INCREMENT=3 ;

--
-- Extraindo dados da tabela `usuario`
--

INSERT INTO `usuario` (`id`, `nome`) VALUES
(1, 'Bruno'),
(2, 'Silveira');
</pre>
</div>