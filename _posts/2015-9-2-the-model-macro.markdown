---
title: The Model Macro
categories: [common-lisp]
visible: true
layout: post
---

HWAT

This is my go-to macro for using databases in CL.  It is a modification of a macro that I got from another site, which I can't seem to find at the moment.  I came across it not long ago looking for something else, so I know it's still out there.  I'll update this post when I find it.

{% highlight common-lisp %}
(defmodel people ((name :col-type text
                        :accessor people-name
                        :initarg :name
                        :export t))
{% endhighlight %}

Evaluating that will


1. Create the database 'people'.
2. Create some functions
<table class="table table-bordered table-hover table-condensed">
<tr><td> `people-select` </td><td>Find a record based on a query.
{% highlight common-lisp %}
(people-select (:= 'name "Clint"))
{% endhighlight %}</td></tr>
<tr><td> `people-get` </td><td>Find a record with a uuid</td></tr>
<tr><td> `people-delete`</td><td>Remove a people record from the database.</td></tr>
<tr><td> `people-get-all` </td><td>Get all of the people records.</td></tr>
<tr><td> `people-update` </td><td>
{% highlight common-lisp %}
(defvar *t* (car (people-get-all)))           
(setf (people-name *t*) "Honk")               
(people-update *t*)
{% endhighlight %}</td></tr>
</table>

<script src="https://gist.github.com/cmoore/77aff7f58149d88f9cc7.js"></script>


Now the challenge is to put this in a package and make it importable in a sane way.
