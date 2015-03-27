---
title: Using rails low level caching
layout: post
ident: using-rails-low-level-caching
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

    Rails.cache.write 'my_caching_key', some_data
Now this data is cached and can be retrieved when needed, there's also extra
options that can be passed such as expiry period

    Rails.cache.write 'my_caching_key', some_data, expires_in: 1.hour
When the cache expires it will return nil when accessed.

The caching key could also be an object, not necessarily a string, for example
the key could be an object, or an array, or a hash, for example

    Rails.cache.write(['some_data', @user], some_data)
    Rails.cache.write({key: 'important_data', owner: @user}, some_data)
You get the idea.

##Read
`read` only takes the cache key to retrieve the data, if the data doesn't exist,
`nil` will be returned instead

    Rails.cache.read 'my_caching_key'
Also like `write`, you can use the non scalar key type to retrieve the data you
saved in the same way

    Rails.cache.read({key: 'important_data', owner: @user})

##Fetch

[rails-low-level-caching-url]: http://guides.rubyonrails.org/caching_with_rails.html#low-level-caching
