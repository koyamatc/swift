---
title: Swift
layout: post
postTitle:  String Literals
categories: strings_characters
---

文字列リテラル
==============================

前もって宣言した文字列値を、文字列リテラルとしてコードの中に含めることｇができます。
文字列リテラルは、　ダブルクォート("")に囲まれた、文字の並びです。

文字列リテラルは、定数や変数の初期値として使えます。

{% highlight c %}
let someString = "Some string literal value"
{% endhighlight %}


文字列リテラルには以下の特別な文字を含めることができます。

+ エスケープ文字 \0 (null character), \\\ (backslash), \t (horizontal tab), \n (line feed), \r (carriage return), \" (double quote) and \' (single quote)

+ Single-byte Unicode scalars,  \xnn　、 nnは 2つの １６進数。

+ Two-byte Unicode scalars,  \unnnn　、 nnnn は ４つの １６進数

+ Four-byte Unicode scalars,  \Unnnnnnnn　　、 nnnnnnnn は ８個の １６進数

{% highlight c linenos %}
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\x24"        // $,  Unicode scalar U+0024
let blackHeart = "\u2665"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\U0001F496"  // 💖, Unicode scalar U+1F496
{% endhighlight %}