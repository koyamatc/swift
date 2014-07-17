---
title: Swift
layout: post
postTitle:  Subscript Usage
categories: subscripts
---

"添え字"の正確な意味は、それが使われている中身に依ります。
添え字は通常、コレクション、リスト、シーケンスの中の要素にアクセスするショートカットとして使われます。
クラスや構造体の機能のために、添え字を実装することができます。

例えば、　Swiftのディクショナリ型は添え字を実装していて、ディクショナリインスタンスに保存される値をセットし取り出します。
{% highlight c %}
var numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
numberOfLegs["bird"] = 2
{% endhighlight %}


<div class="panel">
	<div class="panel-heading">NOTE</div>
	Swiftのディクショナリ型が実装している　key-value型の添え字は、オプショナル型の値をやり取りします。
	上記でいえば、値はオプショナルInt型です。
	ディクショナリ型が、オプショナルな添え字型を使っているのは、　
	keyに値のない場合が想定されるからです。
	また、keyに　nilを代入することで、そのkeyの値を削除する方法を提供しています。
</div>
