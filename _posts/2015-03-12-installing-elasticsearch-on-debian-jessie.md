---
title: Installing and running elasticsearch on debian jessie
layout: post
ident: installing-elasticsearch-on-debian-jessie
date: 2015-03-12
published: true
tags:
  - ElasticSearch
  - Debian
---
Recently I needed to install elasticsearch on my debian jessie laptop, first I
found it in the repos so I installed it normally, it installed a bunch of stuff
with it that I didn't actually need but I thought like fine w/e it needs, I need
it to work to finish my task, and at the end it didn't really work anyways.
<!-- more -->
The thing is that the daemon wasn't starting for some reason and it only starts
if i run it manually from it installation folder, and it wasn't even a daemon
{% gist 97a083ddc28d4c9aef7d run_from_bin.sh %}
Which wasn't very convinient, I decided instead to install it from the website,
you can download the [deb file from this link][elasticsearch-download], then
installing it
{% gist 97a083ddc28d4c9aef7d download_and_install.sh %}
The good thing is that at least this time it didn't download all the packages I
didn't need, I had to use the `init.d` folder
{% gist 97a083ddc28d4c9aef7d run_from_initd.sh %}
But when I tried to use the service format, i get an error
{% gist 97a083ddc28d4c9aef7d service_error.sh %}
After looking around I found how to register the service, you just run these
two lines
{% gist 97a083ddc28d4c9aef7d registering_service.sh %}
Then now it works fine

[elasticsearch-download]: https://www.elastic.co/downloads/elasticsearch
