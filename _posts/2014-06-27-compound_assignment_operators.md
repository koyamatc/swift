---
title: Swift
layout: post
postTitle:  Compound Assignment Operators
categories: basicoperators
---


複合代入演算子
==============================

Swift は、(=) と　ほかの演算子を組み合わせた複合代入演算子を提供しています。 
加算演算子との例(+=):
{% highlight c linenos %}
var a = 1
a += 2
// a is now equal to 3
{% endhighlight %}

a += 2 は a = a + 2　の短縮形です。加算と代入が1つの演算子で1度にまとめて行われています。

<div class="panel">
	<div class="panel-head">
		NOTE
	</div>
	<div class="panel-body">
		複合代入演算子は値を返しません。let b = a += 2　のようには書けません。
	</div>
</div>
