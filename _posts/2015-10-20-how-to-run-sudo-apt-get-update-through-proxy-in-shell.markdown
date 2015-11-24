---
layout: post
title: How to run sudo apt-get update through proxy in Shell
date: 2015-10-20 12:49:21.000000000 -02:00
type: post
published: true
status: publish
categories: proxy shell unix linux
comments: true
---
I was struggling with this because I was configuring my http_proxy, https_proxy and ftp_proxy using `export` but when I was doing `sudo apt-get udpate`, nothing happened. Did some research on StackOverflow and found the solution. So I'm keeping the solution here for future reference. This problem happens because in some releases `sudo` is configured in such a way that all environment variables all cleared when running the command.  
My proxy didn't have authentication so I did:

{% highlight ruby %}
export http_proxy="http://proxy.servername:port/"
export https_proxy="http://proxy.servername:port/"
export ftp_proxy="http://proxy.servername:port/"
{% endhighlight %}

After that I did:

{% highlight ruby %}
visudo
{% endhighlight %}

There is a line that states:

{% highlight ruby %}
Defaults env_reset
{% endhighlight %}

After that line just add:

{% highlight ruby %}
Defaults env_keep = "http_proxy https_proxy ftp_proxy"
{% endhighlight %}

Voilá. Things will start working now.
