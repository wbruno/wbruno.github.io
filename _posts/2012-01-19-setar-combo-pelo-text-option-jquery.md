---
id: 1728
title: 'Setar combo pelo .text() do option - jQuery'
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

``` html
<script type="text/javascript"> type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>
<script type="text/javascript">
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
</script>

<select name="combo">
  <option value="2">Selecione</option>
  <option value="1">Item 1</option>
  <option value="2">Item 2</option>
  <option value="3">Item 3</option>
</select>

<input type="button" name="selecionar" value="Item 1" />
<input type="button" name="selecionar" value="Item 2" />
<input type="button" name="selecionar" value="Item 3" />
```
