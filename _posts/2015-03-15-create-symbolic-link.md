---
id: 34
title: Create symbolic link
date: 2015-03-15T14:21:37+00:00
author: douglasjam
layout: post
guid: http://douglasjam.com.br/?p=34
permalink: http://en.douglasjam.com.br/2015/03/15/create-symbolic-link/
categories:
  - Cloud
  - Linux
  - Windows
---
For those who use a storage service in the cloud, like Dropbox, Google Drive, Skydrive or another, they are always faced with questions like: we will only sync what is in the folder X. But sometimes we are faced with the situation that the directory you want to do a backup in the cloud might not be inside the folder they want, for example, if you want to back up a folder that is in your network, inside a folder of a specific program, or a savegame folder, ie one savegame at &#8220;C: / &#8230;&#8221;.

<!--more-->For this problem, exists a trick called symbolic link, existing both in windows and Linux, which apparently is a shortcut, but it&#8217;s a reference. If you try to put the link to the Cloud backup service it will not work because only the shortcut created will be synchronized and not its content, but using a reference will work as desired, it is as if the entire folder was inside because from the the moment you create the reference it will be like the file it is in the two places, if you chance something here it will be changed there.

Bellow are the commands for creating the symbolic link in windows and linux/debian.

&#8220;Note, in Windows, to create a reference to any folder on the network, choose to use a drive mapping before, is more reliable&#8221;

**Windows**

<pre class="lang:default decode:true">mklink /D "C:/Program Files/GameSavegame" "C:/Users/XPTO/Dropbox"</pre>

**Linux/Debian**

<pre class="lang:default decode:true ">junction ln -s /var/www/sitea/files /var/www/siteb/sitea_files</pre>