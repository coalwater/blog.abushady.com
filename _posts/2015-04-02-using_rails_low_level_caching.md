---
title: Using rails low level caching
layout: post
ident: using-rails-low-level-caching
published: true
tags:
  - Rails
  - Caching
---
Some times we find our selves having a time expensive method or in some cases
using an API that costs money per request, or a slow one, I had that issue once
when using twitter API, I was fetching the last tweet for a website, and
sometimes that request took a second or two to return, which was annoying.
<!-- more -->
Rails proivde nice caching methods where you can cache any thing you want, and
you can set expiry time for this data, so you don't need to handle when the data
is stale, it's explained in details [in this guide
here][rails-low-level-caching-url], but I'll write a few examples here.

For this we have three methods, `write`, `read`, and `fetch`, first let's start
with `write`

##Write  
`write` takes two arguments, a cache key ( the key we're going to use to
retrieve the data ) and a cache value ( the data that's going to be stored ),
here's a simple example
{% gist e382b9d3fdda2e90c5ab basic_write.rb %}
Now this data is cached and can be retrieved when needed, there's also extra
options that can be passed such as expiry period
{% gist e382b9d3fdda2e90c5ab write_with_expire.rb %}
When the cache expires it will return nil when accessed.

The caching key could also be an object, not necessarily a string, for example
the key could be an object, or an array, or a hash, for example
{% gist e382b9d3fdda2e90c5ab write_with_compund_key.rb %}
You get the idea.

##Read
`read` only takes the cache key to retrieve the data, if the data doesn't exist,
`nil` will be returned instead
{% gist e382b9d3fdda2e90c5ab basic_read.rb %}
Also like `write`, you can use the non scalar key type to retrieve the data you
saved in the same way
{% gist e382b9d3fdda2e90c5ab read_with_compund_key.rb %}

##Fetch
`fetch` is a little special, because it does both `read` and `write`, when the
cache exists it returns it, but if it isn't it evaluates the block it's given
then writes the result to the cache and returns the value at the same time, if
the block isn't expensive ( in terms of time ) you could do with only fetch.
{% gist e382b9d3fdda2e90c5ab fetch_with_block.rb %}
If `some_key` is present and not stale, it's returned instantly from the cache,
if it is, the block is evaluated ( `some_calculations` ) and the return value
from the block is saved in the `some_key`

Of course as you can see all options mentioned before are also applicable on the
`fetch` method

[rails-low-level-caching-url]: http://guides.rubyonrails.org/caching_with_rails.html#low-level-caching
