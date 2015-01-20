---
title: Select, Reject, Collect, Detect, Inject
layout: post
ident: select-reject-collect-detect-inject
---
I've recently learned those convenient functions that apply on any array (enumerable), all these functions take a block and according to this block's output the return is decided.

##<a name='select'></a>[Select](#select)
Selects items from the array if the block returns true
**example** : we want to select the even numbers only
<script src="https://gist.github.com/coalwater/4082e2609d3c03370e82.js?file=select-example.rb"></script>

<!-- more -->
##<a name='reject'></a>[Reject](#reject)
Same as select but rejects the items that return true from the block
**example**: we will use the same example to reject even numbers
<script src="https://gist.github.com/coalwater/4082e2609d3c03370e82.js?file=reject-example.rb"></script>

##<a name='collect'></a>[Collect](#collect)
This is quite similar to select but instead it collects the results of the blocks instead of the array them selves.
**example**: we want an array that contains the squared numbers of the current array
<script src="https://gist.github.com/coalwater/4082e2609d3c03370e82.js?file=collect-example.rb"></script>

##<a name='detect'></a>[Detect](#detect)
Detect finds the first ( and only the first ) item that satisfies the conditon inside the block, and returns the item's value
<script src="https://gist.github.com/coalwater/4082e2609d3c03370e82.js?file=detect-example.rb"></script>

##<a name='inject'></a>[Inject](#inject)
Inject is one of my favorite functions, it iterates on all items and accumulates the block's results into an accumelator, then returns that accumelator's value, it also can take an initial value for the accumulator, which could be either an integer or any object, like an array for example
<script src="https://gist.github.com/coalwater/4082e2609d3c03370e82.js?file=inject-example.rb"></script>

<span style='font-size: 12px'>I would like to thank Matthew for his [blog post](http://matthewcarriere.com/2008/06/23/using-select-reject-collect-inject-and-detect/) as that was where I initially learned about the usage those functions</span>
