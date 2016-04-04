---
id: 44
title: Rename tables with Mysql
date: 2015-03-15T14:41:45+00:00
author: douglasjam
layout: post
guid: http://douglasjam.com.br/?p=44
permalink: http://en.douglasjam.com.br/2015/03/15/rename-tables-with-mysql-2/
categories:
  - Databases
  - Mysql
---
It can happen anytime you need to do a batch operation in your database, where is necessaty to rename all tables adding a prefix or suffix or even change their names, whatever what is the reason, there is a more productive method to rename them from one to one when the number of tables is large. The script above read all tables from the database and then mount a new script creating the query to rename the tables.

<pre class="lang:mysql decode:true">SELECT concat('RENAME TABLE ', table_name, ' TO ', concat('ds_', table_name), ';')
FROM information_schema.tables
where table_schema like 'mydatabase'</pre>

After execute this query the output will looks like as above, in this case I concatenated the prefix ds_ to the tables name. Now you just have to execute all the script above and all tables are renamed.

<pre class="lang:mysql decode:true ">RENAME TABLE contasprogramadas TO ds_contasprogramadas;
RENAME TABLE contratoguinchos TO ds_contratoguinchos;
RENAME TABLE empresas TO ds_empresas;
RENAME TABLE filiais TO ds_filiais;
</pre>