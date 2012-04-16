---
layout: post
title: "Using SQL functions with Storm"
date: 2010-04-08 12:25
comments: true
categories: storm
---

People ask me questions about [Storm](https://storm.canonical.com/)
several times a week, and I'm happy to help where I can, but it would
be better if the information our users need was easier to find.  Our
documentation story is weak and, as a result, Storm is harder to
discover than it ought to be.  If you do run into problems or have
questions, please hop into `#storm` on Freenode and we'll do our best
to help you.  I want to improve the documentation situation, but
finding the time to do so hasn't happened yet.  The next best thing is
to post some helpful hints here.

First, some advice: if you don't know what SQL query you want to run,
using Storm will probably be hard.  When I get asked a question about
writing a query using Storm I almost always respond with, "What does
the query you want to run look like?" The querying part of Storm is
essentially just an expression compiler that takes a list of
expressions and converts them to SQL.  Once you know what end result
you want, working backwards to figure out the Storm parlance is
relatively straight forward.

Today I was asked about using
[`COALESCE`](http://en.wikipedia.org/wiki/Null_%28SQL%29#COALESCE).
The person asking the question found the
[`storm.expr.Coalesce`](http://people.canonical.com/~therve/storm/storm.expr.Coalesce.html)
expression but it wasn't obvious how to use it.  He knew he wanted to
run a query like:

``` sql
SELECT * FROM table WHERE COALESCE(col1, col2) = 'foo'
```

With that knowledge, figuring out how to use Storm was quite easy:

``` sql
store.find(Table, Coalesce(Table.col1, Table.col2) == "foo")
```

Furthermore, `Coalesce` is just a helper expression to aid usability
and readability.  If we didn't have a built-in `Coalesce` expression
the query could have been written using the generic
[`storm.expr.Func`](http://people.canonical.com/~therve/storm/storm.expr.Func.html)
expression:

``` sql
store.find(Table, Func("COALESCE", Table.col1, Table.col2) == "foo")
```

If you want to use a SQL function in a Storm query, and there is no
built-in expression for it, you can use `Func` to call it.
