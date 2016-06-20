---
layout: post
title: Auto Deploy with Jenkins into Docker
category: Docker
figure: resources/img/jenkinsdocker.jpg
tags: [linux, docker, vps, linode, port-forwarding, cloud]
----------------------------------------------------------
I use a VPS from [Linode](https://www.linode.com/?r=f548ff90f3ebf67ce61e811294d8de70b45a3e1c) to host and manage my systems, before this change I was using 2 VPS where I installed all the servers in the main machine. But after sometime I got some problems like:
 
 - I needed two different versions of Mysql, but it is not easy to handle this situation 
 - It was too complicate to manage all configurations of many systems at the same machine, per example, if some system has a bug it can affect others, or if I had to test some configuration change exclusively I had the problem that it can affect and crash everything
  
This was a problem to me, to solve this in the first instance I decided to contract more one VPS but with this solution the cost was increasing, and my service does not require all capacity provided by Linode so it was a lost of money.
   
I was already using Docker containers as hobby locally, then I decided to try use it inside my VPS also. And right now I'm completely satisfied with the results, my main VPS machine is very clean, just a SSH Server and Nginx to rewrite domains access to docker ports, and each docker containers are isolated with only the required dependencies and without any conflict. And the best if one container crash it is just recreate it uniquely and it is fixed, easily and fast.
    
I'll write bellow the steps that I did in order to make this environment, you can do it locally, in your Linode, DigitalOcean or in any server that you have access.
    
- 1: Install docker in your machine

{% highlight bash %}
    curl -fsSL https://get.docker.com/ | sh
{% endhighlight %}

- 2: now you need to create your container, you can do it manually or use the available containers in the [docker hub](https://hub.docker.com), I'll show in another post how I create my own customized
docker containers.

{% highlight bash %}
    docker run container-name
{% endhighlight %}

- 3: Now docker will listen in the exposed ports automatically, per example, if you just have one docker containers that runs nginx in the ports 80, and you exposed 80:80, your server is configured 
automatically then, but if you have 2 or more nginx docker containers, it is not possible to expose both in the port 80, then you have to do something per example:

{% highlight text %}
# docker internal port -> exposed port
docker 1 nginx => 80:1000
docker 1 mysql => 3306:1001
docker 2 nginx => 80:1002
docker 3 psql  => 5432:1003
{% endhighlight %}

- 4: In order to map domain:port accessing the main server and redirect to the right containers you can use solver alternatives one of them for nginx http/s protocols is nginx.  

{% highlight bash %}
    apt-get install nginx
{% endhighlight %}

- 5: Now configure some enabled websites

{% highlight bash %}
vim /etc/nginx/sites-enabled/mydomain
{% endhighlight %}

- 5.1: add the configuration to listen in the port 80 for the domain that you want and redirect to docker port locally

{% highlight text %}
server {
     listen       80;
     server_name  mydomain.com www.mydomain.com
     location / {
         proxy_pass http://127.0.0.1:1002;
     }
 }
 
- 6: now restart nginx to reload the new configurations
 
{% highlight bash %}
  service nginx reload
{% endhighlight %}

After this steps you will be able to have multiple docker containers inside your VPS/local machine and redirect access from outside to it. This solution I find by myself, probably others also use it, but maybe I'm doing something wrong, would you like to share some ideas about this solution with me? feel free, I'll be happy.