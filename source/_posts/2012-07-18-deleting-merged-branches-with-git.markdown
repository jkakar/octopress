---
layout: post
title: "Deleting merged branches with Git"
date: 2012-07-18 15:41
comments: true
categories: git scripts
---

My friend and colleague at Fluidinfo,
[Manuel Cerón](https://twitter.com/ceronman), gave me this script that
he wrote to remove merged branches from local and remote Git
repositories.  Removing branches after merging is one of those fairly
painless housekeeping tasks that doesn't create a great deal of
friction, which makes it easy to avoid automating, but it wastes a lot
of time as days and weeks go by.

``` bash
#!/bin/bash

set -x

# Update the master branch.
git checkout master
git pull upstream master

# Synchronize the remote repository.
git push origin master

# Find all merged branches and delete them in the local and remote
# repositories.
for branch in `git branch --merged | grep -v '*' | tr -d ' '`
do
    git branch -d $branch
    git push origin :$branch
done
```

It's available in this [gist](https://gist.github.com/3139743).  You
can wire it up as a `cleanbranches` command by adding the following to
your `~/.gitconfig` file:

```
[alias]
    cleanbranches = !/home/jkakar/bin/gitcleanbranches.sh
```

Now you can run `git cleanbranches` in any repository and local and
remote branches that have already been merged will be deleted
automatically.  It's a simple thing, but one of those simple things
that makes a nice difference in the daily workflow.
