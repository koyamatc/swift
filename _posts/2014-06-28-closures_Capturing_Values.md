---
title: Swift
layout: post
postTitle:  Capturing Values
categories: closures
---

A closure can capture constants and variables from the surrounding context in which it is defined. The closure can then refer to and modify the values of those constants and variables from within its body, even if the original scope that defined the constants and variables no longer exists.

The simplest form of a closure in Swift is a nested function, written within the body of another function. A nested function can capture any of its outer function’s arguments and can also capture any constants and variables defined within the outer function.

Here’s an example of a function called makeIncrementor, which contains a nested function called incrementor. The nested incrementor function captures two values, runningTotal and amount, from its surrounding context. After capturing these values, incrementor is returned by makeIncrementor as a closure that increments runningTotal by amount each time it is called.

func makeIncrementor(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementor() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementor
}
The return type of makeIncrementor is () -> Int. This means that it returns a function, rather than a simple value. The function it returns has no parameters, and returns an Int value each time it is called. To learn how functions can return other functions, see Function Types as Return Types.

The makeIncrementor function defines an integer variable called runningTotal, to store the current running total of the incrementor that will be returned. This variable is initialized with a value of 0.

The makeIncrementor function has a single Int parameter with an external name of forIncrement, and a local name of amount. The argument value passed to this parameter specifies how much runningTotal should be incremented by each time the returned incrementor function is called.

makeIncrementor defines a nested function called incrementor, which performs the actual incrementing. This function simply adds amount to runningTotal, and returns the result.

When considered in isolation, the nested incrementor function might seem unusual:

func incrementor() -> Int {
    runningTotal += amount
    return runningTotal
}
The incrementor function doesn’t have any parameters, and yet it refers to runningTotal and amount from within its function body. It does this by capturing the existing values of runningTotal and amount from its surrounding function and using them within its own function body.

Because it does not modify amount, incrementor actually captures and stores a copy of the value stored in amount. This value is stored along with the new incrementor function.

However, because it modifies the runningTotal variable each time it is called, incrementor captures a reference to the current runningTotal variable, and not just a copy of its initial value. Capturing a reference ensures sure that runningTotal does not disappear when the call to makeIncrementor ends, and ensures that runningTotal will continue to be available the next time that the incrementor function is called.

NOTE

Swift determines what should be captured by reference and what should be copied by value. You don’t need to annotate amount or runningTotal to say that they can be used within the nested incrementor function. Swift also handles all memory management involved in disposing of runningTotal when it is no longer needed by the incrementor function.

Here’s an example of makeIncrementor in action:

let incrementByTen = makeIncrementor(forIncrement: 10)
This example sets a constant called incrementByTen to refer to an incrementor function that adds 10 to its runningTotal variable each time it is called. Calling the function multiple times shows this behavior in action:

incrementByTen()
// returns a value of 10
incrementByTen()
// returns a value of 20
incrementByTen()
// returns a value of 30
If you create another incrementor, it will have its own stored reference to a new, separate runningTotal variable. In the example below, incrementBySeven captures a reference to a new runningTotal variable, and this variable is unconnected to the one captured by incrementByTen:

let incrementBySeven = makeIncrementor(forIncrement: 7)
incrementBySeven()
// returns a value of 7
incrementByTen()
// returns a value of 40
NOTE

If you assign a closure to a property of a class instance, and the closure captures that instance by referring to the instance or its members, you will create a strong reference cycle between the closure and the instance. Swift uses capture lists to break these strong reference cycles. For more information, see Strong Reference Cycles for Closures.