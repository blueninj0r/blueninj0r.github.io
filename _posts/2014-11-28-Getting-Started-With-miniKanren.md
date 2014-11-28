---
layout: post
title: Getting Started With miniKanren
published: false
---

Recently, I picked up [The Reasoned Schemer](http://mitpress.mit.edu/books/reasoned-schemer). It's a popular book on logic programming using a libary called miniKanren that was originally implemented for the Scheme language.

I've not got much Scheme experience and I struggled to find any instructions on running the examples in the book. This post should help other intrepid Scheme or logic programming newbies with their adventures. I'll also add some helpful links at the bottom.

### Step 1: Install Scheme!

There are a bunch of Scheme implementations out there. I chose [MIT Scheme](http://www.gnu.org/software/mit-scheme/). 

You can get it for OS X, Windows and various flavours of *nix. There are various download options on the site.

I just installed it on OS X with brew ```install mit-scheme```. Once this had ran I could boot up the Scheme REPL from the terminal with the ```mit-scheme``` command.

### Step 2: Get miniKanren

If you follow the download links on the miniKanren site you'll probably end up at [this Github repo](https://github.com/miniKanren/miniKanren). 

This is great, but, mk.scm only contains an implementation of miniKanren. You can't input examples as you seem them in the book - this isn't part of core Scheme. 

To get to the full Schemer experience you need to pull in a few other bits of Scheme code that will provide the ability to parse the examples as they are presented.

Grab the latest mk.scm from [here](https://raw.githubusercontent.com/miniKanren/miniKanren/master/mk.scm) and the other files from [here](https://raw.githubusercontent.com/miniKanren/TheReasonedSchemer/master/mkextraforms.scm) and [here](https://raw.githubusercontent.com/miniKanren/TheReasonedSchemer/master/mkprelude.scm) put them in the same directory.

(You might notice that some files come from a TheReasonedSchemer Github repo. This doesn't contain the latest implementation of mk.scm but is implemented by the authors).

### Step 3: Write some miniKanren!

Now you should have Scheme and the miniKanren implementation sitting in a folder somewhere. Let's write some basic code to prove it all hangs together. 

Beside the existing .scm files create hello_logic.scm and open it in the editor of your choice.

Start off by including miniKanren and the parser:

```(load "mk.scm")
(load "mkextraforms.scm")
(load "mkprelude.scm")```

And follow that up with some miniKanren code:

```(run* (q)
      (== #t q))```

Now save your file, head to the terminal and fire up mit-scheme in your working directory.

Once the REPL is going run the following command: (load "test.scm")

You should see something like:

```;Loading "test.scm"...
;  Loading "mk.scm"... done
;  Loading "mkextraforms.scm"... done
;  Loading "mkprelude.scm"... done
;... done
;Value 2: (#t)```

Hooray! That #t tells us this code ran as expected.

You're now ready to become a Reasoned Schemer.

Useful links:

[Scheme docs](http://www.gnu.org/software/mit-scheme/documentation/mit-scheme-user/index.html#Top)

[Scheme quick start](http://www.cs.brandeis.edu/~jrieffel/cs21/quickstart.html)

[miniKanren](http://minikanren.org/)
