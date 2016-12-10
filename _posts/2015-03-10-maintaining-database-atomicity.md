---
title: Maintaining database atomicity using ActiveRecord transactions
layout: post
published: true
ident: maintining-database-atomicity
tags:
  - Rails
  - ActiveRecord
---
[Atomicity][atomicity-wiki] comes from the greek word 'a-tomos' which means
undevidable, atomic database transactions means that we want either all the
database operations to happen together, or none of them at all, which means that
we want them as a single undevidable operation, we would want that because not
doing any of the changes at all would be much less harmful than doing the a
part of the change.
<!-- more -->
One of the most common examples of this can be found in ecommerce websites, when
the customer buys an item and we reserve an item for the user, we want to make
sure that the whole order is done till the generation of the invoice, if for any
reason the flow is interrupted in the middle we want to make sure that we
release the reserved item and undo any orders that was placed.

Here's a sample (maybe unrealistic) implementation of a ecommerce website, but
let it pass for the sake of the example
{% gist 4fe828c7221c8c327219 place_order_without_transaction.rb %}
Suppose the item was reserved successfully, but there was an error in the order
creation, or maybe the order was created but there's an error in the invoice, we
would want to undo all these changes that we done, and maybe any changes that
happend from these changes, like any callbacks or logs that were inserted in the
database too, if you make use of those you'll be in a lot of trouble with this
unconsistent data.

In rails `ActiveRecord::Base` provides us with a very useful method
`#transaction` which starts a database transaction and doesn't commit the
changes to the database until every thing is done successfully, since all models
are subclasses of `ActiveRecord::Base` we can call `#transaction` on our models
too for simplicity.

To protect the `place_order` method we created, we could wrap the statements
inside it inside a transaction
{% gist 4fe828c7221c8c327219 place_order_with_transaction.rb %}
This way if something went wrong `ActiveRecord` will rollback the changes
automatically, and nothing will be persisted.

*Tips:*

  - You could fire the rollback your self if you raise inside the block, you
    could raise a rollback error
    {% gist 4fe828c7221c8c327219 manual_rollback.rb %}


  - Transactions could be nested, but needs a little tweaking to make it work as
    expected, you can read about the [details here][nested-transactions]

  - Transactions are just like any other block, it would return the last executed
    statement, could be used to return to an outer variable
      {% gist 4fe828c7221c8c327219 transaction_block_with_return.rb %}
    This way object will end up being the last array we created



[atomicity-wiki]: https://en.wikipedia.org/wiki/Atomicity_%28database_systems
[nested-transactions]: http://api.rubyonrails.org/classes/ActiveRecord/Transactions/ClassMethods.html
