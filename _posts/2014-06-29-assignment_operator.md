---
title: Swift
layout: post
postTitle:  Assignment Operator
categories: basicoperators
---


代入演算子
==============================

代入演算子 (a = b) は、　b の値で、　a の値を初期化または更新します。
{% highlight c linenos %}
let b = 10
var a = 5
a = b
// a is now equal to 10
{% endhighlight %}

代入の右辺が、複数の値を持ったタプルだと、　その要素は、定数または変数に分解されます。

{% highlight c linenos %}
let (x, y) = (1, 2)
// x is equal to 1, and y is equal to 2
{% endhighlight %}

Swift の代入演算子は値を返しません。下の文は無効です。

{% highlight c linenos %}
if x = y {
    // これは無効です, x = y は値を返さないからです。
}
{% endhighlight %}