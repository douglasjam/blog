---
id: 53
title: Restaurar backup mysql por arquivos
date: 2016-01-11T08:50:09+00:00
author: douglasjam
layout: post
guid: http://blog.djar.com.br/?p=53
permalink: http://douglasjam.com.br/2016/01/11/restaurar-backup-mysql-por-arquivos/
dsq_thread_id:
  - 4715171727
categories:
  - Banco de Dados
  - Linux
  - Mysql
---
Caso algum dia você não possa utilizar o mysqldump para fazer o backup corretamente e isolado do seu banco de dados mysql, seja por algum crash, alguma atualização ou modificação mal feita no servidor, você pode em ultimo caso recorrer ao backup manual dos arquivos, podendo assim você logo apos restaurar os arquivo em uma nova configuração de mysql.

Vou detalhar abaixo o passo a passo o qual segui para recuperar um banco apos este crash, no meu caso, apos um update do mysql para um versão superior, não conseguia mais ligar meu banco de dados mysql, e neste caso achei mais fácil retornar a versão anterior.<!--more-->Passo a passo:

1- Faça backup dos bancos de dados:

<pre class="lang:sh decode:true">cp -rf /var/lib/mysql/ ~/backup_mysql</pre>

2 &#8211; Reconfigure seu novo servidor

3 &#8211; Pare o servidor

<pre class="lang:sh decode:true ">service mysql stop</pre>

4 &#8211; Copie de volta os bancos de dados que deseja, normalmente estes sao separados por pastas

<pre class="lang:sh decode:true">cp -rf ~/mysql_backup/meu_db /var/lib/mysql/</pre>

5 &#8211; Caso voce possua algum banco de dados InnoDB, voce tambem tera que copiar a pasta ibdata1.

<pre class="lang:sh decode:true ">cp -rf ~/mysql_backup/ibdata1 /var/lib/mysql/</pre>

6 &#8211; Restaure as permissoes dos arquivos

<pre class="lang:sh decode:true ">chown mysql:mysql /var/lib/mysql/* -R</pre>

7 &#8211; Reinicie o servidor, e provavelmente estará tudo funcionando

<pre class="lang:default decode:true ">service mysql start</pre>

&nbsp;