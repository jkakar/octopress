---
layout: post
title: "Beautiful emacs configuration"
date: 2010-10-03 12:25
comments: false
categories: emacs
---

**UPDATE** I've moved my emacs configuration to
[GitHub](https://github.com/jkakar/emacs-configuration).

Some time ago during a sprint, I noticed that
[Free Ekanayaka](https://launchpad.net/~free.ekanayaka), one of my
Landscape teammates, had excellent pyflakes/flymake integration that
dramatically improved the experience of editing Python files in emacs.
When I asked him about it he kindly offered to share his configuration
and I was excited to pick out the flymake settings he had.  When I
actually looked at what he'd sent me I was blown away.  He has the
most elegant emacs configuration I've ever seen.  He uses a simple
pattern composed of individual configuration files, each focused on a
particular set of customizations such as appearance, interaction,
programming, etc. that are all wired up to create the final result.
It's very clean and avoids the blob-of-crap problem that most emacs
configuration suffers from.

This evening I finally took his ideas and refactored them to match my
emacs setup.  The structure is the same, but the details are, in some
cases, quite different.  I'm managing the configuration with Bazaar
and have pushed it to Launchpad at
[lp:~jkakar/+junk/emacs](https://code.edge.launchpad.net/~jkakar/+junk/emacs).
Hopefully others will find this as inspiring as I have.
