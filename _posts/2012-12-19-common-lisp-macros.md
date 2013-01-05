---
title: Understanding Common Lisp Macros
categories: lisp
visible: false
layout: post
---

When setting out to learn Common Lisp you will eventually come across comments like this:

> Common Lisp's macros are awesome. They're messy and you can shoot yourself in the foot with them and they need to be used sparingly… but ...

I would argue that macros are one of the more beautiful features of CL, and I think partial understanding is the root of some of this idea that somehow you should use macros as little as possible.  Note that this is aside from issues of style which, it is generally accepted, say that if a function can be written as a `defun`, then it should be.

#### Thinking in macros

What you're telling lisp is, in essence, 'evaluate the form preceded by the backquote first, .... FUCK... this chunk first, and then insert the result into the code, and parse again'.

{% highlight cl %}

(defun number-to-word (number)
  (cond ((string-equal number "12") "twelve")
        (t "what")))

(defun test-it ()
  `(format nil "~a" ,(number-to-word "12")))

(defmacro test-it-m ()
  `(format nil "~a" ,(number-to-word "12")))

...

CL-USER> (test-it)
(FORMAT NIL "~a" "twelve")
CL-USER> (test-it-m)

"twelve"
CL-USER>
{% endhighlight %}
