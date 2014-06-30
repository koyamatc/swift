---
title: Swift
layout: post
postTitle:  Optionals
categories: basics
---

## オプショナル


値が無いかもしれない状況のときオプショナルを使います。

オプショナルは言います

値があり、それは3です

または

値はありません

たとえば、　SwiftのString型には、メソッド toInt があり、文字列を整数に変換しようとします。　
しかし、すべての文字列を整数に変換できるわけではありません。
文字列"123"は、数値123に変換できますが、"hello,world"は変換できません。

{% highlight c linenos %}
let possibleNumber = "123"
let convertedNumber = possibleNumber.toInt()
// convertedNumber は　"Int?"型、または "optional Int"型と推測されます
{% endhighlight %}
toIntメソッドは、整数ではなく、オプショナル整数を返すと失敗します。
オプショナル整数は、　Intではなく Int? 書きます。
疑問符は、値がオプショナルであることを示しています。
つまり、値は整数であるかもしれないし、値は無いかもしれないということです。

### If Statements and Forced Unwrapping

if文でオプショナルが値を持っているか、いないかがわかります。
値があれば、 true を返し、 値が無ければ、 false を返します。

オプショナルに値があることが分かれば、
オプショナルの名前の最後に感嘆符（!）を付けて、その値にアクセスすることができます。

これをオプショナル値の　forced unwrapping　といいます。
{% highlight c linenos %}
if convertedNumber {
    println("\(possibleNumber) has an integer value of \(convertedNumber!)")
} else {
    println("\(possibleNumber) could not be converted to an integer")
}
// prints "123 has an integer value of 123"
{% endhighlight %}

### Optional Binding

optional binding は、オプショナルが値を持っているかどうかを調べるのに使います。
もし持っていれば、その値を一時的に定数または変数として利用できるようにします。

optional binding は、if文やwhile文とともに使い、値をチェックし、定数まてゃ変数に取り出します。
{% highlight c linenos %}
if let constantName = someOptional {
    statements
}
{% endhighlight %}

上の possibleNumber の例を　forced unwrapping　ではなく　optional binding で書き直すと
{% highlight c linenos %}
if let actualNumber = possibleNumber.toInt() {
    println("\(possibleNumber) has an integer value of \(actualNumber)")
} else {
    println("\(possibleNumber) could not be converted to an integer")
}
// prints "123 has an integer value of 123"
{% endhighlight %}

This can be read as:

“If the optional Int returned by possibleNumber.toInt contains a value, set a new constant called actualNumber to the value contained in the optional.”

If the conversion is successful, the actualNumber constant becomes available for use within the first branch of the if statement. It has already been initialized with the value contained within the optional, and so there is no need to use the ! suffix to access its value. In this example, actualNumber is simply used to print the result of the conversion.

You can use both constants and variables with optional binding. If you wanted to manipulate the value of actualNumber within the first branch of the if statement, you could write if var actualNumber instead, and the value contained within the optional would be made available as a variable rather than a constant.

### nil

You set an optional variable to a valueless state by assigning it the special value nil:

var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value
NOTE

nil cannot be used with non-optional constants and variables. If a constant or variable in your code needs to be able to cope with the absence of a value under certain conditions, always declare it as an optional value of the appropriate type.

If you define an optional constant or variable without providing a default value, the constant or variable is automatically set to nil for you:

var surveyAnswer: String?
// surveyAnswer is automatically set to nil
NOTE

Swift’s nil is not the same as nil in Objective-C. In Objective-C, nil is a pointer to a non-existent object. In Swift, nil is not a pointer—it is the absence of a value of a certain type. Optionals of any type can be set to nil, not just object types.

### Implicitly Unwrapped Optionals

As described above, optionals indicate that a constant or variable is allowed to have “no value”. Optionals can be checked with an if statement to see if a value exists, and can be conditionally unwrapped with optional binding to access the optional’s value if it does exist.

Sometimes it is clear from a program’s structure that an optional will always have a value, after that value is first set. In these cases, it is useful to remove the need to check and unwrap the optional’s value every time it is accessed, because it can be safely assumed to have a value all of the time.

