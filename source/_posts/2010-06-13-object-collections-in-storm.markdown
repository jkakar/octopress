---
layout: post
title: "Object collections in Storm"
date: 2010-06-13 12:25
comments: false
categories: storm
---

In [Storm](https://storm.canonical.com/), the
[`Store.find`](http://people.canonical.com/~therve/storm/storm.store.Store.html#find)
method runs a query and returns matching objects.  Finding all
accounts in the database, the equivalent of `SELECT * FROM account`,
is simple:

``` python
result = store.find(Account)
```

Clauses to limit the scope of the query can be passed to find.
Finding all accounts owned by Vince Offer, the equivalent of `SELECT *
FROM account WHERE owner = ‘Vince Offer’`, is also simple:

``` python
result = store.find(Account, Account.owner == "Vince Offer")
```

Another way to achieve the same thing is to take the result from the
first find operation and refine it:

``` python
result1 = store.find(Account)
result2 = result1.find(Account.owner == "Vince Offer")
```

Storm doesn’t run a query until you do something with the result, so
the impact on the database is exactly the same as in the previous
example.  This is the simplest form of what
[Jonathan](http://code.mumak.net/) and I have been calling the
collection pattern.  The basic idea is that you start with a
collection of all objects, and then refine it, until you have the
collection you want.  This pattern is possible using pure Storm, as
shown above, but we’ve found it useful to implement objects that hide
this logic and provide a more user friendly API.  For example, an
`AccountCollection` would provide filtering logic as named methods:

``` python
class AccountCollection(object):

    def owned_by(self, salesman):
        """
        Get a new collection with accounts owned by
        salesman.
        """

    def has_unpaid_invoices(self):
        """
        Get a new collection with accounts that have
        unpaid invoices.
        """

    def find(self):
        """Get a result set of matching accounts."""
```

Each filtering method, such as `owned_by and has_unpaid_invoices`
returns a new `AccountCollection` instance.  This isn’t strictly
necessary but creating a new instance is both easier to understand and
implement.  Finding all accounts owned by `Vince Offer` that have unpaid
invoices is quite easy:

``` python
collection1 = AccountCollection()
collection2 = collection1.owned_by("Vince Offer")
collection3 = collection2.has_unpaid_invoices()
result = collection3.find()
```

This pattern provides several benefits:

- It names filtering options which makes them easy to understand and
  use.

- Query building logic is in one place which eliminates duplication.

- All the criteria used to build a query are available when the query
  is generated, which makes it possible to generate optimized queries.
  All users of the collection benefit from optimizations.

- It creates a clean separation between finding data and using it.
  This helps keep application logic more focused, because it isn’t
  intermingled with the particulars of generating queries.

We’ve used this pattern to good effect in both
[Landscape](https://landscape.canonical.com/) and
[Launchpad](https://launchpad.net/).  In a future post I’ll talk about
some different strategies we’ve used to implement the pattern.
