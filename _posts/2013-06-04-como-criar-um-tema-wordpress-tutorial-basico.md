---
id: 2988
title: 'Como criar um tema WordPress &#8211; Tutorial Básico'
date: 2013-06-04T07:00:44+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2988
permalink: /wordpress/como-criar-um-tema-wordpress-tutorial-basico/
dsq_thread_id:
  - "2100751981"
categories:
  - WordPress
tags:
  - tableless
---
[<img src="http://wbruno.com.br/wp-content/uploads/2013/05/wp.png" alt="wp" width="504" height="279" class="aligncenter size-full wp-image-3003" srcset="http://wbruno.com.br/wp-content/uploads/2013/05/wp.png 504w, http://wbruno.com.br/wp-content/uploads/2013/05/wp-300x166.png 300w" sizes="(max-width: 504px) 100vw, 504px" />](http://wbruno.com.br/wp-content/uploads/2013/05/wp.png)
  
Se você chegou até esse post pela busca, provavelmente este não é o primeiro tutorial sobre criar temas no wordpress que vc está lendo. Então, vou pular algumas coisas que sei que já falaram nos outros links.
  
<!--more-->

## É apenas um site

WordPress é apenas uma camada do site. Só o CMS que vai ser colocado para seu cliente administrar via painel os posts e páginas.

Se você sabe fazer sites, então vc está muito perto de conseguir fazer um tema wordpress.
  
Comece como vc começaria qualquer outro site: do recorte html.

Sim, estou falando para você fazer isoladamente. Se esquecendo que no final, usará o wordpress. Faça o seu recorte css tableless da melhor forma possível, como vc faria normalmente.

## Usando as funções

Creio que as 3 funções mais básicas são: <var>get_header()</var>, <var>get_footer()</var> e <var>get_sidebar()</var>. Basicamente o que elas fazem é apenas um include dos arquivos: <var>header.php</var>, <var>footer.php</var> e <var>sidebar.php</var> respectivamente.

Então os seus arquivos: <var>index.php</var>, <var>404.php</var>, <var>page.php</var>, <var>single.php</var>, <var>archive.php</var> e <var>search.php</var>, terão uma anatomia muito próxima disso:

<pre>&lt;?php
/**
 * The main template file.
 *
 * This is the most generic template file in a WordPress theme
 * and one of the two required files for a theme (the other being style.css).
 * It is used to display a page when nothing more specific matches a query.
 * For example, it puts together the home page when no home.php file exists.
 *
 * Learn more: http://codex.wordpress.org/Template_Hierarchy
 *
 * @package WordPress
 * @subpackage wbruno
 * @since wbruno 0.0.1
 */

get_header(); ?>

	&lt;main id="content" class="fleft" role="main">
		&lt;?php if (have_posts()) : while (have_posts()) : the_post(); ?>

			&lt;?php get_template_part( 'content' ); ?>

		&lt;?php endwhile; else: ?>

			&lt;article class="not-found">
				&lt;p>&lt;?php _e('Desculpe, nenhum post corresponde aos seus crit&eacute;rios.', 'wbruno'); ?>&lt;/p>
			&lt;/article>

		&lt;?php endif; ?>

		&lt;div class="fright">
			&lt;?php posts_nav_link(' &#8212; ', __('&laquo; Anterior', 'wbruno'), __('Pr&oacute;xima &raquo;', 'wbruno')); ?>
		&lt;/div>

	&lt;/main>&lt;!-- /content -->

&lt;?php get_sidebar(); ?>
&lt;?php get_footer(); ?>
</pre>

Onde vemos claramente os includes do topo, sidebar e rodapé.

## Codex

O WP é bem documentado. Tendo alguma dúvida: pesquise no codex.
  
Por exemplo, não faz sentido eu explicar o que é e o que faz cada um dos arquivos básicos de um tema, se o codex já tem um link falando tudo isso: <a href="http://codex.wordpress.org/pt-br:Hierarquia_de_Modelos_Wordpress" rel="nofollow">http://codex.wordpress.org/pt-br:Hierarquia_de_Modelos_Wordpress</a>. Dá uma lida lá.

## Theme Check

Esse plugin é essencial para desenvolver um tema de qualidade. Ele vai te apontar alguns erros como encoding, funções deprecated e algumas boas práticas.
  
Use: <a href="http://wordpress.org/plugins/theme-check/" rel="nofollow">http://wordpress.org/plugins/theme-check/</a>.

### Validador w3c

Eu não disse que um wordpress é apenas um site ?
  
Então todas as boas práticas de um site também valem para um tema wordpress. Portanto, valide sempre o html e css do seu tema: <a href="http://validator.w3.org/" rel="nofollow">http://validator.w3.org/</a>.

## functions.php

É nesse arquivos que vc fará todas as intervenções que quiser no core do wordpress, como por exemplo mudar a forma com que o cms lista as categorias.
  
É importante saber que a única pasta que te pertence quando vc está desenvolvendo um tema, é a própria pasta do tema, localizada em: <var>wp-content/themes/nome_do_seu_tema/</var>, e nada mais.

Não edite de forma nenhuma os outros arquivos do wordpress, afinal uma atualização do core acabaria quebrando as suas modificações.

Mas ele não é obrigatório, e vc pode ter um functions.php em branco e mesmo assim o seu tema funcionará.

## Arquivos básicos e obrigatórios

Você sempre vai precisar ter esses, na raiz do seu tema:

  * **screenshot.png** &#8211; screenshot em 600&#215;450 de como o tema ficará, para vc visualizar no painel de escolha de temas um &#8220;preview&#8221;
  * **style.css** &#8211; independente se vc usará outros arquivos .css externos, o css base do tema, deve ser esse arquivo na raiz do tema. Os comentários iniciais dele, é que informarão ao painel do wp o que o seu tema é. 
    <pre>/*
	Theme Name: wbruno
	Theme URI: http://wbruno.com.br
	Description: Tema do blog wbruno
	Author: William Bruno
	Author URI: http://wbruno.com.br
	Version: 0.0.3
	Tags: light, two-columns, fixed-width, left-sidebar, flexible-width, sticky-post
	License: GNU General Public License v2 or later
	License URI: http://www.gnu.org/licenses/gpl-2.0.html
*/
</pre>

  * **editor-style.css** &#8211; é um arquivos .css opcional que vc pode criar, que se existir será usado para formatar o editor dentro do painel do wordpress.
  * **single.php** &#8211; Quando vc estiver visualizando um post aberto, é esse arquivo que está sendo mostrado.
  * **page.php** &#8211; Este aqui é para uma página.

Algumas coisa obrigatórias do <var>style.css</var> e do <var>functions.php</var> o plugin Theme Check que eu indiquei, lhe dirá para fazer.

## White Themes

Eu comecei assim. Pegando um tema padrão do wordpress e estilizando ele, até chegar no resultado que eu queria. Também é um caminho, mas não é a bala de prata. Talvez o seu tema seja tão específico que você não encontre nenhum white theme parecido para personalizar.

Porém, ainda assim vale a pena dar uma estudada em alguns para aprender como o author fez aquilo que vc quer, ou entender melhor como desenvolver o seu próprio do zero.

No meu github, há o tema que utilizo aqui no blog: <a href="https://github.com/wbruno/blog-dev" rel="external">https://github.com/wbruno/blog-dev</a>. Ele é bem minimalista, e sempre será um &#8220;white theme&#8221;. Então pode clonar o projeto e dar uma estudada lá.

Fique a vontade para mandar um pull request do seu fork caso você tenha feito alguma implementação legal no projeto. =)