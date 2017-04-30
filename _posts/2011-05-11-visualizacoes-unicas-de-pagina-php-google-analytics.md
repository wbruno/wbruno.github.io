---
id: 924
title: 'Visualizações únicas e de página, com php &#8211; google analytics'
date: 2011-05-11T06:55:54+00:00
author: William Bruno
layout: post
guid: http://www.wbruno.com.br/blog/?p=924
permalink: /php/visualizacoes-unicas-de-pagina-php-google-analytics/
dsq_thread_id:
  - "2101259956"
categories:
  - PHP
tags:
  - analytics
---
=)

Foi um script que desenvolvi um tempo atrás.
  
Eu precisava resgatar a quantidade de **visitas únicas**, e de **visualizações**, das páginas de um site.
  
<!--more-->

Existe uma <a href="http://code.google.com/p/gapi-google-analytics-php-interface/" target="_blank">class oficial, a GAPI</a>.
  
Se você dedicar um tempinho para ler a <a href="http://code.google.com/intl/pt-BR/apis/analytics/docs/gdata/gdataReferenceDimensionsMetrics.html" target="_blank">API do Google Analytics</a>, dá para customizar bem os relatórios..

<pre name="code" class="php">&lt;?php
	include 'gapi.class.php';

	define('ga_profile_id', '123456789');
	$ga = new gapi( 'seu_email@provedor.com', 'sua_senha' );


	$ga->requestReportData(ga_profile_id, 'pagePath', array('uniquePageviews','pageviews'),'-uniquePageviews', null, null, null, null, 300);

	echo '&lt;table>&lt;tr>&lt;th>URL&lt;/th>&lt;th>Visitas Únicas&lt;/th>&lt;th>Visualizações&lt;/th>&lt;/tr>&lt;tbody>';
	foreach($ga->getResults() as $result)
	{
			echo '&lt;tr>&lt;td>&lt;u>',$result->getPagePath(), '&lt;/u>&lt;/td>&lt;td>',$result->getUniquePageviews(),
									'&lt;/td>&lt;td> ',$result->getPageviews(), '&lt;/td>';
	}
	echo '&lt;/tbody>&lt;/table>';
</pre>

A saída é algo do tipo:

<pre>URL						Visitas Únicas	Visualizações
&lt;u>/blog/&lt;/u>						635			973
&lt;u>/blog/2011/04/29/afinal-e-orientacao-objetos/&lt;/u>	303			325
&lt;u>/blog/2011/04/15/carousel-jquery-usando-cycle/&lt;/u>	239			373
</pre>

No caso, abrindo o teu google analytics, você notará, que a resposta se refere aos dados dos últimos 30 dias.
  
O **ga\_profile\_id**, vc recupera assim que logar no GA.

Note a URL, depois de ter entrado no teu perfil:
  
<u>https://www.google.com/analytics/reporting/?reset=1&id=**123456789**pdr=20110409-20110509</u>

Só informar na constante ali do php, o valor da chave ID dessa query string.
  
Bom divertimento.