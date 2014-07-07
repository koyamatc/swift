---
title: Swift
layout: post
postTitle:  Function Parameter Names
categories: functions
---

{% highlight c linenos %}
func someFunction(parameterName: Int) {
    // function body goes here, and can use parameterName
    // to refer to the argument value for that parameter
}
{% endhighlight %}

ここで指定されたパラメータ名は、関数内部でだけ使うことができます。　

これをローカル・パラメータ名と呼びます。

###External Parameter Names

関数を呼ぶときに関数に受け渡す引数の目的を表すような名前をパラメータに付けることは有益です。

ローカル・パラメータ名に加えて、外部パラメータ名を書くことができます。

{% highlight c linenos %}
func someFunction(externalParameterName localParameterName: Int) {
    // function body goes here, and can use localParameterName
    // to refer to the argument value for that parameter
}
{% endhighlight %}

<div class="panel">
	<div class="panel-heading">NOTe</div>
	パラメータに外部パラメータ名を設定したら、関数を呼ぶときには必ず外部パラメータ名を使わなければならない
</div>

以下の関数で考えてみましょう

{% highlight c linenos %}
func join(s1: String, s2: String, joiner: String) -> String {
    return s1 + joiner + s2
}
{% endhighlight %}

When you call this function, the purpose of the three strings that you pass to the function is unclear:

{% highlight c linenos %}
join("hello", "world", ", ")
// returns "hello, world"
{% endhighlight %}

To make the purpose of these String values clearer, define external parameter names for each join function parameter:

{% highlight c linenos %}
func join(string s1: String, toString s2: String, withJoiner joiner: String)
    -> String {
        return s1 + joiner + s2
}
{% endhighlight %}

In this version of the join function, the first parameter has an external name of string and a local name of s1; the second parameter has an external name of toString and a local name of s2; and the third parameter has an external name of withJoiner and a local name of joiner.

You can now use these external parameter names to call the function in a clear and unambiguous way:

{% highlight c linenos %}
join(string: "hello", toString: "world", withJoiner: ", ")
// returns "hello, world"
{% endhighlight %}

The use of external parameter names enables this second version of the join function to be called in an expressive, sentence-like manner by users of the function, while still providing a function body that is readable and clear in intent.

NOTE

Consider using external parameter names whenever the purpose of a function’s arguments would be unclear to someone reading your code for the first time. You do not need to specify external parameter names if the purpose of each parameter is clear and unambiguous when the function is called.

###Shorthand External Parameter Names

