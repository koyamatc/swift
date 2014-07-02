---
title: Swift
layout: post
postTitle:  Range Operators
categories: basicoperators
---

範囲演算子
==============================

Swift には２つの範囲演算子があり、　それは、値の範囲を表すための短縮形です。

###Closed Range Operator

閉じた範囲演算子 (a...b) は、 a から b の範囲で、a と　b　の値を含む、と定義されます。

{% highlight c linenos %}
for index in 1...5 {
    println("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
{% endhighlight %}

### Half-Closed Range Operator

半分閉じた範囲演算子 (a..b) は、 a から b　の範囲で b　を含まない　と定義されます。

半分閉じた範囲演算子は、配列などの0を規定としたリストで使うと便利です。
{% highlight c linenos %}
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..count {
    println("Person \(i + 1) is called \(names[i])")
}
// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
{% endhighlight %}
