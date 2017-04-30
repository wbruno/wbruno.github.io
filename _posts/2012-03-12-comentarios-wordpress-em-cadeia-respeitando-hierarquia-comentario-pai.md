---
id: 1856
title: 'Comentários do WordPress em cadeia &#8211; Respeitando hierarquia do comentário pai'
date: 2012-03-12T07:00:56+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=1856
permalink: /wordpress/comentarios-wordpress-em-cadeia-respeitando-hierarquia-comentario-pai/
dsq_thread_id:
  - "2102281845"
categories:
  - WordPress
---
Refiz recentemente o novo tema do blog da Locaweb:
  
<http://wbruno.com.br/2012/02/24/novo-tema-wordpress-em-html5-blog-da-locaweb/>

Acabei deixando passar em branco, a funcionalidade dos comentários Reply, aparecerem logo abaixo do comentário pai deles. Em cadeia mesmo.
  
Ficando assim:
  
<!--more-->


  
[<img src="http://wbruno.com.br/wp-content/uploads/2012/03/Screen-shot-2012-03-08-at-7.58.31-PM-300x266.png" alt="" title="Screen shot 2012-03-08 at 7.58.31 PM" width="300" height="266" class="aligncenter size-medium wp-image-1864" srcset="http://wbruno.com.br/wp-content/uploads/2012/03/Screen-shot-2012-03-08-at-7.58.31-PM-300x266.png 300w, http://wbruno.com.br/wp-content/uploads/2012/03/Screen-shot-2012-03-08-at-7.58.31-PM.png 902w" sizes="(max-width: 300px) 100vw, 300px" />](http://wbruno.com.br/wp-content/uploads/2012/03/Screen-shot-2012-03-08-at-7.58.31-PM.png)

O que é bem ruim para organização, e confunde bastante a discussão. Eu não queria ter que instalar plugins de comentário apenas para isso.
  
Estudei um pouquinho o tema TwentyTeen, com a dica do @ThiagoCruz, e então:
  
[<img src="http://wbruno.com.br/wp-content/uploads/2012/03/Screen-shot-2012-03-08-at-7.58.54-PM-300x261.png" alt="" title="Screen shot 2012-03-08 at 7.58.54 PM" width="300" height="261" class="aligncenter size-medium wp-image-1865" srcset="http://wbruno.com.br/wp-content/uploads/2012/03/Screen-shot-2012-03-08-at-7.58.54-PM-300x261.png 300w, http://wbruno.com.br/wp-content/uploads/2012/03/Screen-shot-2012-03-08-at-7.58.54-PM.png 919w" sizes="(max-width: 300px) 100vw, 300px" />](http://wbruno.com.br/wp-content/uploads/2012/03/Screen-shot-2012-03-08-at-7.58.54-PM.png)

É isso. Os códigos que adicionei estão abaixo:

**function.php**

<pre name="code" class="php">if ( ! function_exists( 'parent_comment' ) ) :
/**
 * Template for comments and pingbacks.
 *
 * To override this walker in a child theme without modifying the comments template
 * simply create your own twentyten_comment(), and that function will be used instead.
 *
 * Used as a callback by wp_list_comments() for displaying the comments.
 *
 * @since Twenty Ten 1.0
 */
function parent_comment( $comment, $args, $depth ) {
	$GLOBALS['comment'] = $comment;
	switch ( $comment->comment_type ) :
		case '' :
	?>
		&lt;li &lt;?php comment_class(); ?> id="comment-&lt;?php comment_ID() ?>"> &lt;?php echo get_avatar( $comment, 32 ); ?>
		
			&lt;cite>&lt;?php comment_text() ?>&lt;/cite>
			
			&lt;?php comment_type(_x('Coment&aacute;rio', 'noun'), __('Trackback'), __('Pingback')); ?>
			&lt;?php _e('por'); ?>
			&lt;?php comment_author_link() ?>
			&#8212;
			
			&lt;time datetime="&lt;?php echo $comment->comment_date; ?>">
				&lt;?php comment_date() ?>
				@ &lt;a href="#comment-&lt;?php comment_ID() ?>">
				&lt;?php comment_time() ?>
				&lt;/a>
			&lt;/time>
			&lt;?php edit_comment_link(__("Editar"), ' | '); ?>
			
			&lt;?php if ( $comment->comment_approved == '0' ) : ?>
				&lt;em class="comment-awaiting-moderation">&lt;?php _e( 'Your comment is awaiting moderation.' ); ?>&lt;/em>
			&lt;?php endif; ?>
		
		
			&lt;?php comment_reply_link( array_merge( $args, array( 'depth' => $depth, 'max_depth' => $args['max_depth'] ) ) ); ?>			
		&lt;/li>

	&lt;?php
			break;
		case 'pingback'  :
		case 'trackback' :
	?>
	&lt;li class="post pingback">
		&lt;p>&lt;?php _e( 'Pingback:' ); ?> &lt;?php comment_author_link(); ?>&lt;?php edit_comment_link( __( '(Edit)' ), ' ' ); ?>&lt;/p>
	&lt;?php
			break;
	endswitch;
}
endif;
?></pre>

**comments.php**

<pre name="code" class="php">&lt;?php if ( have_comments() ) : ?>
	&lt;ol id="commentlist">
		&lt;?php wp_list_comments( array( 'callback' => 'parent_comment' ) ); ?>
	&lt;/ol>
&lt;?php else : // If there are no comments yet ?>
	&lt;p>&lt;?php _e('Nenhum coment&aacute;rio ainda.'); ?>&lt;/p>
&lt;?php endif; ?>
</pre>

**style.css**

<pre name="code" class="css">#commentlist .children { margin-left: 25px; }</pre>

Ahh, e sem se esquecer do novo input hidden, para o comentário reply saber quem é o pai dele:

**comments.php** ou comment_form() [caso vc não tenha personalizado o form]

<pre name="code" class="html">&lt;input type="hidden" name="comment_parent" id="comment_parent" value="&lt;?php if( isset( $_GET['replytocom'] ) ) echo $_GET['replytocom']; ?>" /></pre>

=)