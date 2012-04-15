---
layout: post
title: "Introducing Commandant"
date: 2010-06-12 12:25
comments: false
categories: commandant
---

I’ve been meaning to write about
[Commandant](https://launchpad.net/commandant) for ages.  I started it
last year because I wanted to write command driven applications with a
user experience just like [Bazaar](http://bazaar.canonical.com/).
There are several things that I like about Bazaar’s user interface:

- You only have to know that the program is called `bzr` to start
  discovering it, because its default behaviour is to teach you how to
  use the builtin help system.
- Each command has a clear name that makes its purpose easy to discern.
- Each command has a succinct summary and a well written long
  description, along with clear information about the arguments and
  options the command accepts.
- Help topics provide general information about the program that isn’t
  command-specific.  The topics describe conceptual and technical
  aspects of the program that help the user better understand how to
  use it.
- The interface conventions are very simple.  It doesn’t take long to
  figure out how things work.

I wanted, as much as possible, to start writing application logic
without having to do much work to get a working user interface.  With
that in mind, the basic goal for Commandant is to provide a
Bazaar-like user interface with the least effort possible.  I started
by trying to extend Bazaar but I ran into tricky integration problems
that made it hard to make progress, so I switched gears and started
implementing the logic from scratch.  Reinventing the wheel got me
further than trying to integrate, but I quickly reached a point where
progress slowed down because I had to deal with tricky problems that
Bazaar had already solved.  In the meantime,
[Robert](http://rbtcollins.wordpress.com/) landed changes in Bazaar
that removed the integration hurdles that I’d run into.

With the integration problems out of the way, I stopped wasting time
reinventing the wheel, and Commandant is now a thin layer on top of
`bzrlib` itself.  Being able to take advantage of the work that has
been done in Bazaar has been a blessing.  There’s more that can be done
to improve Commandant, but it is very usable in its current state.  If
you’re interested in learning more, the
[README](http://bazaar.launchpad.net/~jkakar/commandant/trunk/annotate/head:/README)
file should get you started.
