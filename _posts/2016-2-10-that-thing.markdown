---
title: That thing I've always wanted.
categories: [haskell]
visible: true
layout: post
---

Lately I've been writing desktop applications.  This time around, we have several people testing the different versions to ensure that the program works correctly on lots of different types of machines.

I've always wanted a 'patcher'.  Something that simply duplicates a directory tree stored somewhere out there, and duplicates it on a local machine.  Most games these days, especiall mmorpg's have this sort of thing.  I could never find one that was easy to use and didn't come with some sort of weird licensing.  So, naturally, I wrote one.

[bob](http://github.com/cmoore/bob) is really super simple, no magic, and either generates a manifest from a directory in JSON form, or takes the url of a manifest and duplicates it.

