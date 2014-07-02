---
title: Swift
layout: post
postTitle:  Working with Characters

categories: strings_characters
---

Character を使う
==============================

Swift　の 文字列型は　特定の順番に並んだ文字値の集まりとして表されます。
各文字値は１つの Unicode文字であらわされます。
文字列の中の個々の文字値にアクセスするには　for-in ループを使います。

{% highlight c linenos %}
for character in "Dog!🐶" {
    println(character)
}
// D
// o
// g
// !
// 🐶
{% endhighlight %}

一方、１文字だけの定数や変数は、　Character type 記法で、１文字の文字列リテラルから作ります。
{% highlight c %}
let yenSign: Character = "¥"
{% endhighlight %}
