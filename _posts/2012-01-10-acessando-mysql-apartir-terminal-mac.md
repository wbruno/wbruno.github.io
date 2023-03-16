---
id: 1714
title: Acessando o mysql apartir do terminal no MAC
date: 2012-01-10T10:34:36+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1714
permalink: /mac/acessando-mysql-apartir-terminal-mac/
dsq_thread_id:
  - "2101058896"
categories:
  - MAC
tags:
  - terminal
---
``` js
Mac:~ william$ alias mysql=/usr/local/mysql/bin/mysql
Mac:~ william$ alias mysqladmin=/usr/local/mysql/bin/mysqladmin
Mac:~ william$ mysql -u root -p wordpress
Enter password:
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 62
Server version: 5.5.17 MySQL Community Server (GPL)

Copyright (c) 2000, 2011, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show tables;
+-----------------------+
| Tables_in_wordpress   |
+-----------------------+
| wp_commentmeta        |
| wp_comments           |
| wp_links              |
| wp_options            |
| wp_postmeta           |
| wp_posts              |
| wp_term_relationships |
| wp_term_taxonomy      |
| wp_terms              |
| wp_usermeta           |
| wp_users              |
+-----------------------+
11 rows in set (0.00 sec)

mysql>
```

Reiniciando:

```/usr/local/mysql/bin/mysqladmin -uroot -p shutdown```

start

```sudo /usr/local/mysql/bin/mysqld_safe &
```
