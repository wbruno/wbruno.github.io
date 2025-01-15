---
id: 1171
title: 'Traduzir URLs - inglês/português/espanhol'
date: 2011-07-12T00:23:17+00:00
author: wbruno
layout: post
guid: http://wbruno.com.br/blog/?p=1171
permalink: /php/traduzir-urls-inglesportuguesespanhol/
categories:
  - PHP
---
``` php
class Language
{
  private $lang = Array();
  private $matches;
  private $current;

  public function __construct( $page, $current )
  {
    $this->current = $current;

    $page = preg_replace( '/\.html(.*)/', '', $page );
    preg_match( '/([^\/]+)\/?([^\.]+)?/', $page, $this->matches ); //cloud-server/compare-and-decide-pricing.html?adas=dasd

    $this->lang['es'] = Array(
      'pricing' => 'cambio',
      'features' => 'funcionalidades',
      'faqs' => 'dudas'
    );

    $this->lang['en'] = Array(
      'pricing' => 'plans-and-pricing',
      'features' => 'features',
      'faqs' => 'faq'
    );

    $this->lang['pt'] = Array(
      'pricing' => 'precos',
      'features' => 'vantagens',
      'faqs' => 'duvidas-frequentes'
    );

  }

  public function translate( $to )
  {
    (int)$branches = count($this->matches);


    $done = "";
    if ($branches > 0) {

      for ($i=1; $i<$branches; $i++) {
        $key = array_search( $this->matches[ $i ], $this->lang[ $this->current ] );

        $done .=  !empty( $this->lang[ $to ][ $key ] ) ? '/'.$this->lang[ $to ][ $key ] : '';
      }
    }
    return $done=="" ? "" : $done.".html";
  }
}
$pagina_atual = str_replace( 'es/', '', $_SERVER['REQUEST_URI'] );

$language = new Language( $pagina_atual, 'es' );
$pt = $language->translate( 'pt' );
$en = $language->translate( 'en' );
```
