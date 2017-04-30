---
id: 1728
title: 'Setar combo pelo .text() do option &#8211; jQuery'
date: 2012-01-19T10:58:27+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1728
permalink: /jquery/setar-combo-pelo-text-option-jquery/
dsq_thread_id:
  - "2102340110"
categories:
  - jQuery
---
Apenas repositório mesmo:
  
<!--more-->

<pre name="code" class="html">&lt;script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js">&lt;/script>
&lt;script type="text/javascript">
jQuery(document).ready(function(){
	var combo = jQuery("select[name='combo']");
	
	
	jQuery("input[name='selecionar']").click(function(){
		var button = jQuery( this );
		combo.find("option").each(function(){
			if( jQuery( this ).text()==button.val() )
			{
				combo.val( jQuery( this ).val() );		
			}
		});	
	});	

});
&lt;/script>

&lt;select name="combo">
	&lt;option value="2">Selecione&lt;/option>
	&lt;option value="1">Item 1&lt;/option>
	&lt;option value="2">Item 2&lt;/option>
	&lt;option value="3">Item 3&lt;/option>
&lt;/select>

&lt;input type="button" name="selecionar" value="Item 1" />
&lt;input type="button" name="selecionar" value="Item 2" />
&lt;input type="button" name="selecionar" value="Item 3" />
</pre>