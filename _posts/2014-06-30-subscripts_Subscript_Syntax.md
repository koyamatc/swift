---
title: Swift
layout: post
postTitle:  Subscript Syntax
categories: subscripts
---

添え字型の定義
{% highlight c %}
subscript(index: Int) -> Int {
    get {
        // return an appropriate subscript value here
    }
    set(newValue) {
        // perform a suitable setting action here
    }
}
{% endhighlight %}

newValueの型は、　添え字の戻り値の型と同じです。
セッタの　newValue パラメータは、記述しなくてもよい、
デフォルトパラメータ　newValueはセッタ用に提供される。

getキーワードを省いて、　リードオンリの添え字型とすることができる。 
{% highlight c %}
subscript(index: Int) -> Int {
    // return an appropriate subscript value here
}
{% endhighlight %}


Here’s an example of a read-only subscript implementation, which defines a TimesTable structure to represent an n-times-table of integers:

{% highlight c %}
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
let threeTimesTable = TimesTable(multiplier: 3)
println("six times three is \(threeTimesTable[6])")
// prints "six times three is 18"
{% endhighlight %}
In this example, a new instance of TimesTable is created to represent the three-times-table. This is indicated by passing a value of 3 to the structure’s initializer as the value to use for the instance’s multiplier parameter.

You can query the threeTimesTable instance by calling its subscript, as shown in the call to threeTimesTable[6]. This requests the sixth entry in the three-times-table, which returns a value of 18, or 3 times 6.

NOTE

An n-times-table is based on a fixed mathematical rule. It is not appropriate to set threeTimesTable[someIndex] to a new value, and so the subscript for TimesTable is defined as a read-only subscript.