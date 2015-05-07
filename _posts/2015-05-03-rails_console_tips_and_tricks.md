---
title: Some rails console tips and tricks
layout: post
ident: rails-console-tips-and-tricks
published: true
tags:
  - Rails
  - Console
  - Tips and Tricks
---
Any rails developer probably uses rails console every day, when testing methods,
when debugging, or doing some database modifications, knowing some convenient
tips will make you save some time, and on the long run you'll become more
productive with these simple tricks.

<!-- more -->

## Modifying objects safely
Sometimes I need to test a method that modifys some database objects, and at the
same time i don't want to destruct the data, rails console provides you with a
neat sandbox, you can delete and modify data as you like, and when you are done
all the data is rolled back, this is done using a database transaction.
{% gist d1255c8b264c9b1974d8 sandbox.rb %}
When you run console a second time, you'll find that all your users are back to
normal.

## The value of the last expression
Sometimes you write a query and then realize you want that result in a variable,
irb keeps the value of the last run expression in a variable called `_`, here's
an example.
{% gist d1255c8b264c9b1974d8 underscore_1.rb %}
Also you can do operations on it directly
{% gist d1255c8b264c9b1974d8 underscore_2.rb %}

## Clearing your console
When your console becoems too crowded and you want to start clean, a simple
ctrl+L will clear your console.

## Reloading models
When you change something in your models and you want to load it in your already
running console session you could just run `reload!` and the model changes will
be loaded.  
*Note that this won't work on libraries and classes in the `lib` directory.*

## Testing view helpers in the console
Sometimes I try to test a view helper, you can easily call those methods using
`helper` prefix
{% gist d1255c8b264c9b1974d8 view_helpers.rb %}
