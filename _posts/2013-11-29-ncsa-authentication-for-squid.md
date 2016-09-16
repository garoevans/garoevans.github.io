---
layout: post
title: NCSA Authentication For Squid
category: code
redirect_from:
- /2013/11/29/ncsa-authentication-for-squid/
---

## Introduction

In my last post [Anonymous Web Proxy With Squid On Ubuntu](/2013/11/28/anonymous-web-proxy-with-squid-on-ubuntu/) I wrote a step by step for setting up a web proxy using Squid on Ubuntu 12.04. This was restricted based on the static IP that you access the proxy from. But what if you don’t have a static IP, then what…
<!--more-->

Squid comes with support for a few [different methods for authentication](http://wiki.squid-cache.org/action/show/Features/Authentication), some require a few extra installs and some are ready to go straight off the bat. I decided to use the [`ncsa_auth`](http://www.squid-cache.org/Versions/v3/3.1/manuals/ncsa_auth.html) method, which uses a username and password file on the server to authenticate incoming connections.

The steps below originated from the post [Howto: Squid proxy authentication using ncsa_auth helper](http://www.cyberciti.biz/tips/linux-unix-squid-proxy-server-authentication.html) with a couple of tiny tweaks for version 3 of Squid.

### Step 1 – Create a Username and Password

{% highlight bash %}
sudo htpasswd -c /etc/squid3/passwd username
{% endhighlight %}

*Replace “username” with the username you would like to use. You will then be prompted to enter a password and to confirm it.*

*You also need to make sure that the file has read permissions.*

{% highlight bash %}
sudo chmod o+r /etc/squid3/passwd
{% endhighlight %}

### Step 2 – Edit your config

{% highlight bash %}
sudo nano /etc/squid3/squid.conf
{% endhighlight %}

*Add the following lines to setup your ncsa auth.*

{% highlight bash %}
auth_param basic program /usr/lib/squid3/ncsa_auth /etc/squid3/passwd
auth_param basic children 5
auth_param basic realm Squid proxy-caching web server
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive off
{% endhighlight %}

*The following two lines set your authentication type, and allow http access based on that authentication.*

{% highlight bash %}
acl ncsa_users proxy_auth REQUIRED
http_access allow ncsa_users
{% endhighlight %}

### Step 3 – Restart Squid

{% highlight bash %}
sudo /etc/init.d/squid3 restart
{% endhighlight %}

## Conclusion

Now, you can add your new username and password to authenticate your access to your new web proxy. If you’re unable to set the authenticating username and password in the headers you will be prompted by your browser to enter them when you first connect. The line `auth_param basic credentialsttl 2 hours` tells Squid to keep us authenticated for up to 2 hours. Tweak this as necessary!
