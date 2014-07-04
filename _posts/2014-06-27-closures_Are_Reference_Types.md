---
title: Swift
layout: post
postTitle:  Closures Are Reference Types
categories: closures
---

In the example above, incrementBySeven and incrementByTen are constants, but the closures these constants refer to are still able to increment the runningTotal variables that they have captured. This is because functions and closures are reference types.

Whenever you assign a function or a closure to a constant or a variable, you are actually setting that constant or variable to be a reference to the function or closure. In the example above, it is the choice of closure that incrementByTen refers to that is constant, and not the contents of the closure itself.

This also means that if you assign a closure to two different constants or variables, both of those constants or variables will refer to the same closure:

let alsoIncrementByTen = incrementByTen
alsoIncrementByTen()
// returns a value of 50