---
layout: post
title: "Updating/Installing Packages for Linux Ubuntu behind (Imperfect) Firewall"
date: 2016-02-29
tags: technical
---
<br/>

I have a development server sitting in a data center with no internet access. It is running Ubuntu 14.04. The only means of accessing the server is through a SSH connection. It doesn't have any internal Ubuntu repository available in the network, since this is a new thing for a Windows-based company.

I want to try some stuffs on the server, and some packages are obsoletes. I also need to install new packages. I'm thinking of several options to do this.

First, **manually downloading** the packages and upload them to the servers. This is the most less hassling way for a simple package. The problem arise when they are dependency packages required, which means I have to download the dependencies one by one.

Second, **creating local repository** using Apache web server, or just point the repository link to a folder in my server. This sounds like a good idea to implement. But, it means I might need to download all the packages available, and make sure they are updated in my repository. 

Third, that came out of nowhere, is by **connecting the server to the internet with my laptop as proxy**. My laptop has a connection to the internet, and the development server is connected to my laptop. So, I think I can make it through. My lazy way to do it is as follow:

1. Download and install a portable xampp, which has a ready to use Apache web server, on your laptop. I use the portable one because I cannot install anything on my laptop (poor me).

2. Find your `httpd.conf` file:
   * Enable (uncomment) the `mod_proxy_http`
   * Add the forward proxy input, as mentioned in the [Apache httpd documentation](https://httpd.apache.org/docs/current/mod/mod_proxy.html#forwardreverse)
 
3. Run the Apache server

4. Do the usual `apt-get` with the proxy set, e.g., for installation: `sudo http_proxy='http://ip-address-of-your-laptop:port' apt-get install package-name`





