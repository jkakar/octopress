---
layout: post
title: "Storm 0.17 is out in the world!"
date: 2010-08-06 12:25
comments: true
categories: storm
---

Yesterday I released version 0.17 of
[Storm](http://storm.canonical.com/).  This release fixes a
checkpointing bug that could cause coherency issues in certain
situations involving triggers.  It introduces a handful of new
features and optimizations including the ability to get a
[`Select`](http://people.canonical.com/~therve/storm/storm.expr.Select.html)
expression from a
[`ResultSet`](http://people.canonical.com/~jkakar/storm/storm.store.ResultSet.html),
which is useful when building a query with a subselect.  It also
includes safety checks to ensure that a
[`Store`](http://people.canonical.com/~therve/storm/storm.store.Store.html)
is only used when database access is expected and only from the thread
in which it was created.  The
[release notes](http://launchpad.net/storm/+milestone/0.17) have
detailed information about the changes along with links to the MD5 sum
and GPG signature for the
[tarball](http://edge.launchpad.net/storm/trunk/0.17/+download/storm-0.17.tar.bz2).
I've also built official packages for Ubuntu users, available in the
[Storm PPA](https://launchpad.net/~storm/+archive/ppa).

We're always interested in hearing about your experiences with Storm.
If you have comments or questions please feel free to hop into
`#storm` on Freenode and talk to us, or post a message on the
[mailing list](https://lists.canonical.com/mailman/listinfo/storm).
