---
title: Select, Reject, Collect, Detect, Inject
layout: post
ident: select-reject-collect-detect-inject
published: true
tags:
  - Ruby
---
I've recently learned those convenient functions that apply on any array, or
just basically any enumerable, all these functions take a block and according
to this block's output the return is decided, those methods are select, reject,
collect, detect, inject.

<!-- more -->

##<a name='select'></a>[Select](#select)
Selects items from the array if the block returns true
**example** : we want to select the even numbers only
{% gist 4082e2609d3c03370e82 select-example.rb %}

##<a name='reject'></a>[Reject](#reject)
Same as select but rejects the items that return true from the block
**example**: we will use the same example to reject even numbers
{% gist 4082e2609d3c03370e82 reject-example.rb %}

##<a name='collect'></a>[Collect](#collect)
This is quite similar to select but instead it collects the results of the blocks instead of the array them selves.
**example**: we want an array that contains the squared numbers of the current array
{% gist 4082e2609d3c03370e82 collect-example.rb %}

##<a name='detect'></a>[Detect](#detect)
Detect finds the first ( and only the first ) item that satisfies the conditon inside the block, and returns the item's value
{% gist 4082e2609d3c03370e82 detect-example.rb %}

##<a name='inject'></a>[Inject](#inject)
Inject is one of my favorite functions, it iterates on all items and accumulates the block's results into an accumelator, then returns that accumelator's value, it also can take an initial value for the accumulator, which could be either an integer or any object, like an array for example
{% gist 4082e2609d3c03370e82 inject-example.rb %}

<span style='font-size: 12px'>I would like to thank Matthew for his [blog post](http://matthewcarriere.com/2008/06/23/using-select-reject-collect-inject-and-detect/) as that was where I initially learned about the usage those functions</span>
