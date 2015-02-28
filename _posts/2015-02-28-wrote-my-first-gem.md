---
title: Wrote my first ruby gem
layout: post
published: true
ident: wrote-my-first-gem
---
I was helping a fellow developer on his rails project, and I found something
interesting in his code, it was a query on how to find if two date intervals are
intersecting or not.
<!-- more -->
we've already done something similar at work and it
required a big query to test, so I thought, maybe I should turn this into a gem
and then we could use it in this project, and in any future projects.

At the beginning I looked around for useful guides, found a lot of tutorials,
but most of them just end at a hello world gem and that's it, for me i wanted an
advance `acts_as` kind of gem, with dynamic methods and every thing, the most
useful guide for me was the [rails plugin guide][rails-plugin-guide] it self, there was
also the [ruby gems guide][ruby-gems-guide] which wasn't as useful but it helped
me know how to publish the gem it self.

After a few hours of trial and error, I was able to get my gem working, and
I wrote a few tests, pushed first gem version, with basic static named methods,
installed it and tested it on the code I already have from work, it worked, but
then I decided to upgrade it a bit, I wanted to use the dynamic methods,
methods that are named after the model it self.

At some point I got really stuck, trying to figure out how to define methods
that are named after the model that implements them, took me a while and I even
asked a [question on stackoverflow][so-question] which I don't usually do, and I
continued trying till I finally figured it out, I added my solution to the same
question.

For a beginner I really would recommend reading about ruby meta-programming,
there's a great book called ruby meta programming, I haven't finished reading it
yet but I've learned a lot about ruby it self and it's internal structure, a
very useful read.

You can check the gem's [rubygems][gem-rubygems] page and the
[github][gem-github] page, if you have any thoughts please leave a comment.


[rails-plugin-guide]: http://guides.rubyonrails.org/plugins.html
[ruby-gems-guide]: http://guides.rubygems.org/make-your-own-gem/
[so-question]: http://stackoverflow.com/questions/28772222/
[gem-rubygems]: https://rubygems.org/gems/acts_as_interval
[gem-github]: https://github.com/coalwater/acts_as_interval
