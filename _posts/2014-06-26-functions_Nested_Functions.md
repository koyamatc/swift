---
title: Swift
layout: post
postTitle:  Nested Functions
categories: functions
---

今までの関数はすべてグローバル関数でした、グローバル・スコープ上で定義されていました。
ほかの関数の中で、関数を定義することができます。

入れ子の関数は、デフォルトでは外から隠されています。
しかし入れ子の関数を含んでいる関数によって呼び出して使うことができます。
入れ子を内包している関数は、関数の外側のスコープで入れ子の関数が使えるように、その入れ子の関数を戻り値に設定することができます。

{% highlight c linenos %}
func chooseStepFunction(backwards: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backwards ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(currentValue > 0)
// moveNearerToZero now refers to the nested stepForward() function
while currentValue != 0 {
    println("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
println("zero!")
// -4...
// -3...
// -2...
// -1...
// zero!
{% endhighlight%}