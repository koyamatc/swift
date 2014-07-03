---
title: Swift
layout: post
postTitle:  Uppercase and Lowercase Strings
categories: strings_characters
---

大文字　と　小文字
==============================

uppercaseString と lowercaseString プロパティを使い、　
文字列の大文字または小文字バージョンにアクセスできます。

{% highlight c linenos %}
let normal = "Could you help me, please?"
let shouty = normal.uppercaseString
// shouty is equal to "COULD YOU HELP ME, PLEASE?"
let whispered = normal.lowercaseString
// whispered is equal to "could you help me, please?"
{% endhighlight %}
