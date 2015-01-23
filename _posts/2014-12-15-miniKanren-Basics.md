---
layout: post
title: Getting Started With miniKanren
published: false
---

When people learn some new piece of programming magic they often try and solve a problem they already understand. In time honoured tradition, I'd like to do the same in learning about miniKanren and its implementations in different languages.

"Hello, World" seemed a bit too straightforward for a first go, so, I've decided to implement the first Project Euler problem in Scheme with and without miniKanren. This should be simple enough to be easy to follow whilst still giving a small impression in the difference in program construction between the two approaches.

### The Problem

The first Project Euler problem is:

> Find the sum of all the multiples of 3 or 5 below 1000.

Pretty straightforward. You can find the problem and its siblings here: https://projecteuler.net/problem=1

### Solution 1: miniKa(n't)ren

Here's a solution in plain Scheme:

<PUT CODE HERE>

It's pretty straightforward. I think some programmers without Scheme or LISP experience would be able to understand what was going on.

The code, at the level we are writing and reasoning about it, is describing how to generate a list of numbers under 1,000, it is then explicitly checking each of these using a conditional based on the return values of two modulo operations before adding each value to the one preceding it.

This is a perfectly valid approach to the problem and it'll give you the correct answer to the problem as it is set.

### Solution 2: (load "mk.scm")

This solution is written in Scheme using the miniKanren and supporting libraries:

<PUT CODE HERE>

I think this is still a straightforward solution to the problem - it's probably still possible for a fair number of people to understand what's going on if they knew the problem.

It's already easy to see a difference in programming style, though, between this solution and the first one. 