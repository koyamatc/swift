---
title: Swift
layout: post
postTitle:  Ternary Conditional Operator
categories: basicoperators
---

３項条件演算子
==============================

３項条件演算子は、３つの部分を持つ特別な演算子で、
問い ? 答え1 : 答え2　という形式をとります。

問いが true なら、　答え1が評価されその値が返り、
問いが false なら、　答え2が評価されその値が返ります。

３項条件演算子は下のｺｰﾄﾞの短縮形です
{% highlight c linenos %}
if question {
    answer1
} else {
    answer2
}
{% endhighlight %}

{% highlight c linenos %}
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50 : 20)
// rowHeight is equal to 90
{% endhighlight %}

上の例は、下のｺｰﾄﾞの短縮形です。

{% highlight c linenos %}
let contentHeight = 40
let hasHeader = true
var rowHeight = contentHeight
if hasHeader {
    rowHeight = rowHeight + 50
} else {
    rowHeight = rowHeight + 20
}
// rowHeight is equal to 90
{% endhighlight %}

使い過ぎに注意、読みずらいコードになる