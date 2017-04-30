---
id: 2888
title: str_pad com javascript de forma recursiva
date: 2013-01-02T11:33:45+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/?p=2888
permalink: /javascript-puro/str_pad-com-javascript-de-forma-recursiva/
categories:
  - Javascript
---
<pre name="code" class="javascript">&lt;script type="text/javascript">
function pad( a ){
	var t, b = '';

	a = ''+a;

	if( a.length>=3 ) {
		return a;
	} else {
		t = pad( '0' + a ); 
	}

	return t;
}

document.writeln( pad( 1 ) + '&lt;br />' );
document.writeln( pad( 2 ) + '&lt;br />' );
document.writeln( pad( 10 ) + '&lt;br />' );
document.writeln( pad( 100 ) );
&lt;/script>
</pre>