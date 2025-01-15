---
id: 3344
title: Como trabalhar com array de checkboxes opcionais 2
date: 2015-04-18T20:19:36+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/?p=3344
permalink: /php/como-trabalhar-com-array-de-checkboxes-opcionais-2/
categories:
  - PHP
---
Dando continuidade ao artigo anterior:

<http://wbruno.com.br/sql/como-trabalhar-com-array-de-checkboxes-opcionais/>

<img src="/wp-content/uploads/2015/04/Screen-Shot-2015-04-18-at-20.10.45.png" alt="Screen Shot 2015-04-18 at 20.10.45" width="1392" height="668" class="aligncenter size-full wp-image-3346" />

Iremos escrever enfim, os códigos para fazer esse CRUD com checkboxes.

<!--more-->



Lembrando que o intuito do artigo não é ensinar programação orientada a objetos. Então irei deixar o script php o mais simples possível, para que você possa extrair e então montar o seu dentro da sua estrutura/framework.

## Listando os opcionais do banco

A listagem dos itens é super trivial:

``` php
<?php
  $query = $mysqli->query('SELECT id, name FROM optional');
  while($row = $query->fetch_object()) {
?>
    <label>
      <input type="checkbox" name="optional[]" value="<?php echo $row->id; ?>" />
    <?php echo $row->name; ?></label>
<?php
  }
?>
```

Apenas conecto no MySQL com a lib **mysqli** e imprimo um checkbox para cada registro da tabela.

## DESCRIBE TABLE optional_vehicle

Ainda não estamos preocupados com trazer os checkboxes marcados, pois precisamos entender como utilizar a tabela optional_vehicle.

Ela faz um relacionamento N:N (um veículo para N opcionais, e 1 opcional para N veículos).

Para inserir nessa tabela, precisamos mais ou menos da seguinte string sql:

``` sql
INSERT INTO vehicle_optional (id_vehicle, id_optional) VALUES (42, 1),(42 2)
```

Nessa query acima, estamos inserindo o opcional 1 e 2 para o veículo 42.

Se quisessemos inserir mais o opcional 5, bastaria:

``` sql
INSERT INTO vehicle_optional (id_vehicle, id_optional) VALUES (42, 1),(42, 2),(42, 5)
```

Okay ?

Fazer essa string é uma simples maniplação de array. Lembra que o name do checkbox é <var>name=&#8221;optional[]&#8221;</var> então, no php irá chegar um array:

``` bash
_POST['optional'][0], $_POST['optional'][1], $_POST['optional'][2]
```

Visto isso, vamos montar o INSERT:

``` php
//optional insert
  $values = [];
  foreach($optionals AS $id_optional) {
    $values[] = "({$id}, {$id_optional})";
  }
  $values = implode(',', $values);

  $sql = "INSERT INTO vehicle_optional (id_vehicle, id_optional) VALUES {$values}";
  echo $sql;
  $query = $mysqli->query($sql)or die($mysqli->error);
```

Simples, não ? a saída do echo $sql, será a string que escrevi acima.

Comecei pelos opcionais para matar logo a sua curiosidade, mas para deixar registrado o INSERT simples do veículo tem apenas as colunas que são atributos da entidade veículo:

``` bash
sql = "INSERT INTO vehicles (id, name, year, model) VALUES(NULL, '{$name}', '{$year}', '{$model}')";
  echo $sql, '<br /><br />';
  $query = $mysqli->query($sql)or die($mysqli->error);

  $id = $mysqli->insert_id;//ultimo id inserido no banco
```

## Os truques

As duas queries acima são bem triviais e você já está mais do que acostumado com elas no seu dia a dia. Só existem 2 truques no server-side para essa modelagem.

O primeiro é:

### Delete tudo, depois insira novamente

O comportamento do input type=&#8221;checkbox&#8221; do html é enviar para o server-side **apenas** os **checkboxes marcados**. Então aqueles que não estiverem no estado **checked**.

Tente imaginar a lógica de atualizar os opcionais de um carro. Ele já possui alguns cadastrados no banco. No submit do formulário você precisa remover os que não foram marcados, inserir os novos e com os que não alteraram não fazer nada. Complexo, não?

Um truque muito mais simples é remover tudo e depois inserir tudo o que vier.

``` sql
DELETE FROM vehicle_optional WHERE id_vehicle = 42;
INSERT INTO vehicle_optional (id_vehicle, id_optional) VALUES (42, 1),(42, 2),(42, 5);
```

### Marque os checkboxes

Agora precisamos marcar os checkboxes na listagem durante a edição de um registro.

O truque aqui é puramente SQL e se baseia em uma subquery.

``` sql
SELECT `id`, `name`, (SELECT 'checked' FROM vehicle_optional WHERE id_vehicle = 1 AND id_optional = optional.id) AS `checked` FROM `optional`;
```

Pense no seguinte:

-> Temos que listar **todos os opcionais**

Fácil, já tinhamos feito isso.

-> E dizer quem está marcado ou não.

Aqui que entra a subquery.

``` sql
(SELECT 'checked' FROM vehicle_optional WHERE id_vehicle = 1 AND id_optional = optional.id)
```

ela vai trazer a string &#8216;checked&#8217; apelidada como a coluna \`checked\` <var>AS `checked`</var> apenas nos registros do veiculo id = 1 que tiverem marcados. o/

``` sql
mysql>SELECT `id`, `name`, (SELECT 'checked' FROM vehicle_optional WHERE id_vehicle = 1 AND id_optional = optional.id) AS `checked` FROM `optional`;
+----+------------------+---------+
| id | name             | checked |
+----+------------------+---------+
|  1 | air_con          | checked |
|  2 | bluetooth        | checked |
|  3 | parking_sensors  | NULL    |
|  4 | escape_motorcyle | NULL    |
|  5 | plasma_cannon    | NULL    |
|  6 | cruise_control   | checked |
|  7 | leather          | NULL    |
|  8 | metallic_paint   | NULL    |
|  9 | electric_locks   | NULL    |
| 10 | xenon_lights     | NULL    |
| 11 | nitro            | NULL    |
| 12 | wings            | NULL    |
+----+------------------+---------+
12 rows in set (0.00 sec)
```

E então vamos simplesmente imprimir isso no nosso input:

``` html
<input type="checkbox" name="optional[]" value="<?php echo $row->id; ?>" <?php echo $row->checked; ?>/>
```
Mágica.

## Código no GitHub

<https://github.com/wbruno/examples/tree/gh-pages/checkboxes-opcionais>
