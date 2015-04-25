---
title: How to stop ActiveRecord logs temporarily in heavy queries
layout: post
ident: stop-active-record-logs-temporarily
published: true
---
When I'm writing a heavy query rake task or just running something in the
console that does a lot of updates, and i want to output something it gets lost
in all the query logs output.
<!-- more -->
So I looked around for a convinent way to temporarily stop the output for just
this method, then I found that you could access the active record logger object
through `ActiveRecord::Base.logger` object, and it has many options that you
can play with, here's some options:

 - Completly silence logs in a block
  {% gist 40b061b2d0adcc8b3c9d silence.rb %}

 - Change logger level
  Logger has quite a few levels, and they are convieniently named with symbols
that can be used.

    Qouted from the debugging rails guide, in the [logger levels
section][log-levels]

    > The available log levels are: `:debug`, `:info`, `:warn` , `:error` ,
    > `:fatal`, and `:unknown`, corresponding to the log level numbers from 0 up
    > to 5 respectively.

  here's how to change the values
    {% gist 40b061b2d0adcc8b3c9d logger_levels.rb %}
    Unlike the `silence` method this doesn't restore the old value after a blog,
  so if you plan to restore the old value then you need to save it in a variable
  before changing it


[log-levels]: http://guides.rubyonrails.org/debugging_rails_applications.html#log-levels

