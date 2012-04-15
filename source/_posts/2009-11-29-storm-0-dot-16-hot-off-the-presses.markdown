---
layout: post
title: "Storm 0.16 hot off the presses!"
date: 2009-11-29 12:01
comments: false
categories: storm
---

Yesterday I released version 0.16 of
[Storm](http://storm.canonical.com/).  This release fixes some memory
leaks and introduces a handful of new features.  The number of changes
since 0.15 aren’t vast, but we’re trying to get into the habit of
releasing regularly, so hopefully this will become a trend. The
[release notes](http://launchpad.net/storm/+milestone/0.16) have
detailed information about the changes along with links to the MD5 sum
and GPG signature for the
[tarball](http://launchpad.net/storm/trunk/0.16/+download/storm-0.16.0.tar.bz2).
I’ve also built official packages for Ubuntu users, available in the
[Storm PPA](https://launchpad.net/~storm/+archive/ppa).

Unfortunately, the `karmic` and `lucid` packages don’t work properly
because they install files in `/usr/lib/python2.6/site-packages`,
which is no longer included in `sys.path` by default.  In the next
couple of days I’ll build new packages that correctly install files in
`/usr/lib/python2.6/dist-packages`, which should fix the problem.  For
now, adding the `site-packages` path to `sys.path` or including it in
`PYTHONPATH` will workaround the issue.

We’re always interested in hearing about your experiences with Storm.
If you have comments or questions please feel free to hop into
`#storm` on Freenode and chat us up, or post a message to the
[mailing list](https://lists.canonical.com/mailman/listinfo/storm).
