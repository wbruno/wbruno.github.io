---
id: 1720
title: Capturar lista de email dos comentários do seu WordPress e outras queries úteis
date: 2012-01-11T07:00:12+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1720
permalink: /wordpress/capturar-lista-de-email-dos-comentarios-seu-wordpress-outras-queries-uteis/
categories:
  - WordPress
---
Boas galera,

resolvi colocar algumas queries úteis aqui. Coisa bem simples mesmo.

<!--more-->

## Capturar lista de email dos comentários do seu WordPress

``` sql
SELECT DISTINCT(comment_author_email), comment_author
FROM `wp_comments`
WHERE comment_author_email<>''```

Nessa query eu peço apenas o nome e o email do autor do comentário.

O WHERE ali, é para excluir os trackback, pois eles são inseridos nessa tabela também, mas não enviam um email válido.

o DISTINCT serve para limpar um pouco o mailing, e não trazer nenhum email repetido. Eu poderia ter feito o mesmo usando um GROUP BY.

## Remover revisões de posts

Dificilmente eu uso esse recurso(para recuperar algo), mas como ele é automático, vários e vários registros são criados no banco por causa dele.

``` sql
SELECT * FROM wp_posts WHERE post_type = 'revision';
```

Basta trocar o SELECT * por um DELETE, e teremos excluido as revisões. Aqui, contabilizou quase 500 revisões.

## Remover rascunhos automáticos

Um pouco menos &#8220;problemático&#8221;, que as revisões, mas mesmo assim, não deixam de ser &#8220;sujeiras&#8221; no banco.

``` sql
SELECT * FROM `wp_posts` WHERE `post_status` = 'auto-draft'```

No instante em que rodei essa query, só peguei um único registro.

## O número de registros no banco, não bate com meu número de posts

Calma, é assim mesmo. &#8220;Estranhamente&#8221;, do ponto de vista de modelagem SQL, o WordPress usa a tabela wp_posts, para também guardar o path dos arquivos que subimos no meio do post(imagens, videos..)

``` sql
SELECT * FROM `wp_posts` WHERE `post_type` <> 'post';
```

**Não delete!** a menos que vc saiba oque está fazendo. (Excluir aqui, não apaga o arquivo real, portanto não quebra o seu post).

É apartir dessa tabela que o WP faz a listagem que vemos em Media -> Library

(note que temos post\_type como inhreit, e post\_parent como o ID do post, no qual subimos aquela imagem).

Bom, acho que é isso.

Se tiverem mais idéias de queries ou alguma outra forma de conseguir esses dados(resultados), me digam. =)

E se vc usou, comente por aqui também.

## Todas essas operações são por sua própria conta e risco

Salve um backup antes de brincar com o seu banco, e eu não me responsabilizo por absolutamente nada. Nem tenho como. =)
