---
title: Parenscript and Macros 2
categories: lisp
visible: true
layout: post
---

So, we've decided to make a game.  Not just any game though - it's a game about a chicken with super space powers.  It's drawn with [jawsjs](http://jawsjs.com) with help from [underscore.js](http://underscorejs.org).

The Javascript is also generated on the fly in Common Lisp because I hate javascript with all of my little black heart.

{% highlight cl %}


; The one-stop shop for all of your _.js needs.
(defpsmacro _ (func (&rest body))
  `((@ _ ,func) ,@body))

(defpsmacro new-sprite (&key (x 0)
                             (y 0)
                             (image "grass-dirt.png")
                             (anchor "bottom_center")
                             (flipped false))
  `(new (jaws.-sprite (create image ,image
                              x ,x
                              y ,y
                              flipped ,flipped
                              anchor ,anchor))))

(defpsmacro add-powerup (&key (x 0) (frame 1))
  (let ((nom (gensym)))
    `(let ((,nom (new-sprite :x ,x :y (- world.height texture-size))))
       ((@ ,nom set-image) (aref pickups-sheet.frames ,frame))
       (powerups.push ,nom)
       (blocks.push ,nom))))

; Later, at the Hall of Justice...

; As a test, draw all of the sprites from the powerups sheet
; so we can confirm that they're being cut correctly.

(setf powerups (new -array))
(setf pickups-sheet (new (jaws.-sprite-sheet
                           (create image "/blocks/pickups.png"
                                   frame_size (array 34 42)
                                   ;scale_image 2
                                   orientation "right"))))

(defun show-powerups ()
  (dotimes (i 100)
    (add-powerup :x (+ 30 (* 32 i)) :frame i)))

{% endhighlight %}

{% highlight js %}
(function () {
    for (var i = 0; i < 100; i += 1) {
        var g1328 = new jaws.Sprite({ image : 'grass-dirt.png',
                                      x : 30 + 32 * i,
                                      y : world.height - textureSize,
                                      flipped : null,
                                      anchor : 'bottom_center'
                                    });
        g1328.setImage(pickupsSheet.frames[i]);
        powerups.push(g1328);
        blocks.push(g1328);
    };
})();
{% endhighlight %}

{% highlight cl %}
; show the collision rect of every powerup.
(_ map (powerups (lambda (x) ((@ (x.rect) draw)))))

{% endhighlight %}

{% highlight js %}

_.map(powerups, function (x) {
   return x.rect().draw();
});

{% endhighlight %}

{% highlight cl %}
; draw all of the powerups
(_ map (powerups (lambda (x) ((@ x) draw))))
{% endhighlight %}

{% highlight js %}
_.map(powerups, function (x) {
    return x(draw);
});
{% endhighlight %}

Granted, this is just basic substitution and could be done with any reasonably adept editor with an expansion plugin.  My next sub-project, however, is to insert the code to move ramdomly, and depending on the situation, attack the player, and I want that to be bound as closely to the individual enemy as possible.  Then, later, I'm going to have to define levels in json (probably json) and then build a level around the player on demand.  Oh, and then there's the fact that powerups need to actually do something to the player.  Plus, the lower level mechanics need to be easily tweakable until I get it just right.

You think web apps or machine learning is hard?  Try making a game that can actually suck a person in and tickle their sense of autonomy, mastery, and achievement.
