---
title: Justifying Common Lisp in 2017
categories: [lisp]
visible: false
layout: post
---

  Why, in this modern age where we have tools like Node.js, Docker, Atom.io, and the like, would anyone use a language as old as Common Lisp, or as complicated as Haskell?

  The short answers are that the modern world has yet to catch up with the Common Lisp of 30 years ago in many important areas, and, if you can navigate the complexity of modern Javascript with callbacks, promises, and all of the other features that, at least from this angle, seem tacked on, then you'll almost certainly find Haskell far easier to reason about.

  The long answer is probably where I will show my age.  I sometimes feel like I'm turning into a UCB-Beard wielding, sandals-shorts-and-tshirt wearing, technology snob.  I make great efforts to be objective about technology, especially about technologies and languages that I don't like.  It does me no good to dismiss anything out of hand simply because it strikes me as limited, 'what amateurs do', or *especially* things that strike me as out of fashion.  I dislike that quality in other engineers and I give myself no end of hell when I catch myself doing it, which happens more times that I'd like to admit.

  That said, there simply some things that we could not do without a language like Common Lisp and it gives us an agility that we're not interested in compromising on.

We have several instances that are only restarted when there are significant OS updates.  When they do have to be updated, we have built a framework with which we can transfer all state over the wire to a new instance, and traditional load balancers make it easy to divert traffic to another instance without any service interruption.  The thing about this that's unusual, among others, is that it's not some dirty hack we've come up with, but rather a perfectly legitimate use of the language.

We update live, production images with new features and bug fixes, often many times a day.  Again, not a hack, but a directly supported feature of the language.  Since Common Lisp is image based [1], we can save the execution environment of a product at any time and use that as either a production image, or as a checkpoint of the development.  It's not that far off of what Docker gives you, only this isn't the operating system, just the code and data that was running at the time the image was dumped.

The two examples above are nice, for sure, but the real selling point is that we can connect over an SSH tunnel to a live instance and inspect the system, and debug errors on the fly.  When an error happens, we are given a debugger, over the wire, and are able to inspect the environment where the bug happened, and optionally continue the execution with an update.  Now, I apologize here, but I think this bears repeating in a different way: When there is a bug, and an editor is connected to the instance over the wire, errors cause the editor to enter the debugger **without unwinding the call stack** and the programmer can fix the error and continue.  Then they can open that function in the source code, fix the root cause of the error, re-evaluate that specific form, and thereby update the live system.  Compared to the traditional edit-compile-run-observe-rinse-repeat cycle of debugging, this is a huge leap forward.  Our internal support code, affectionately known as *mesh* supports migrating both data and code changes to instances in a cluster, so we just need to run a form on one machine to synchronize a function or list of functions and their dependencies.  The only other programming language that I've had significant experience with that comes close to this level of availability is Erlang.  Erlang is certainly worth a close look for systems that absolutely have to be working 24/7.

I realize that this is a bold statement, and I also realize that there are a lot of people out there trying to convince the world that their solution or language choice is the best, but in my opinion, this is a radical leap forward from the status quo.  All from a programming language that was standardized 30+ years ago.




1. As far as I know, all Common Lisps are image based in some way, but there's several I've never used.  CLISP comes to mind.  Again, I'm pretty sure they are, but I don't know for sure, so I'm reluctant to say 'all' here.
