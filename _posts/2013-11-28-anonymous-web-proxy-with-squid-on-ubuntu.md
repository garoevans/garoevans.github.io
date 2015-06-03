---
layout: post
title: Anonymous Web Proxy With Squid on Ubuntu
---

##The Problem

I was doing a little bit of testing on a web app earlier today and I wanted to be able to switch my IP easily. I’d never used a web proxy before, I’ve never had the need to.

First I found some [free proxy listings](http://www.freeproxylists.net/) on sites like [HIDE MY ASS](http://hidemyass.com/proxy-list/), these give you an IP address and port to connect to from your browser. This did the trick but I felt a little vulnerable going through some random proxy. This wasn’t the solution for me.

Then I found [Squid](http://www.squid-cache.org/). This solved all my problems in one beautiful move, all I needed was a box somewhere to do my dirty work (luckily I have a very reasonable droplet at [Digital Ocean](https://www.digitalocean.com/?refcode=c5bcfe2a51e7)) and the following setup.

##The Solution

###1. Install the Squid server on Ubuntu 12.04

{% highlight bash %}
sudo apt-get install squid
{% endhighlight %}

###2. Make a backup of the config file before you mess it up :)

{% highlight bash %}
sudo cp /etc/squid3/squid.conf /etc/squid3/squid.conf.original
sudo chmod a-w /etc/squid3/squid.conf.original
{% endhighlight %}

*For the next few steps I’m going to use some pretend IPs for the purpose of this post. Let’s say my home IP address (where I’m using my browser) is “1.2.3.4” and my server’s IP address is “11.22.33.44”.*

###3. Add some Squid config lines to allow access from your home machine

{% highlight bash %}
acl home src 1.2.3.4/24
http_access allow home
{% endhighlight %}

*The first line needs to come first :) and is best kept with the other default `acl` config lines. The second line needs to come before the default deny from all `http_access deny all`.*

###4. Restart Squid

{% highlight bash %}
sudo /etc/init.d/squid3 restart
{% endhighlight %}

*You can now test your proxy. Open your browser and set your proxy configuration. There are lots of tutorials around for this sort of thing, if using Chrome you can follow a [handy tutorial](http://www.googlechrometutorial.com/google-chrome-advanced-settings/Google-chrome-proxy-settings.html); set the IP to “11.22.33.44” (your proxy server) and the port to “3128” (default port for Squid) unless you change the port in the squid config. If you visit a site like [http://www.whatismyip.com/](http://www.whatismyip.com/) you should see the IP as “11.22.33.44”. You may also notice that it has recognised you using a proxy and says that this is via “1.2.3.4”.*

*__Top Tip:__ do you use a firewall? Make sure port 3128 is open for incoming traffic.*

###5. Make it Anonymous, add the following to the bottom of your config

{% highlight bash %}
acl ip1 myip 11.22.33.44
tcp_outgoing_address 11.22.33.44 ip1

forwarded_for off
request_header_access Allow allow all
request_header_access Authorization allow all
request_header_access WWW-Authenticate allow all
request_header_access Proxy-Authorization allow all
request_header_access Proxy-Authenticate allow all
request_header_access Cache-Control allow all
request_header_access Content-Encoding allow all
request_header_access Content-Length allow all
request_header_access Content-Type allow all
request_header_access Date allow all
request_header_access Expires allow all
request_header_access Host allow all
request_header_access If-Modified-Since allow all
request_header_access Last-Modified allow all
request_header_access Location allow all
request_header_access Pragma allow all
request_header_access Accept allow all
request_header_access Accept-Charset allow all
request_header_access Accept-Encoding allow all
request_header_access Accept-Language allow all
request_header_access Content-Language allow all
request_header_access Mime-Version allow all
request_header_access Retry-After allow all
request_header_access Title allow all
request_header_access Connection allow all
request_header_access Proxy-Connection allow all
request_header_access User-Agent allow all
request_header_access Cookie allow all
request_header_access All deny all
{% endhighlight %}

*The first two lines tell squid that any connection coming in on “11.22.33.44” should have an outgoing IP of “11.22.33.44”. You can set your outgoing to whatever you like.*

###6. Restart Squid (see point 4)

And we’re done. You’re proxy server is now set up safely and anonymously. You can add incoming IPs so that you can access it from other locations and configure it to your hearts content.

##And More

To make life even easier, using Chrome I added the [Proxy Switchy!](https://chrome.google.com/webstore/detail/proxy-switchy/caehdcpeofiiigpdhbabniblemipncjj) extension. This allows me to save as many proxy profiles as I like to easily switch between.
