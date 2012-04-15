---
layout: post
title: "Talking about Storm"
date: 2009-12-02 12:14
comments: false
categories: storm
---

Today I gave a talk about [Storm](http://storm.canonical.com/) to the
fine folks that make up the local
[Python users group](http://wiki.python.org/moin/VanPyZ). I think the
talk went alright.  It wasn’t awesome but I don’t think it was
terrible either.  It’s the third public talk I’ve given, pretty much
ever, and so I have a lot to learn about the process.  The group is
friendly and I felt comfortable standing up in front of everyone and
yammering on about Storm.

In retrospect, I should have come up with much better example code.  I
didn’t make enough time to prepare and, due to rushing at the end, the
topics I covered were rather basic.  I did an experiment and wrote a
psuedo-doctest to use as slides.  The doctest and a script to run it
are available at
[lp:~jkakar/+junk/storm-talk](https://code.launchpad.net/~jkakar/+junk/storm-talk).
I used a slightly hacked version of
[Michael Hudson-Doyle’s](https://launchpad.net/~mwhudson) very awesome
[console-presenter](http://launchpad.net/console-presenter), which is
available at
[lp:~jkakar/console-presenter/two-line-separator](https://code.launchpad.net/~jkakar/console-presenter/two-line-separator).

The format was great for getting me to focus on content, even though I
didn’t have enough time to do a great job preparing it, but the slides
were a bit lackluster being grey text on a black background.  Also, a
common problem with doctests is that you need to keep track of the
state of the program as you read the document.  I think this problem
made the format awkward for the audience.  It was a good experiment,
but in the future I’ll use traditional slides, and try to avoid a
situation that requires the audience to keep program state in their
head as the talk progresses.  Funny how these things seem so obvious
in hindsight.

[Doug Latornell](http://douglatornell.ca/) gave a nice talk about his
experiences using [PyYAML](http://pyyaml.org/),
[flickerapi](http://stuvel.eu/projects/flickrapi) and
[Tkinter](http://wiki.python.org/moin/TkInter) to build an application
that displays random photos on his living room TV, both from his
personal collection and from his favourite groups on Flickr.  I
enjoyed the talk and the discussion it spurred.

All in all it was a good experience and from which I’ve learnt some
lessons, which I can hopefully use to make the next talk better.
