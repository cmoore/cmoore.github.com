---
layout: post
title: The not so obvious stuff.
tagline: and the stuff that will mysteriously explode.
description: Some gotchas when setting up a new Haskell and Cabal development environment.
category: haskell
keywords: [cabal, haskell, ghc, cabal install]
---

So you want to start writing some haskell?  Here's some of the stuff that's not completely obvious when you are setting up a dev environment.

* Cabal, cabal-install, etc.

`Cabal` is a library that ships with `GHC`.  `cabal-install` is a program that is separate, and can sometimes be a real pain in the ass to install.  For instance, right now (as I type this out) if you download `GHC` 7.4.1 and install it, and get `cabal-install` from hackage, it won't build via the handy-dandy `boostrap.sh` script.  It will say it requires a different version of `Cabal`.  That can be a real wtf moment.  Usually, this will get you out of the bind:

Check out, or download cabal from [the official Github repo](http://github.com/haskell/cabal).  There's a link to download a zip file of that repo if you don't have Git installed.

Inside that directory, there is another directory called `cabal-install`.  Try running the `bootstrap.sh` script in there.  If it works, you're done!  If not, back up to the top level `cabal` directory and build that like so:

 1. `ghc --make Setup` (no, not `Setup.hs` which should be a file in that directory, just `Setup`)
 2. `./Setup configure --user`
 4. `./Setup build`
 5. `./Setup install`

Now, you have a pretty good chance of `cabal-install` from the directory before installing.

I'll try to keep on the lookout for other things.
