---
title: Swift
layout: post
postTitle:  Initializing an Empty String
categories: strings_characters
---

空の文字列を作る
==============================

空の文字列値を作るには、　空の文字列リテラルを変数に代入するか、
イニシャライザーで　新しい文字列のインスタンスを生成します。

{% highlight c linenos %}
var emptyString = ""               // empty string literal
var anotherEmptyString = String()  // initializer syntax
// these two strings are both empty, and are equivalent to each other
{% endhighlight %}

文字列値が空であるかをチェックするには　isEmpty プロパティ　を使います。

{% highlight c linenos %}
if emptyString.isEmpty {
    println("Nothing to see here")
}
// prints "Nothing to see here"
{% endhighlight %}
