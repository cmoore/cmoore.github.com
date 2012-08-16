---
layout: post
title: The not so obvious stuff.
tagline: and the stuff that will mysteriously explode.
---

<legend> {{ page.title }} </legend>

So you want to start writing some haskell?  Here's some of the stuff that's not completely obvious when you are setting up a dev environment.

* Cabal, cabal-install, etc.

`Cabal` is a library that ships with `GHC`.  `cabal-install` is a program that is separate, and can sometimes be a real pain in the ass to install.  For instance, right now (as I type this out) if you download `GHC` 7.4.1 and install it, and get `cabal-install` from hackage, it won't build via the handy-dandy `boostrap.sh` script.  It will say it requires a different version of `Cabal`.  That can be a real wtf moment.  Usually, this will get you out of the bind:

 1. Go [here](http://wiki.darcs.net/Binaries) and grab a binary of `darcs`.
 2. Now use that binary to check out the cabal repo from [here](http://www.haskell.org/cabal/code.html).

Inside that directory, there is another directory called `cabal-install`.  Try running the `bootstrap.sh` script in there.  If it works, you're done!  If not, back up to the top level `cabal` directory and build that.  You can build a package without cabal-install like so:

 There should be a file called `Setup.hs` in that directory.
  
 1. `ghc --make Setup` (no, not `Setup.hs`, just `Setup`)
 2. `./Setup configure --user`
 4. `./Setup build`
 5. `./Setup install`

Now, you have a pretty good chance of `cabal-install` from the directory before installing.

* Also, when dealing with `Cabal`, `cabal-install` and the like, you can almost be guaranteed that the `--global` flag to `cabal-install` will trash your setup.  It is apparently only for use in carefully crafted, multiuser boxes (real multiuser machines, not your typical nerd's linux box.  I'm thinking university machine, etc.) where specific package versions are needed for homework.  Unless you know beyond a shadow of a doubt that you really need to use it, don't.


I'll try to keep on the lookout for other things.
