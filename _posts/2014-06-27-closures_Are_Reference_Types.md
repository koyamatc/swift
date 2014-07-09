---
title: Swift
layout: post
postTitle:  Closures Are Reference Types
categories: closures
---

前出の incrementBySeven と incrementByTen は定数です。
しかし、定数が参照しているクロージャは、受け取った　runningTotal変数を加算できます。
これは、関数とクロージャは参照型ということです。

関数またはクロージャを定数または変数に代入することは、
その定数または変数を、関数またはクロージャを参照するように設定することです。

２つの異なる定数、または変数に同じクロージャを代入すると、２つの定数または変数は、同じクロージャを参照するという意味です。

{% highlight c%}
let alsoIncrementByTen = incrementByTen
alsoIncrementByTen()
// returns a value of 50
{% endhighlight %}