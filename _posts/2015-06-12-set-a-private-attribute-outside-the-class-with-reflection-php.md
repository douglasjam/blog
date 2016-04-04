---
id: 39
title: Set a private attribute outside the class with reflection (PHP)
date: 2015-06-12T16:31:00+00:00
author: douglasjam
layout: post
guid: http://douglasjam.com.br/?p=39
permalink: http://en.douglasjam.com.br/2015/06/12/set-a-private-attribute-outside-the-class-with-reflection-php/
categories:
  - PHP
---
The example bellow demonstrate how is possible to change the value of a private property even through private at runtime. It show us how we must stay alert when we provide an API&#8217;s and believe that it will be restrict to our scope.

<pre class="lang:php decode:true">&lt;?php

class User {

private $name = 'Douglas';

    public function getName(){
        return $this-&gt;name;
    }

}

$test = new User();

// verify that the value is Douglas
echo $test-&gt;getName() . PHP_EOL;

// Try to change the value directly, will throw a exception
//$test-&gt;name= 'Rodrigo';

// Make the change with reflection at runtime
$refObject = new ReflectionObject($test);
$refProperty = $refObject-&gt;getProperty('name');
$refProperty-&gt;setAccessible(true);
$refProperty-&gt;setValue($test, 'Rodrigo');

// Checks if the value was changed
echo $test-&gt;getName() . PHP_EOL;

// We confirm that it works in execution time and do not affect the Class
$test2 = new User();
echo $test2-&gt;getName() . PHP_EOL;</pre>

Saída:

<pre class="lang:default decode:true ">Douglas Rodrigo Douglas</pre>

&nbsp;