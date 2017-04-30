---
id: 2291
title: Mostrando featured image e custom fields no feed do WordPress
date: 2012-08-10T18:57:07+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2291
permalink: /wordpress/mostrando-featured-image-e-custom-fields-no-feed-do-wordpress/
dsq_thread_id:
  - "2101881937"
categories:
  - WordPress
---
Sabendo ler o namespace **<content:encoded>**, do feed do wordpress, conforme eu postei aqui:

[Ler namespace xml php, usando a simplexml – content:encoded – feed WordPress](http://wbruno.com.br/2012/08/08/ler-namespace-xml-php-usando-a-simplexml/ "Ler namespace xml php, usando a simplexml – content:encoded – feed WordPress")

Podemos adicionar mais coisas interessantes nesse nosso feed, como os **Custom Fields**.
  
<!--more-->


  
Eu já havia feito um add_filter para o featured image:

<pre name="code" class="php">/**
 * 
 */
function featured_image_feed($content) {
	global $post;

	if ( has_post_thumbnail( $post->ID ) ){
		$content = '' . get_the_post_thumbnail( $post->ID, 'thumbnail' ) . '' . $content;	
	}
	return $content;
}
add_filter('the_content_feed', 'featured_image_feed');
</pre>

E agora, fiz mais um para os custom fields:

<pre name="code" class="php">/**
 * 
 */
function custom_fields_feed($content) {
    if (is_feed()) {
        $meta =  get_post_custom(get_the_ID());
        $content .= implode( ',', $meta['publico'] );
    }
    return $content;
}
add_filter('the_content_feed', 'custom_fields_feed');</pre>

Com esses dois hooks no arquivo **functions.php** do nosso tema, chegarão no name espace :encoded, o featured image e os custom fields(key: publico).

Note que ali eu fiz <var>$meta[&#8216;publico&#8217;]</var>. Se o teu custom field, tiver outra key, vc deve alterar esta linha.