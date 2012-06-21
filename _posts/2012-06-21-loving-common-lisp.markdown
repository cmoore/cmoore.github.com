---
layout: post
title: An elementary macro in Common Lisp
---

{{ page.title }}
====

I decided today that I wanted to partially apply functions in Common Lisp like you can do in Haskell.  It's Lisp, so that was easy.

In the package `cl-mongo`, `get-element` takes a name and a document and returns the value or nil for that element of the doc.  I was messing around in the repl viewing different documents and every time I did so I had to do something like this:

{% highlight lisp %}
(mapcar #'(lambda (x) (get-element "uid" x)) (car (db.find "stuff" :all)))
{% endhighlight %}

Which, as an also-Haskell programmer, that is just far too verbose.

The solution was, as always, a macro.

{% highlight common lisp %}
(defmacro @-map (toapply list)
  `(mapcar #'(lambda (x)
              (,@toapply x)) ,base))
{% endhighlight %}

