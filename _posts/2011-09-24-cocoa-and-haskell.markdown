---
layout: post
title: It's like that one Reeses commercial everyone cites.
---

{{ page.title }}
====

This post is about getting the assurance of Haskell with the GUI love of Cocoa.  Though it is definitely Cocoa-specific in places, using the FFI there's no reason why it couldn't be abstracted out to support any GUI environment with a little work.

First things first
---

This is based on work by Tim Scheffler which you can see at [his github page](https://github.com/tscheff/HSOBJC_Test).  There's also an associated [blog post](http://tscheff.blogspot.com/2010/03/cocoa-application-almost-completely.html) with far more detail about the implementation.

Well, it works on my machine.
---

I tested this with Mac OS X 10.7, XCode 4.1, and GHC 7.0.4.  If run into problems, there are two places to look for tweakables.  The first is the *Build Settings* pane in XCode.  Specifically, the project only lists x86_64 in "Valid Architectures", and is targetted to 10.6 because the project I was using it for originally required support for it.  The second is under *Build Phases*, the last phase is a Run Script phase that runs a Python script to assemble the final binary, among other things.

The basics
---

* Check out a copy of [cocoa-app-shell](/cocoa-app-shell)

* Give it a spanky new name.  If you are using XCode 4 this is relatively easy if you slow-click on the top level of the project heirarchy.

![one](/1.png)

If you did that right, you'll see something like this, assuming you decided to name the project "Does It Work"

![one](/2.png)

Ok, how does it all actually work?
---

There are two ways to connect methods to Haskell code.  The first is connecting events to objects - buttons, text areas, and the like.

The second is calling functions directly.  This is a bit more involved.

Binding Events
---

*cocoa-app-shell* is about as simple as you can get.

![App Shell](/app-window.png)

If you enter some text in the textarea by *From Event*, it will convert it to upper case by simply calling `toUpper`.  This is bound programatically by haskell using the following code.

(For context, start at Controller.hs - line 78)

{% highlight haskell %}
msg <- (outlet "fh_hello_field") >>= objectValue
(outlet "fh_hello_field") >>= setObjectValue (T.toUpper msg)
{% endhighlight %}

Pretty simple.  As long as the outlet named "fh_hello_field" is mapped from Interface Builder to the main class it just works.

Poking around in the code, you'll also come across this line:

{% highlight haskell %}
"fh_hello_button" `connect` ff_say_hello
{% endhighlight %}

Which, as you might expect, connects a button's press event to a Haskell function.  Again, not terribly complicated.

Accessing functions directly
---

The second field in the example takes the string out of the textfield and converts it to uppercase, this time by calling a function straight up.  The objc side of this is in a handler for the button press.

{% highlight objectivec %}
- (IBAction)ff_say_hello:(id)sender {
  NSArray *res = [getMethod(controller,@"give_it") callWithArg:[ff_hello_field stringValue]];
  [ff_hello_field setStringValue:[res description]];
}
{% endhighlight %}

And now, here's the Haskell side of things.

{% highlight haskell %}
methods :: MethodTable
methods =  M.fromList $ map ( first T.pack )  methodTable
 where
   methodTable =
     [ ("isCorrectText", mkMethod (\_ -> is_correct))
     , ("give_it", mkMethod (\_ -> give_it'))
     ] 

   mkMethod :: (OBJC a) => (Controller -> a) -> (Controller -> IOOBJC StableId)
   mkMethod action = \contrl -> toStableId $ action contrl

   give_it' :: T.Text -> IO T.Text
   give_it' = return . T.toUpper
   
   is_correct :: T.Text -> IO T.Text
   is_correct a = do
     putStrLn $ "Got: " ++ (show a)
     return "OH SNAP, SON!"
{% endhighlight %}


Wrap up
---

I have delivered one application using this and have plans for a couple more.  I'm hoping to update the cocoa-app-shell project with a new version that has [Sparkle](http://sparkle.andymatuschak.org/) already configured.  We used it in the first deliverable and it really enjoyed using it.

