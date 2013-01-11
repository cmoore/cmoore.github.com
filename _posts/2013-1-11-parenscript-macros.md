---
title: Parenscript and Macros
categories: lisp
visible: true
layout: post
---

{% highlight cl %}

(defpsmacro with-page-loaded (&rest block)
  `((@ ($ document) ready) (lambda ()
                               ,@block)))

(defpsmacro set-element-html (element value)
  `((@ ($ ,element) html) ,name))

{% endhighlight %}

Later...

{% highlight cl %}
; Assuming cl-who and parenscript are loaded...

CL-USER> (htm
           (:script
             (str (ps (with-page-loaded
                        (set-element-html "#title" "We Like Titles!"))))))
<script>$(document).ready(function () {
    return $('#title').html('We Like Titles!');
});</script>
"</script>"
{% endhighlight %}


  There is much undiscovered country here.

