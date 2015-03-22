---
title: Routing all dev domains to localhost
layout: post
ident: dnsmasq-for-local-domains
published: true
---
When developing locally, you might find your self that you often need to route
some domain to localhost, for example `my-amazing-website.dev`  
<!-- more -->
Usually I used to do that by adding that domain to my `/etc/hosts` file, but I
found that keeping track of all those domains and adding more will crowd my
hosts file and will make it look ugly, not to mention that every time I wanna
try some domain I need to save it in my hosts file first.  
So I found a way to make this work dynamically, by installing a local
lightweight DNS server called `dnsmasq`, dnsmasq can use a regex to resolve
domains, so i found it easy to just apply a regex on all domains that end with
the `.dev` suffix.

First let's install dnsmasq, for ubuntu/debian you can simply use `apt-get`
{% gist 20dd4ca27dd34e0811ec install-dnsmasq %}
Then edit the conf file `/etc/dnsmasq.conf` and add this line
{% gist 20dd4ca27dd34e0811ec dnsmasq.conf %}
The remaining would be adding the localhost as a dns resolver, the easiest way
would be adding it manually in the network manager, but to keep it dynamic and
not affected by your own network manager settings you can use something like the
`resolvconf` package, first we install it
{% gist 20dd4ca27dd34e0811ec install-resolvconf %}
Then we edit the base file `/etc/resolvconf/resolv.conf.d/base` and add this
simple line
{% gist 20dd4ca27dd34e0811ec resolvconf.base %}

