---
title: Swift
layout: post
postTitle:  Closure Expressions
categories: closures
---

クロージャは、コードを書く中で、受け渡したり使ったりできる機能を含んでいるコードのブロックです。

Closures can capture and store references to any constants and variables from the context in which they are defined. This is known as closing over those constants and variables, hence the name “closures”. Swift handles all of the memory management of capturing for you.


グローバルや入れ子の関数は、クロージャの特別な場合です。クロージャは３つの形式をとります。

+ グローバル関数は名前は持ているが、どの値もキャプチャしないクロージャです。
+ 入れ子の関数は、名前があり、入れ子の関数を内包する関数から値を受け取るクロージャです。
+ クロージャの表記は、周囲のコンテキストから値を受け取れる簡単な文法で書かれた名前のないクロージャです・

Swift’s closure expressions have a clean, clear style, with optimizations that encourage brief, clutter-free syntax in common scenarios. These optimizations include:

+ Inferring parameter and return value types from context
+ Implicit returns from single-expression closures
+ Shorthand argument names
+ Trailing closure syntax

### Closure Expressions

Nested functions, as introduced in Nested Functions, are a convenient means of naming and defining self-contained blocks of code as part of a larger function. However, it is sometimes useful to write shorter versions of function-like constructs without a full declaration and name. This is particularly true when you work with functions that take other functions as one or more of their arguments.

Closure expressions are a way to write inline closures in a brief, focused syntax. Closure expressions provide several syntax optimizations for writing closures in their simplest form without loss of clarity or intent. The closure expression examples below illustrate these optimizations by refining a single example of the sort function over several iterations, each of which expresses the same functionality in a more succinct way.

### The Sort Function

Swiftの標準ライブラリは　sortという関数を提供しています、　
それはあなたが書いた並び換えクロージャの出力結果をもとに、
わかっている型の配列の値を並び替えます。
並び替えのプロセスを完了するたびに、　
sort 関数はもとの配列と同じ型、同じサイズの新しい配列を正しく並び替えて返します。

下記のクロージャの書き方の例では、　sort関数を使い、文字列の配列値を逆順に並べ替えをしています。

{% highlight c %}
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
{% endhighlight %}

The sort function takes two arguments:

An array of values of a known type.
A closure that takes two arguments of the same type as the array’s contents, and returns a Bool value to say whether the first value should appear before or after the second value once the values are sorted. The sorting closure needs to return true if the first value should appear before the second value, and false otherwise.
This example is sorting an array of String values, and so the sorting closure needs to be a function of type (String, String) -> Bool.

One way to provide the sorting closure is to write a normal function of the correct type, and to pass it in as the sort function’s second parameter:

func backwards(s1: String, s2: String) -> Bool {
    return s1 > s2
}
var reversed = sort(names, backwards)
// reversed is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
If the first string (s1) is greater than the second string (s2), the backwards function will return true, indicating that s1 should appear before s2 in the sorted array. For characters in strings, “greater than” means “appears later in the alphabet than”. This means that the letter "B" is “greater than” the letter "A", and the string "Tom" is greater than the string "Tim". This gives a reverse alphabetical sort, with "Barry" being placed before "Alex", and so on.

However, this is a rather long-winded way to write what is essentially a single-expression function (a > b). In this example, it would be preferable to write the sorting closure inline, using closure expression syntax.

### Closure Expression Syntax

Closure expression syntax has the following general form:

{ (parameters) -> return type in
    statements
}
Closure expression syntax can use constant parameters, variable parameters, and inout parameters. Default values cannot be provided. Variadic parameters can be used if you name the variadic parameter and place it last in the parameter list. Tuples can also be used as parameter types and return types.

The example below shows a closure expression version of the backwards function from earlier:

reversed = sort(names, { (s1: String, s2: String) -> Bool in
    return s1 > s2
    })
Note that the declaration of parameters and return type for this inline closure is identical to the declaration from the backwards function. In both cases, it is written as (s1: String, s2: String) -> Bool. However, for the inline closure expression, the parameters and return type are written inside the curly braces, not outside of them.

The start of the closure’s body is introduced by the in keyword. This keyword indicates that the definition of the closure’s parameters and return type has finished, and the body of the closure is about to begin.

Because the body of the closure is so short, it can even be written on a single line:

reversed = sort(names, { (s1: String, s2: String) -> Bool in return s1 > s2 } )
This illustrates that the overall call to the sort function has remained the same. A pair of parentheses still wrap the entire set of arguments for the function. However, one of those arguments is now an inline closure.

### Inferring Type From Context

Because the sorting closure is passed as an argument to a function, Swift can infer the types of its parameters and the type of the value it returns from the type of the sort function’s second parameter. This parameter is expecting a function of type (String, String) -> Bool. This means that the String, String, and Bool types do not need to be written as part of the closure expression’s definition. Because all of the types can be inferred, the return arrow (->) and the parentheses around the names of the parameters can also be omitted:

reversed = sort(names, { s1, s2 in return s1 > s2 } )
It is always possible to infer parameter types and return type when passing a closure to a function as an inline closure expression. As a result, you rarely need to write an inline closure in its fullest form.

Nonetheless, you can make the types explicit if you wish, and doing so is encouraged if it avoids ambiguity for readers of your code. In the case of the sort function, the purpose of the closure is clear from the fact that sorting is taking place, and it is safe for a reader to assume that the closure is likely to be working with String values, because it is assisting with the sorting of an array of strings.

### Implicit Returns from Single-Expression Closures

Single-expression closures can implicitly return the result of their single expression by omitting the return keyword from their declaration, as in this version of the previous example:

reversed = sort(names, { s1, s2 in s1 > s2 } )
Here, the function type of the sort function’s second argument makes it clear that a Bool value must be returned by the closure. Because the closure’s body contains a single expression (s1 > s2) that returns a Bool value, there is no ambiguity, and the return keyword can be omitted.

### Shorthand Argument Names

Swift automatically provides shorthand argument names to inline closures, which can be used to refer to the values of the closure’s arguments by the names $0, $1, $2, and so on.

If you use these shorthand argument names within your closure expression, you can omit the closure’s argument list from its definition, and the number and type of the shorthand argument names will be inferred from the expected function type. The in keyword can also be omitted, because the closure expression is made up entirely of its body:

{% highlight c %}
reversed = sort(names, { $0 > $1 } )
{% endhighlight %}

$0 と $1 は　クロージャの　１番目と２番目の文字列引数を参照しています。

### Operator Functions

上記のクロージャの書き方を短くする方法があります。
Swift の文字列型は、２つの文字列型のパラメータをとり、真偽値を返す関数として　（>） を
文字列型特有に実装しています。
これは sort 関数の２番目のパラメータとして必要な関数型にぴったりです。
それゆえ、　> 演算子を受け渡すと、　Swiftは、文字列特有の実装された機能を使いたいのだと推測します。

{% highlight c %}
reversed = sort(names, >)
{% endhighlight %}
