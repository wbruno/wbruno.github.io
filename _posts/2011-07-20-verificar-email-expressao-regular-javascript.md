---
id: 1212
title: 'Verificar email com expressão regular &#8211; javascript'
date: 2011-07-20T15:29:18+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1212
permalink: /javascript-puro/verificar-email-expressao-regular-javascript/
dsq_thread_id:
  - "2102114097"
categories:
  - Javascript
---
=)

<pre name="code" class="javascript">function is_email(email){
	er = /^[a-zA-Z0-9][a-zA-Z0-9\._-]+@([a-zA-Z0-9\._-]+\.)[a-zA-Z-0-9]{2,3}/; 
	if( !er.exec(email) )
	{
		jQuery('#retorno_capta').html('Email inválido!');
		return false;
	}
}
</pre>