---
title: Geiser for Gambit
slug: geiser-for-gambit-presentation-for-gambit-at-30
date_published: 2019-10-15T02:53:53.000Z
date_updated: 2021-01-11T01:34:26.000Z
tags: Emacs, Geiser, Gambit, Scheme
---

Geiser presentation for Gambit at 30 event at University of Montreal.
Ceci est un document [Microsoft Office](https://office.com) incorporé, avec [Office](https://office.com/webapps).
**** intro
As an undergraduate intern for Mr Feeley, the creator of Gambit-scheme, I worked on lot of projects. 
All these projects were concerning gambit-scheme and Emacs.
Emacs being in Elisp, it makes it a great environment for scheme. So I asked myself if there was some editors for scheme in Emacs as modes. That is when I discovered Geiser which is an awesome emacs mode for scheme! 
I decided to implement the Gambit feature in Geiser.
**** what is Geiser?
Geiser is an Emacs mode ; a coding environment to hack and have fun in scheme. [https://www.nongnu.org/geiser/](https://www.nongnu.org/geiser/)
**** Geiser inner functionning
When you start geiser, it asks you which scheme implementation you want to use.
Then, according to your choice, it loads an Elisp file. This Elisp file tells Geiser how to open the scheme implementation chosen with the right arguments.

Talking about these arguments, when it starts Gambit, as it is actually evolving from a monolithic system to a modularised one, it will verify which version of Gambit you are using to decide wether it will load the _geiser module or the geiser/scheme/gambit/geiser/* files to join the elisp functions to their Gambit Scheme's corresponding ones inside the GSI ( Gambit Scheme Interpreter )...
**** Geiser functionnalities:
***** form evaluation
For the form evaluation, there is a scheme function joined to
Geiser/gambit#geiser:eval function . this function will do the
afferent evaluation and returns a result and output.
***** macro expansion
The ability to use macros is of great help in a lot of context . But
sometimes it can become a headache (even more in huge programs ) to remember what do your macros refer to. Geiser offers a functionnality to display the expansion of the macro so that you can more easily use them.
***** file loading / compilation
As of now, the file compilation method is still to be implemented for
Gambit but the file loading and execution is working pretty well.
***** completions
Geiser offers a great autocompletion system for which I implemented
the gambit function as well. It works in two ways. 
If you configured Gambit using --enable-rtlib-debug, it will do it dynamically.
Else , it will go get it in an already defined function's list.
You can enable company-mode which will work in symbiosis with this autocompletion.
***** autodoc
While you code , the echo area also named mini buffer, like when
you write elisp code, will show you the function you are using
with the different arguments and which one of those your are actually
writing.
***** access to online documentation
This one is not implemented for Gambit.
***** Rudimentary support for debugging
Geiser also offers rudimentary support for debugging and I will show
you how in the demo, but there is still a lot of upgrades that I am
working on for this part. Though, this stays very usable as you can also
plug the gambit.el mode with geiser and use it for the debugging part
***** support for multiple simultaneous REPLs
***** Remote connection
you can also connect Geiser to an external Gambit REPL , and use this
REPL remotely with Geiser.

The explanation about how to do so is in the geiser doc and also in
the gambit's doc.
***** Functionalities helper
You probably already ask yourself how many Keybinds you will have to
learn to become Geiser fluent hahaha but dont worry, there is little
helpers close enough to help you remember all of them at any time :

when you will start geiser, in the Emacs menubar, a new geiser option
will appear.

If you click on it , it will give you a lot of functionnalities and
their matching keybinds.

And if you dont like to use menubars ; dont worry ! you can always use
the ctrl-h m keybind to access the emacs help page for you mode!
***** Form Evaluation
Because we like to double check what we are coding , being able to
evaluate each and every single part of it is important . Geiser gives
you a lot of different functions to evaluate your Scheme files and
their multiple sexpressions.
***** Pay attention to the details
because this is always the small details that makes the big pictures ,
it is very important to pay attention to all those small details that
I personally think are really importants when coding.

Geiser offers great code indentation in the REPL and parenthesis
balancing at all time. The macro expansions . A debugger. a cool way
to connect remotely to a REPL . And ALL OF THIS IN A fully
customizable environment.
***** Coming soon
As it was juste one of numerous things I worked on this summer there
is obviously a lot of cool things still to add to it.
****** current thread identification in the repl
this one is almost ready

Let me know in the comments if you have any questions or comments ! :) 

Math