If you want to provide an external parameter name for a function parameter, and the local parameter name is already an appropriate name to use, you do not need to write the same name twice for that parameter. Instead, write the name once, and prefix the name with a hash symbol (#). This tells Swift to use that name as both the local parameter name and the external parameter name.

This example defines a function called containsCharacter, which defines external parameter names for both of its parameters by placing a hash symbol before their local parameter names:

func containsCharacter(#string: String, #characterToFind: Character) -> Bool {
    for character in string {
        if character == characterToFind {
            return true
        }
    }
    return false
}
This function’s choice of parameter names makes for a clear, readable function body, while also enabling the function to be called without ambiguity:

let containsAVee = containsCharacter(string: "aardvark", characterToFind: "v")
// containsAVee equals true, because "aardvark" contains a "v"
Default Parameter Values

You can define a default value for any parameter as part of a function’s definition. If a default value is defined, you can omit that parameter when calling the function.

NOTE

Place parameters with default values at the end of a function’s parameter list. This ensures that all calls to the function use the same order for their non-default arguments, and makes it clear that the same function is being called in each case.

Here’s a version of the join function from earlier, which provides a default value for its joiner parameter:

func join(string s1: String, toString s2: String,
    withJoiner joiner: String = " ") -> String {
        return s1 + joiner + s2
}
If a string value for joiner is provided when the join function is called, that string value is used to join the two strings together, as before:

join(string: "hello", toString: "world", withJoiner: "-")
// returns "hello-world"
However, if no value of joiner is provided when the function is called, the default value of a single space (" ") is used instead:

join(string: "hello", toString: "world")
// returns "hello world"
External Names for Parameters with Default Values

In most cases, it is useful to provide (and therefore require) an external name for any parameter with a default value. This ensures that the argument for that parameter is clear in purpose if a value is provided when the function is called.

To make this process easier, Swift provides an automatic external name for any defaulted parameter you define, if you do not provide an external name yourself. The automatic external name is the same as the local name, as if you had written a hash symbol before the local name in your code.

Here’s a version of the join function from earlier, which does not provide external names for any of its parameters, but still provides a default value for its joiner parameter:

func join(s1: String, s2: String, joiner: String = " ") -> String {
    return s1 + joiner + s2
}
In this case, Swift automatically provides an external parameter name of joiner for the defaulted parameter. The external name must therefore be provided when calling the function, making the parameter’s purpose clear and unambiguous:

join("hello", "world", joiner: "-")
// returns "hello-world"
NOTE

You can opt out of this behavior by writing an underscore (_) instead of an explicit external name when you define the parameter. However, external names for defaulted parameters are always preferred where appropriate.

###Variadic Parameters

A variadic parameter accepts zero or more values of a specified type. You use a variadic parameter to specify that the parameter can be passed a varying number of input values when the function is called. Write variadic parameters by inserting three period characters (...) after the parameter’s type name.

The values passed to a variadic parameter are made available within the function’s body as an array of the appropriate type. For example, a variadic parameter with a name of numbers and a type of Double... is made available within the function’s body as a constant array called numbers of type Double[].

The example below calculates the arithmetic mean (also known as the average) for a list of numbers of any length:

func arithmeticMean(numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// returns 3.0, which is the arithmetic mean of these five numbers
arithmeticMean(3, 8, 19)
// returns 10.0, which is the arithmetic mean of these three numbers
NOTE

A function may have at most one variadic parameter, and it must always appear last in the parameter list, to avoid ambiguity when calling the function with multiple parameters.

If your function has one or more parameters with a default value, and also has a variadic parameter, place the variadic parameter after all the defaulted parameters at the very end of the list.

###Constant and Variable Parameters

Function parameters are constants by default. Trying to change the value of a function parameter from within the body of that function results in a compile-time error. This means that you can’t change the value of a parameter by mistake.

However, sometimes it is useful for a function to have a variable copy of a parameter’s value to work with. You can avoid defining a new variable yourself within the function by specifying one or more parameters as variable parameters instead. Variable parameters are available as variables rather than as constants, and give a new modifiable copy of the parameter’s value for your function to work with.

Define variable parameters by prefixing the parameter name with the keyword var:

func alignRight(var string: String, count: Int, pad: Character) -> String {
    let amountToPad = count - countElements(string)
    for _ in 1...amountToPad {
        string = pad + string
    }
    return string
}
let originalString = "hello"
let paddedString = alignRight(originalString, 10, "-")
// paddedString is equal to "-----hello"
// originalString is still equal to "hello"
This example defines a new function called alignRight, which aligns an input string to the right edge of a longer output string. Any space on the left is filled with a specified padding character. In this example, the string "hello" is converted to the string "-----hello".

The alignRight function defines the input parameter string to be a variable parameter. This means that string is now available as a local variable, initialized with the passed-in string value, and can be manipulated within the body of the function.

The function starts by working out how many characters need to be added to the left of string in order to right-align it within the overall string. This value is stored in a local constant called amountToPad. The function then adds amountToPad copies of the pad character to the left of the existing string and returns the result. It uses the string variable parameter for all its string manipulation.

NOTE

The changes you make to a variable parameter do not persist beyond the end of each call to the function, and are not visible outside the function’s body. The variable parameter only exists for the lifetime of that function call.

###In-Out Parameters

Variable parameters, as described above, can only be changed within the function itself. If you want a function to modify a parameter’s value, and you want those changes to persist after the function call has ended, define that parameter as an in-out parameter instead.

You write an in-out parameter by placing the inout keyword at the start of its parameter definition. An in-out parameter has a value that is passed in to the function, is modified by the function, and is passed back out of the function to replace the original value.

You can only pass a variable as the argument for an in-out parameter. You cannot pass a constant or a literal value as the argument, because constants and literals cannot be modified. You place an ampersand (&) directly before a variable’s name when you pass it as an argument to an inout parameter, to indicate that it can be modified by the function.

NOTE

In-out parameters cannot have default values, and variadic parameters cannot be marked as inout. If you mark a parameter as inout, it cannot also be marked as var or let.

Here’s an example of a function called swapTwoInts, which has two in-out integer parameters called a and b:

func swapTwoInts(inout a: Int, inout b: Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
The swapTwoInts function simply swaps the value of b into a, and the value of a into b. The function performs this swap by storing the value of a in a temporary constant called temporaryA, assigning the value of b to a, and then assigning temporaryA to b.

You can call the swapTwoInts function with two variables of type Int to swap their values. Note that the names of someInt and anotherInt are prefixed with an ampersand when they are passed to the swapTwoInts function:

var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
println("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// prints "someInt is now 107, and anotherInt is now 3"
The example above shows that the original values of someInt and anotherInt are modified by the swapTwoInts function, even though they were originally defined outside of the function.

NOTE

In-out parameters are not the same as returning a value from a function. The swapTwoInts example above does not define a return type or return a value, but it still modifies the values of someInt and anotherInt. In-out parameters are an alternative way for a function to have an effect outside of the scope of its function body.
