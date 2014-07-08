---
title: Swift
layout: post
postTitle:  Function Types
categories: functions
---

関数には、パラメータの型と戻り値の型から出来上がる特定の型があります。

{% highlight c linenos %}
func addTwoInts(a: Int, b: Int) -> Int {
    return a + b
}
func multiplyTwoInts(a: Int, b: Int) -> Int {
    return a * b
}
{% endhighlight %}
２つの関数の型は (Int, Int) -> Int　です

{% highlight c linenos %}
func printHelloWorld() {
    println("hello, world")
}
{% endhighlight %}

この関数の型は () -> ()　つまり　引数の無い関数で、返り値は void です。
これは空のタプル　() と同等です。


###Using Function Types

ある関数型の定数や変数を定義でき、その変数に適した関数を代入することができます。
{% highlight c %}
var mathFunction: (Int, Int) -> Int = addTwoInts
{% endhighlight %}

この意味は

「２つの整数値を受け取り、１つの整数値を返す関数の型を持つ、 mathFunction　という名の変数を定義し、
この新しい変数に、　addTwoInts という名の関数への参照を設定する」

addTwoInts 関数と　mathFunction 変数は同じ型です。

代入した関数を　mathFunction という名前で呼び出すことができます。

{% highlight c linenos %}
println("Result: \(mathFunction(2, 3))")
// prints "Result: 5"
{% endhighlight %}

型が同じ別の関数を、　同じ変数へ代入することができます。

{% highlight c linenos %}
mathFunction = multiplyTwoInts
println("Result: \(mathFunction(2, 3))")
// prints "Result: 6"
{% endhighlight %}

ほかの型と同様に、関数を定数や変数に代入すると、Swiftはその関数の型を推測します。

{% highlight c linenos %}
let anotherMathFunction = addTwoInts
// anotherMathFunction is inferred to be of type (Int, Int) -> Int
{% endhighlight %}

###Function Types as Parameter Types

(Int, Int) -> Int　のような関数型を、ほかの関数のパラメータ型として使うことができます。
これは、そｎ関数が呼ばれたときに、関数を呼び出した側に、関数が実装している概要をある程度教えることができます。

上記の算術関数の結果を印刷する例です

{% highlight c linenos %}
func printMathResult(mathFunction: (Int, Int) -> Int, a: Int, b: Int) {
    println("Result: \(mathFunction(a, b))")
}
printMathResult(addTwoInts, 3, 5)
// prints "Result: 8"
{% endhighlight %}

３つのパラメータを持つ　printMathResult関数を定義します。
第１パラメータは、(Int, Int) -> Int　型の　mathFunction　です。
この第１パラメータには、同じ型の関数ならば引数として受け渡すことができます。
２番目と３番目のパラメータは、整数型の a と　b　です。
この２つは、　mathFunction の　入力値として使われます。

printMathResultが呼ばれると、　addTwoInts関数と、整数値　3 と 5 が渡されます。
そして渡された関数を 3　と　5　を引数として呼び出し、その結果である　8 を出力します。

###Function Types as Return Types

関数型をほかの関数の戻り値の型として使えます。

{% highlight c linenos %}
func stepForward(input: Int) -> Int {
    return input + 1
}
func stepBackward(input: Int) -> Int {
    return input - 1
}
{% endhighlight %}

関数 chooseStepFunction　は、　戻り値が関数型の (Int) -> Int　です。 chooseStepFunction は、論理値パラメータの backwards　の値にしたがって　stepForward 関数か stepBackward 関数を返します。

{% highlight c linenos %}
func chooseStepFunction(backwards: Bool) -> (Int) -> Int {
    return backwards ? stepBackward : stepForward
}
{% endhighlight %}

これによって、一方へ進んだり、他方へ進む関数を持つ、　chooseStepFunction　を使えるようになります。

{% highlight c linenos %}
var currentValue = 3
let moveNearerToZero = chooseStepFunction(currentValue > 0)
// moveNearerToZero now refers to the stepBackward() function
{% endhighlight %}

上記の例は、　変数　currentValue を徐々にゼロへ近づけるために、　正または負の移動値を算出します。
currentValue の初期値は３で、currentValue > 0 は true　を返し、
true は　chooseStepFunction に　stepBackward 関数を返します。
戻ってきた関数に対する参照が、定数 moveNearerToZero　に保存されています。

moveNearerToZero は、カウントダウンするのに正しい関数を参照しています。

{% highlight c linenos %}
println("Counting to zero:")
// Counting to zero:
while currentValue != 0 {
    println("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
println("zero!")
// 3...
// 2...
// 1...
// zero!
{% endhighlight %}
