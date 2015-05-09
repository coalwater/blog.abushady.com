---
title: Using the null object pattern
layout: post
ident: using-null-objects-pattern
published: true
tags:
  - Ruby
  - Clean Code
  - AntiPattern
  - Object Oriented Programming
---
This is a common problem, you have an object, and that object does some logic,
and then you find that at some point this logic needs a special condition,
because the object is null, or somet variable inside it that holds another
variable is null, here's a small example
<!-- more -->
{% gist 8c0730a0911b3f871d9c order_class.rb %}
Then in the view we do something like this

{% gist 8c0730a0911b3f871d9c order_view.rb %}
But then we find that sometimes this book doesn't exist for some reason, so we
add this condition

{% gist 8c0730a0911b3f871d9c order_view_patched.rb %}
This works, but it's considered a bad smell and an antipattern, first of all
you added the logic of handling non existent books in the view, and if we have
multiple partials each will have this block, a smiple change would require
going through all these templates.

Instead we could use what's called a [null object ][wikipedia-null-object],
which is an object from a different class but has the same interface of the
original class, and would respond to the same method, and returns the case
specific response that we want.

For our case a simple way to impelemt this is by returning a `NullBook`
instance for `Order`s that don't have a book, when we try to read the book's
title, the `NullBook` will respond with `No books exist`, so the view will
handle it normally thinking that it's the actual book.

First we just create a `NullBook` class and place this logic inside it

{% gist 8c0730a0911b3f871d9c null_book.rb %}
Then in the `Order` class we will modify the getter a little bit

{% gist 8c0730a0911b3f871d9c order_with_nullbook.rb %}
This way if `@book` is null then we return an instance of `NullBook`, now we can
clean up the view back to this

{% gist 8c0730a0911b3f871d9c order_view.rb %}

[wikipedia-null-object]: https://en.wikipedia.org/wiki/Null_Object_pattern