These kinds of optionals are defined as implicitly unwrapped optionals. You write an implicitly unwrapped optional by placing an exclamation mark (String!) rather than a question mark (String?) after the type that you want to make optional.

Implicitly unwrapped optionals are useful when an optional’s value is confirmed to exist immediately after the optional is first defined and can definitely be assumed to exist at every point thereafter. The primary use of implicitly unwrapped optionals in Swift is during class initialization, as described in Unowned References and Implicitly Unwrapped Optional Properties.

An implicitly unwrapped optional is a normal optional behind the scenes, but can also be used like a nonoptional value, without the need to unwrap the optional value each time it is accessed. The following example shows the difference in behavior between an optional String and an implicitly unwrapped optional String:

let possibleString: String? = "An optional string."
println(possibleString!) // requires an exclamation mark to access its value
// prints "An optional string."
 
let assumedString: String! = "An implicitly unwrapped optional string."
println(assumedString)  // no exclamation mark is needed to access its value
// prints "An implicitly unwrapped optional string."
You can think of an implicitly unwrapped optional as giving permission for the optional to be unwrapped automatically whenever it is used. Rather than placing an exclamation mark after the optional’s name each time you use it, you place an exclamation mark after the optional’s type when you declare it.

NOTE

If you try to access an implicitly unwrapped optional when it does not contain a value, you will trigger a runtime error. The result is exactly the same as if you place an exclamation mark after a normal optional that does not contain a value.

You can still treat an implicitly unwrapped optional like a normal optional, to check if it contains a value:

if assumedString {
    println(assumedString)
}
// prints "An implicitly unwrapped optional string."
You can also use an implicitly unwrapped optional with optional binding, to check and unwrap its value in a single statement:

if let definiteString = assumedString {
    println(definiteString)
}
// prints "An implicitly unwrapped optional string."
NOTE

Implicitly unwrapped optionals should not be used when there is a possibility of a variable becoming nil at a later point. Always use a normal optional type if you need to check for a nil value during the lifetime of a variable.

Assertions

Optionals enable you to check for values that may or may not exist, and to write code that copes gracefully with the absence of a value. In some cases, however, it is simply not possible for your code to continue execution if a value does not exist, or if a provided value does not satisfy certain conditions. In these situations, you can trigger an assertion in your code to end code execution and to provide an opportunity to debug the cause of the absent or invalid value.

Debugging with Assertions

An assertion is a runtime check that a logical condition definitely evaluates to true. Literally put, an assertion “asserts” that a condition is true. You use an assertion to make sure that an essential condition is satisfied before executing any further code. If the condition evaluates to true, code execution continues as usual; if the condition evaluates to false, code execution ends, and your app is terminated.

If your code triggers an assertion while running in a debug environment, such as when you build and run an app in Xcode, you can see exactly where the invalid state occurred and query the state of your app at the time that the assertion was triggered. An assertion also lets you provide a suitable debug message as to the nature of the assert.

You write an assertion by calling the global assert function. You pass the assert function an expression that evaluates to true or false and a message that should be displayed if the result of the condition is false:

let age = -3
assert(age >= 0, "A person's age cannot be less than zero")
// this causes the assertion to trigger, because age is not >= 0
In this example, code execution will continue only if age >= 0 evaluates to true, that is, if the value of age is non-negative. If the value of age is negative, as in the code above, then age >= 0 evaluates to false, and the assertion is triggered, terminating the application.

Assertion messages cannot use string interpolation. The assertion message can be omitted if desired, as in the following example:

assert(age >= 0)
When to Use Assertions

Use an assertion whenever a condition has the potential to be false, but must definitely be true in order for your code to continue execution. Suitable scenarios for an assertion check include:

An integer subscript index is passed to a custom subscript implementation, but the subscript index value could be too low or too high.
A value is passed to a function, but an invalid value means that the function cannot fulfill its task.
An optional value is currently nil, but a non-nil value is essential for subsequent code to execute successfully.
See also Subscripts and Functions.

NOTE

Assertions cause your app to terminate and are not a substitute for designing your code in such a way that invalid conditions are unlikely to arise. Nonetheless, in situations where invalid conditions are possible, an assertion is an effective way to ensure that such conditions are highlighted and noticed during development, before your app is published.