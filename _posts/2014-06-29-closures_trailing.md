---
title: Swift
layout: post
postTitle:  Trailing Closures
categories: closures
---

If you need to pass a closure expression to a function as the function’s final argument and the closure expression is long, it can be useful to write it as a trailing closure instead. A trailing closure is a closure expression that is written outside of (and after) the parentheses of the function call it supports:

func someFunctionThatTakesAClosure(closure: () -> ()) {
    // function body goes here
}
 
// here's how you call this function without using a trailing closure:
 
someFunctionThatTakesAClosure({
    // closure's body goes here
    })
 
// here's how you call this function with a trailing closure instead:
 
someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}
NOTE

If a closure expression is provided as the function’s only argument and you provide that expression as a trailing closure, you do not need to write a pair of parentheses () after the function’s name when you call the function.

The string-sorting closure from the Closure Expression Syntax section above can be written outside of the sort function’s parentheses as a trailing closure:

reversed = sort(names) { $0 > $1 }
Trailing closures are most useful when the closure is sufficiently long that it is not possible to write it inline on a single line. As an example, Swift’s Array type has a map method which takes a closure expression as its single argument. The closure is called once for each item in the array, and returns an alternative mapped value (possibly of some other type) for that item. The nature of the mapping and the type of the returned value is left up to the closure to specify.

After applying the provided closure to each array element, the map method returns a new array containing all of the new mapped values, in the same order as their corresponding values in the original array.

Here’s how you can use the map method with a trailing closure to convert an array of Int values into an array of String values. The array [16, 58, 510] is used to create the new array ["OneSix", "FiveEight", "FiveOneZero"]:

let digitNames = [
    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",
    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"
]
let numbers = [16, 58, 510]
The code above creates a dictionary of mappings between the integer digits and English-language versions of their names. It also defines an array of integers, ready to be converted into strings.

You can now use the numbers array to create an array of String values, by passing a closure expression to the array’s map method as a trailing closure. Note that the call to numbers.map does not need to include any parentheses after map, because the map method has only one parameter, and that parameter is provided as a trailing closure:

let strings = numbers.map {
    (var number) -> String in
    var output = ""
    while number > 0 {
        output = digitNames[number % 10]! + output
        number /= 10
    }
    return output
}
// strings is inferred to be of type String[]
// its value is ["OneSix", "FiveEight", "FiveOneZero"]
The map function calls the closure expression once for each item in the array. You do not need to specify the type of the closure’s input parameter, number, because the type can be inferred from the values in the array to be mapped.

In this example, the closure’s number parameter is defined as a variable parameter, as described in Constant and Variable Parameters, so that the parameter’s value can be modified within the closure body, rather than declaring a new local variable and assigning the passed number value to it. The closure expression also specifies a return type of String, to indicate the type that will be stored in the mapped output array.

The closure expression builds a string called output each time it is called. It calculates the last digit of number by using the remainder operator (number % 10), and uses this digit to look up an appropriate string in the digitNames dictionary.

NOTE

The call to the digitNames dictionary’s subscript is followed by an exclamation mark (!), because dictionary subscripts return an optional value to indicate that the dictionary lookup can fail if the key does not exist. In the example above, it is guaranteed that number % 10 will always be a valid subscript key for the digitNames dictionary, and so an exclamation mark is used to force-unwrap the String value stored in the subscript’s optional return value.

The string retrieved from the digitNames dictionary is added to the front of output, effectively building a string version of the number in reverse. (The expression number % 10 gives a value of 6 for 16, 8 for 58, and 0 for 510.)

The number variable is then divided by 10. Because it is an integer, it is rounded down during the division, so 16 becomes 1, 58 becomes 5, and 510 becomes 51.

The process is repeated until number /= 10 is equal to 0, at which point the output string is returned by the closure, and is added to the output array by the map function.

The use of trailing closure syntax in the example above neatly encapsulates the closure’s functionality immediately after the function that closure supports, without needing to wrap the entire closure within the map function’s outer parentheses.
