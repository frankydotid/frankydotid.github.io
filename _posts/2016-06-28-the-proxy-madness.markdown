---
layout: post
title: "The proxy madness"
date: 2016-06-28
tags: technical
---
<br/>

I was trying to follow a tutorial on real-time event processing by [Hortonworks](http://hortonworks.com/hadoop-tutorial/realtime-event-processing-nifi-kafka-storm/), to the step where I needed to download and install several things on the sandbox. My network was behind a proxy, with authentication. It was a time-consuming experience to *just* download packages through the proxy, but probably, worth it. I need to set the proxy configuration separately for the three main programs used for downloading and setting up the tutorial: `git`, `wget`, and `maven`.

On Linux, you can set a proxy for your internet connection by `export`-ing or setting the environment variable `HTTP_PROXY` or `HTTPS_PROXY`, etc. The format is: `HTTP_PROXY=[DOMAIN]\[USERNAME]:[PASSWORDINPLAINTEXT]@[PROXY_URL]:[THE_PORT]`. The [DOMAIN] and [USERNAME] are only required when your proxy needs an authentication. In theory, any programs that required an internet connection should use this. In practice, this information might need to be repeated somewhere else.

<br/>

> It should be one time. It should be automatically detected. You wish!

<br/>

**Git with proxy** 

The command to use `git` with proxy should be quite simple. You need to update the global config:

```shell
git config --global http.proxy http://[DOMAIN]\[USERNAME]:[PASSWORDINPLAINTEXT]@[PROXY_URL]:[THE_PORT]
```

<br/>

**Wget with proxy** 

The `wget` program should be using your `HTTP_PROXY` variable. But, sometimes you may need to set it somewhere else. The config file that you are looking for is `wgetrc`. The global one is located at `/etc/wgetrc`. If you don't have access to edit the global config file, you can set it up for yourself in your home directory as `~/.wgetrc`. The basic information that you need to put are `use_proxy`, that tells `wget` to use a proxy, and `HTTP_PROXY` or other proxy variables that tells you the URL for the proxy and the credential (username and password) for authentication. 

```shell
use_proxy=yes
HTTP_PROXY=http://johndoe:password@127.0.0.1:8080
```

<br/>

**Maven with proxy** 

Maven has another different way of connecting through proxy. The configuration needs to be put in `settings.xml` file, which depends on your need can be set as global in `${maven.home}/conf/settings.xml` or for your eyes only in `${user.home}/.m2/settings.xml`. Find the `proxies` tag and fill up the information for the proxy there. The glonal `settings.xml` contains template on what attributes are available to set. You can find the reference on [Maven's site](https://maven.apache.org/guides/mini/guide-proxies.html)


<br/>
