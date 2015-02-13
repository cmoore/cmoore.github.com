---
title: How Hunchentoot?
categories: []
visible: true
layout: post
---

I've written a fair number of sites with hunchentoot, cl-who, and parenscript.  In each one, I write a couple of macros that look something like this:

{% highlight common-lisp %}

(defmacro with-authenticated-user (&rest body)
  (let ((uid (session-uid ...)))
    (when (not (is-this-session-valid? uid))
      (redirect "/"))
   ,@body))

{% endhighlight %}

Strangely I never seemed to remember that hunchentoot uses a seemingly sly method of capturing `*request*` that would be very handy, not to mention simple, to implement.

{% highlight common-lisp %}

(define-easy-handler (test-handler :uri "/test") ()
  ; (when (request-method *request*) ...
  ; (when (request-method) ...

{% endhighlight %}

Both of those calls to `request-method` are correct and do the right thing.  How?

The answer is probably obvious to you, but it took a fair bit of digging in the hunchentoot source to see it for myself.

First, at the top level, we have a simple `defvar`:

{% highlight common-lisp %}
(eval-when (:compile-toplevel :execute :load-toplevel)
  (defmacro defvar-unbound (name &optional (doc-string ""))
    `(progn
       (defvar ,name)
       (setf (documentation ',name 'variable) ,doc-string)
       ',name)))

(defvar-unbound *request*)
{% endhighlight %}

So, `*request*` is there, it just depends on it's scope whether it's bound or not.

My solution might be ham-handed, I'll have to experiment more, but this is already a lot more simple than what I had before.

{% highlight common-lisp %}

(defclass auth ()
  ((uid :initarg :uid
        :reader auth-uid)
   (admin :initarg :admin
          :reader auth-admin)
   (person :initarg :person
           :reader auth-person)))

(defvar *authentication*)

(defun auth-person* (&optional (authentication *authentication*))
  (auth-person authentication))

(defun auth-admin* (&optional (authentication *authentication*))
  (auth-admin authentication))

(defun auth-uid* (&optional (authentication *authentication*))
  (auth-uid authentication))

(defmacro with-authentication (&rest body)
  (let ((person (gensym))
        (uid (gensym)))
    `(let* ((,uid (hunchentoot-secure-cookie:get-secure-cookie "uid"))
            (,person (and ,uid (car (with-pg (select-dao 'person (:= 'uid ,uid)))))))
       (let ((*authentication* (make-instance 'auth
                                              :uid ,uid
                                              :person ,person
                                              :admin (and ,person
                                                          (person-admin ,person)))))
         ,@body))))


(define-easy-handler (test :uri "/test") ()
  (with-authentication
    (unless (auth-person*)
      (redirect "/")) ; not logged in!
    (...)))

{% endhighlight %}

