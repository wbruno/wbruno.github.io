---
id: 1618
title: 'Codificar em entities apenas &#8220;letras&#8221; &#8211; php'
date: 2011-11-24T14:49:38+00:00
author: William Bruno
layout: post
guid: http://wbruno.com.br/blog/?p=1618
permalink: /php/codificar-em-entities-apenas-letras-php/
categories:
  - PHP
---
Precisei disso.. e ai a função htmlentities() do php, não era capaz de me atender.
  
Pelo menos eu, não vi se é possível ignorar os outros símbolos com essa função, para que ela faça o entitie apenas das letras.
  
<!--more-->


  
Foi então que vi este comentário no manual:
  
<http://www.php.net/manual/en/function.htmlentities.php#102363>

Tudo oque eu precisava. Ai restou o trabalho, de escrever uma rotina para fazer o replace das letras com acentos, para o entitie de cada uma delas. Separei em 2 arrays, e pronto:

<pre name="code" class="php">&lt;?php
	$str = "'homeMessageTitle' => __('Atendimento online, fácil e rápido!', 'saas'),";

	$vogais = array(
		'À', 'à', 'Á', 'á', 'Â', 'â', 'Ã', 'ã', 'Ä', 'ä', 'Å', 'å', 'Æ', 'æ', 
		'Ç', 'ç', 
		'Ð', 'ð', 'È', 'è', 'É', 'é', 'Ê', 'ê', 'Ë', 'ë', 
		'Ì', 'ì', 'Í', 'í', 'Î', 'î', 'Ï', 'ï', 
		'Ñ', 'ñ', 
		'Ò', 'ò', 'Ó', 'ó', 'Ô', 'ô', 'Õ', 'õ', 'Ö', 'ö', 'Ø', 'ø', 'Œ', 'œ', 
		'ß', 
		'Þ', 'þ', 
		'Ù', 'ù', 'Ú', 'ú', 'Û', 'û', 'Ü', 'ü', 
		'Ý', 'ý', 'Ÿ', 'ÿ'
	);
	$ent = array(
	 	'&Agrave;', '&agrave;', '&Aacute;', '&aacute;', '&Acirc;', '&acirc;', '&Atilde;', '&atilde;', '&Auml;', '&auml;', '&Aring;', '&aring;', '&AElig;', '&aelig;', 
		'&Ccedil;', '&ccedil;', 
		'&ETH;', '&eth;', '&Egrave;', '&egrave;', '&Eacute;', '&eacute;', '&Ecirc;', '&ecirc;', '&Euml;', '&euml;', 
		'&Igrave;', '&igrave;', '&Iacute;', '&iacute;', '&Icirc;', '&icirc;', '&Iuml;', '&iuml;', 
		'&Ntilde;', '&ntilde;', 
		'&Ograve;', '&ograve;', '&Oacute;', '&oacute;', '&Ocirc;', '&ocirc;', '&Otilde;', '&otilde;', '&Ouml;', '&ouml;', '&Oslash;', '&oslash;', '&OElig;', '&oelig;', 
		'&szlig;', 
		'&THORN;', '&thorn;', 
		'&Ugrave;', '&ugrave;', '&Uacute;', '&uacute;', '&Ucirc;', '&ucirc;', '&Uuml;', '&uuml;', 
		'&Yacute;', '&yacute;', '&Yuml;', '&yuml;'
	);


	echo str_replace( $vogais, $ent, $str );
</pre>

=)