---
title: Using active record's &#35;merge to separate concerns
layout: post
published: true
ident: using-active-records-merge-to-separate-concerns
---
We've all written this kind of code at some point of our lives, a query that
requires a join, and adding a condition to the joined table to limit the
returned results, but then by doing that you're adding a dependency, and you are
coupling the two models together.
<!-- more -->
Let's explain this on an example to make it clear, assume we have a dvd renting
store, and we have a system to manage the users, and dvds rentals, here's how
the models could look like ( in a very basic form )
{% gist 5a6bb89670424b63c6fd basic_models.rb %}
This is a basic simple relation, let's assume the dvds table has a simple flag
that says which dvds were returned and which were not.  
To find users that have un returned dvds, we could create a scope like this
{% gist 5a6bb89670424b63c6fd user_scope.rb %}
This scope has a problem, the thing is that the `User` class knows the name of
the field (`returned`), and the value it wants it to be (`false`), if for any
reason we decided to split the rentals into a separate table, or change the
field's name or value we need to modify this method too, which resides in the
`User` class, it should not have that dependency.

To fix this we could split this condition into a scope in the dvds table
{% gist 5a6bb89670424b63c6fd dvd_scope.rb %}
Now the Dvd model only knows what unreturned means, to use that in the users
method we will update the scope to use &#35;merge
{% gist 5a6bb89670424b63c6fd user_scope_with_merge.rb %}
It will generate the same SQL query, but without sharing the knowledge of the
field or the value with the `User` model



