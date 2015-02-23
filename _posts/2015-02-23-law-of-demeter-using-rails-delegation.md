---
title: Law of demeter and rails delegation
layout: post
published: true
ident: law-of-demeter-using-rails-delegation
---
## Defining law of demeter
The [law of demeter][law-of-demeter-wikipedia] simply states that objects should
only talk to them selves or objects directly associated to them selves, because
otherwise this is considered a dependency and would reduce maintainability and
cause tight coupling between objects, <!-- more -->this rule can often be
ignored if the objects are of the same type, but more about that later.

Here's some violations of the law of demeter:
{% gist 3584ed4bf2a15a88c3ee law_of_demeter_violation.rb %}

And here's some methods that don't violate the law
{% gist 3584ed4bf2a15a88c3ee law_of_demeter_fix.rb %}

To simplify the rule we might state it as

> Don't use more than a single dot in methods calls

## Violating the law of demeter in rails
First lets take a look at a few places where we could find violations in rails,
first and easiest place to find this violation is in rails, let's take this
example snippet from a view, assuming this is an order object in a cart system,
such code could also be found in a view, model or controller, it's very common
{% gist 3584ed4bf2a15a88c3ee violating_view.rb %}

Such code works because rails internatlly queries for the associated object and
then sends the corresponding method call to the new queried object, this could
go wrong very easily, assuming for some reason we moved the invoice number to a
different object, or changed its name, we will need to find every single usage
of this method and replace it in every view, which is a very bad maintainability
issue.

## Adding wrappers
To fix someone might think ok we'll wrap these methods in the model so then
they'll be centralized and can be maintained easier and in a single place,
here's the modifined order model
{% gist 3584ed4bf2a15a88c3ee order_with_wrapper.rb %}

And here's the updated view
{% gist 3584ed4bf2a15a88c3ee delegated_view.rb %}

This sure does a lot better than how we started, if any thing changes in the
models, the public API of the object stays the same, and the internal method
gets changed, but this intrudces a new kind of problem, the size of the file,
if we keep going like this, we'll end up with one huge model, consisting mostly
of tiny wrapper functions to handle these small things, luckily rails gave us a
way to improve this one step further.

## #delegate
In rails models you can specify certain messages that are delegated to other
objects using the [delegate keyword][rails-guides-delegate], you could say it's
like specifying a handler to handle this message, here's how we delegate the
methods form our past examples:
{% gist 3584ed4bf2a15a88c3ee initial_delegate.rb %}

Just by defining those two lines, our order instance now can respond to those
messages, and delegate them to the `:item` object and `:invoice` object.

But for them to work we need to implement those messages
{% gist 3584ed4bf2a15a88c3ee item_with_wrapper.rb %}

Well we separated the concern, but we still have an implementation issue, we
just moved the methods from one place to another, to solve this we can check
the `:prefix` option.

The prefix option allows us to specify a prefix that will be used during the
method call, but not passed during the delgation, if prefix is set to `true`
then the prefix will be set as the name of the object we're delegating to,  
so now by setting `prefix: :true` we can say `item_name` but the item will only
recieve `name`, this should solve our problems
{% gist 3584ed4bf2a15a88c3ee delegate_with_prefix.rb %}

If the associated object is nil, rails will raise an error because there's no
object to recieve the message and handle it, for this we can specify an extra
parameter called `allow_nil` this message will tell rails to return nil if the
associated object is nil, instead of raising an error, this way we don't need
to handle special cases when the object is not initialized or not existing.

So here's the final model version
{% gist 3584ed4bf2a15a88c3ee delegate_with_allow_nil.rb %}

and here's the final view
{% gist 3584ed4bf2a15a88c3ee delegated_view.rb %}

[law-of-demeter-wikipedia]: https://en.wikipedia.org/wiki/Law_of_Demeter
[rails-guides-delegate]: http://guides.rubyonrails.org/active_support_core_extensions.html#method-delegation
