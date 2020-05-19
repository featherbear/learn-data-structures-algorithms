---
title: "Recursion"
layout: "bundle"
outputs: ["Reveal"]
date: 2020-05-20T01:51:56+10:00
draft: true
---

Base Case  
Recursive Case

Factorials - count from 1!!!!!!!!
Fibonacci post  https://featherbear.cc/UNSW-COMP2521/blog/post/c-fibonacci/

Tail-call optimisation is where you are able to avoid allocating a new stack frame for a function because the calling function will simply return the value that it gets from the called function.

A function ends with a tail call if the last operation before the function returns is another function call. If this call invokes the same function, it is tail-recursive.

// A function can probably be optimised if it’s last operation is calling itself