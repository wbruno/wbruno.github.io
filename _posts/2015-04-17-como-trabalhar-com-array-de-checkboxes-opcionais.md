---
id: 3330
title: Como trabalhar com array de checkboxes opcionais
date: 2015-04-17T14:20:02+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=3330
permalink: /sql/como-trabalhar-com-array-de-checkboxes-opcionais/
categories:
  - SQL
---
Imagine a seguinte situação: você precisa fazer um sistema de cadastro de veículos para uma vitrine virtual.

<img src="/wp-content/uploads/2015/04/Screen-Shot-2015-04-17-at-13.49.12.png" alt="Screen Shot 2015-04-17 at 13.49.12" width="956" height="340" class="aligncenter size-full wp-image-3334" />

<!--more-->

O nosso sistema venderá _&#8220;carros famosos&#8221;_, por isso cada carro possui um nome (Batmóvel 1941, Tumbler, Herbie, Dick Vigarista, Penélope Charmosa).. um ano de fabricação (1941, 2008..), e um modelo (esporte, clássico, corrida, tanque de guerra)..

Um das primeiras coisas que vem a nossa mente, é [modelar os atributos dessa entidade](http://wbruno.com.br/sql/afinal-o-que-e-entidade/) **veículo**.

<pre>mysql> DESCRIBE vehicles_wrong;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(50) | YES  |     | NULL    |                |
| year  | char(4)     | YES  |     | NULL    |                |
| model | varchar(30) | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)</pre>

Tranquilo, certo ?

Um id para identificarmos cada veículo como único, o nome, ano e modelo.

Mas, o Batmóvel de 1941 tem acessórios diferentes do Tumbler de 2008 (o tanque de guerra do filme Batman Begins), certo ?

E precisamos mostrar isso para nossos usuários, dizendo se o veículo possui ou não: **ar condicionado, travas elétricas, tiro de canhão, moto acoplada para fuga**.. no caso do carro do Dick Vigarista: **turbinas propulsoras**!

## O problema

Poderíamos adicionar esses itens na entidade veículos:

<pre>mysql> DESCRIBE vehicles_wrong;
+-----------+-------------+------+-----+---------+----------------+
| Field     | Type        | Null | Key | Default | Extra          |
+-----------+-------------+------+-----+---------+----------------+
| id        | int(11)     | NO   | PRI | NULL    | auto_increment |
| name      | varchar(50) | YES  |     | NULL    |                |
| year      | char(4)     | YES  |     | NULL    |                |
| model     | varchar(30) | YES  |     | NULL    |                |
| air_con   | bit(1)      | YES  |     | NULL    |                |
| bluetooth | bit(1)      | YES  |     | NULL    |                |
+-----------+-------------+------+-----+---------+----------------+
6 rows in set (0.00 sec)</pre>

Só que ai precisamos ainda colocar:

<pre>mysql> DESCRIBE vehicles_wrong;
+------------------+-------------+------+-----+---------+----------------+
| Field            | Type        | Null | Key | Default | Extra          |
+------------------+-------------+------+-----+---------+----------------+
| id               | int(11)     | NO   | PRI | NULL    | auto_increment |
| name             | varchar(50) | YES  |     | NULL    |                |
| year             | char(4)     | YES  |     | NULL    |                |
| model            | varchar(30) | YES  |     | NULL    |                |
| air_con          | bit(1)      | YES  |     | NULL    |                |
| bluetooth        | bit(1)      | YES  |     | NULL    |                |
| parking_sensors  | bit(1)      | YES  |     | NULL    |                |
| escape_motorcyle | bit(1)      | YES  |     | NULL    |                |
| plasma_cannon    | bit(1)      | YES  |     | NULL    |                |
| cruise_control   | bit(1)      | YES  |     | NULL    |                |
| leather          | bit(1)      | YES  |     | NULL    |                |
| metallic_paint   | bit(1)      | YES  |     | NULL    |                |
| electric_locks   | bit(1)      | YES  |     | NULL    |                |
| xenon_lights     | bit(1)      | YES  |     | NULL    |                |
| nitro            | bit(1)      | YES  |     | NULL    |                |
| wings            | bit(1)      | YES  |     | NULL    |                |
+------------------+-------------+------+-----+---------+----------------+
6 rows in set (0.00 sec)</pre>

E para cada opcional extra que precisamos cadastrar iríamos adicionando uma nova coluna na tabela veículos, mesmo que o Motor de Propulsão seja um item específico do carro do Dick Vigarista, e os demais carros irão sempre deixar essa coluna em branco (como false).

Isso por si só, já mostra um grave problema de modelagem: não está escalável!

Ter que alterar o modelo e possuir diversas colunas sem valores no banco de dados é um exemplo de **modelagem desnormalizada** que devemos evitar.

## A solução

Em vez de ficarmos criando novas colunas a cada opcional novo que precisamos listar, temos que modelar melhor nossa entidade e dividir a entidade veículos em duas: veículos e opcionais, veja:

<pre>mysql> DESCRIBE optional; DESCRIBE vehicle_optional; DESCRIBE vehicles;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(50) | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)

+-------------+---------+------+-----+---------+-------+
| Field       | Type    | Null | Key | Default | Extra |
+-------------+---------+------+-----+---------+-------+
| id_vehicle  | int(11) | YES  |     | NULL    |       |
| id_optional | int(11) | YES  |     | NULL    |       |
+-------------+---------+------+-----+---------+-------+
2 rows in set (0.00 sec)

+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(50) | YES  |     | NULL    |                |
| year  | char(4)     | YES  |     | NULL    |                |
| model | varchar(30) | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)</pre>

Ficando assim, a cargo de uma terceira tabela de relacionamento o cruzamento da informação, sobre quais opcionais cada carro tem.

E para cada novo opcional extra que tivermos que cadastrar no sistema, apenas adicionamos um **linha** (registro) na tabela _optional_, em vez de uma **coluna** na tabela _veículos_. Entendeu a diferença ?

-> **Não precisamos** alterar nada no banco de dados para disponibilizar um novo opcional.

-> Não precisamos mexer nos nossos códigos backend;

-> Nem na nossa query SQL!

O impacto de adicionar opcionais (mostrar mais checkboxes) é apenas cadastrar um novo registro na tabela.

<pre>mysql> SELECT * FROM optional;
+----+------------------+
| id | name             |
+----+------------------+
|  1 | air_con          |
|  2 | bluetooth        |
|  3 | parking_sensors  |
|  4 | escape_motorcyle |
|  5 | plasma_cannon    |
|  6 | cruise_control   |
|  7 | leather          |
|  8 | metallic_paint   |
|  9 | electric_locks   |
| 10 | xenon_lights     |
| 11 | nitro            |
| 12 | wings            |
+----+------------------+
12 rows in set (0.00 sec)
</pre>

No próximo artigo irei mostrar como listar dessas entidades e fazer o CRUD dos opcionais como checkboxes. Também colocarei todos os códigos, inclusive o DUMP de criação das tabelas no github: <https://github.com/wbruno/examples/tree/gh-pages/checkboxes-opcionais>.

## Parte 2

<http://wbruno.com.br/php/como-trabalhar-com-array-de-checkboxes-opcionais-2/>
