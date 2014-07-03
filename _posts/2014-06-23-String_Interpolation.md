---
title: Swift
layout: post
postTitle:  String Interpolation
categories: strings_characters
---

文字列補完
==============================

_ 文字列補完 _ は、文字列リテラルの中に、定数、変数、リテラルを組合わせて新しい文字列を組み立てる方法です。
文字列リテラルに挿入される各要素は先頭にバックスラッシュを付けたカッコで囲みます。

{% highlight c linenos %}
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message is "3 times 2.5 is 7.5"
{% endhighlight %}

<div class="panel">
	<div class="panel-header">NOTE</div>
	<div class="panel-body">
		補完された文字列の中のカッコの中には、 ("),(\) それと　キャリッジリターン、ラインフィードは書くことができません。
	</div>
</div>
