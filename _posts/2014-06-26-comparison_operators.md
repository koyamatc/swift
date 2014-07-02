---
title: Swift
layout: post
postTitle:  Comparison Operators
categories: basicoperators
---

比較演算子
==============================


+ Equal to (a == b)
+ Not equal to (a != b)
+ Greater than (a > b)
+ Less than (a < b)
+ Greater than or equal to (a >= b)
+ Less than or equal to (a <= b)

<div class="panel">
	<div class="panel-head">
		NOTE
	</div>
	<div class="panel-body">
		Swift は、2つの identity operators (=== and !==)　もサポートしています、　
		これらは、比較する2つのオブジェクトが同じオブジェクトの実体を参照しているかどうかをテストするために使います。
	</div>
</div>

どの比較演算子も論理値を返します。

{% highlight c linenos %}
1 == 1   // true, because 1 is equal to 1
2 != 1   // true, because 2 is not equal to 1
2 > 1    // true, because 2 is greater than 1
1 < 2    // true, because 1 is less than 2
1 >= 1   // true, because 1 is greater than or equal to 1
2 <= 1   // false, because 2 is not less than or equal to 1
{% endhighlight %}

比較演算子は、if文のような条件文でしばしば使われます。

{% highlight c linenos %}
let name = "world"
if name == "world" {
    println("hello, world")
} else {
    println("I'm sorry \(name), but I don't recognize you")
}
// prints "hello, world", because name is indeed equal to "world"
{% endhighlight %}

