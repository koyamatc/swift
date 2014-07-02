---
title: Swift
layout: post
postTitle:  String Mutability
categories: strings_characters
---

文字列の可変性
==============================

変数に代入した文字列は変更できます。

{% highlight c linenos %}
var variableString = "Horse"
variableString += " and carriage"
// variableString is now "Horse and carriage"
 
let constantString = "Highlander"
constantString += " and another Highlander"
// this reports a compile-time error - a constant string cannot be modified
{% endhighlight %}