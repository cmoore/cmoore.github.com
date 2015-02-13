---
layout: post
title: Fun with elisp v2
categories: [emacs]
visible: t
---

Proof that we're really only a couple of years from realizing our most glaring mistakes.

The old:
{% highlight emacs-lisp %}
(defun ext-package-ensure (pkg)
  (or (progn
        (ignore-errors (require pkg))
        (ext-package-get-version-for-name pkg))
      (ignore-errors
        (and (package-install pkg)
             (message (symbol-name pkg))))))
{% endhighlight %}

The new:
{% highlight emacs-lisp %}
(defun ext-ensure-package (pkg)
  (unless (package-installed-p pkg)
    (package-install pkg)))
{% endhighlight %}
