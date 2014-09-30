1. 

Let's publish a webpage

In
    /pub/fab/guide/exercise/1/hymn.hook

Put

    ;div
      ;h1: Exercise 1 — Simple HTML
      ;p: As you may notice, urbit has no problem talking to the web.
    ==

Try it

    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/1/

What did you just do?

The code you just wrote is urbit's naitive programming langauge, hoon. Generating HTML with hoon is similar to writing [jade](link) or other similar HTML shorthand. In hoon, this shorthand is called `++sail` and it's a naitive part of the hoon language.

In `++sail` node-names are prefixed with a `;` and closed with a `==`. Nodes that have text content and are only on one line use a `:` and are closed implicitly with a new line. Nodes with no content are closed with another `;`, such as `;br;`. 

When you need to you can find more information about `++sail` [here](link). 


2.

Let's do some programming on the page. 

In
    /pub/fab/guide/exercise/2/hymn.hook

Put

    ;div
      ;h1: Exercise 2 — Call a function
      ;p: Although it may be obvious, 2+2={<(add 2 2)>}
    ==

Try it
    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/2/

What's going on there?

Clearly, the code `(add 2 2)` is generating `4`, and it's not too hard to see why. `add` is one of the library functions that are a part of `hoon.hoon`. Try replacing `(add 2 2)` with `(sub 2 2)`. You can find documentaiton for the full hoon library in the [library reference](link) if you're interested. 

Since the product of `(add 2 2)` is a number, we need a few extra things to have it print properly. In `++sail` we use `{` and `}` to do string interpolation. Everything after the `:` is considered a string, so we need to tell the parser when we start writing code again. The `<` and `>` are converting our result `4`, a number, to the string `"4"`. hoon is a strongly typed language kind of like haskell. 


3. 

Let's assign some variables.

In
    /pub/fab/guide/exercise/3/hymn.hook

Put
    =+  a=2
    =+  ^=  b  (add 2 2)
    ;div
      ;h1: Assignment
      ;p: a={<a>}
      ;p: b={<b>}
      ;p: a+b={<(add a b)>}
    ==

Try it
    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/3/

How does that work?

The first thing you should notice in this example is the `=+` at the top of our file. `=+` is a rune. hoon is a programming with no reserved words. No `if` `this` or `function` at all. Instead, runes have their own pronunciation. `=+` is pronounced 'tislus'. You can find the table of pronunciation [here](link). In hoon you construct your programs using runes, which are two character ascii pairs. You can see the whole set of runes in the [rune index](link).

`=+` pushes an expression on to our subject. The subject in hoon is something like `this` in other languages. hoon being a functional language if we want something to be available further on in our computation we need to attach it to the subject first. 

Looking at the rendered page it's clear that we're assigning `a` to be `1` and `b` to be `2`. Looking at the code, however, you can see that we're doing this in two different ways. Runes in hoon can have irregular forms, and `^=` is one of them. The first two lines of our example are doing the same thing, where `a=2` is simply the irregular form of `^=  a  2`. You can see the full list of irregular forms [here](link).


4. 

Let's build our own computation

In
    /pub/fab/guide/exercise/3/hymn.hook

Put
    |%
      ++  start  1
      ++  end  10
      ++  length
        |=
          [start=@ud end=@ud]
        (sub end start)
    --
    ;div
      ;h1: Cores
      ;p: We'll be starting at {<start>}
      ;p: And ending at {<end>}
      ;p: Looks like a length of {<(length (add start 1) end)>}
    ==

Try it
    http://talsur-todres.urbit.org/gen/main/pub/fab/guide/exercise/4/

What's happening?

As you can see from the output, we have written a little function that takes two numbers, start and end and returns their difference. The first thing to notice about our code is the first rune. `|%` is a `core` rune. You can think of cores like functions or objects in other languages. `|%` runes contain an arbitrary number of arms, denoted with either `++` or `+-` and closed with `--`. 

Each arm has a value, either static data (in the case of `++start` and `++end`) or a gate (in the case of `++length`). A gate is a kind of core. Gates only have one arm and are quite similar to a function in other languages. We use `|=` to construct our gate. Runes in hoon are generally categorized by their first character. `|` indicates a rune having to do with cores. 

Our `++length` gate takes two arguments, start and end. In hoon we call this the 'sample'. Every `|=` has two parts, the sample type and the computation. `[start=@ud end=@ud]` says that the gate takes two arguments, each of which should be a `@ud` or unsigned decimal, and will be addressable as `start` and `end`. Our computation, `(sub end start)` simply computes the difference between `end` and `start`