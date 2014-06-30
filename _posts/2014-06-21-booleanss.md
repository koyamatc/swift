---
title: Swift
layout: post
postTitle:  Booleans
categories: basics
---

## 真偽値

Swift には　Bool という基本的な真偽型があり、　２つの真偽定数値　true と false　があります。

{% highlight c linenos %}
let orangesAreOrange = true
let turnipsAreDelicious = false
{% endhighlight %}

真偽値はif文のような条件文とともに使うと特に役立ちます。e if statement:

{% highlight c linenos %}
if turnipsAreDelicious {
    println("Mmm, tasty turnips!")
} else {
    println("Eww, turnips are horrible.")
}
// prints "Eww, turnips are horrible."
{% endhighlight %}

Swift’s 型安全機能は 真偽値でないものが　Boolの代わりになることを防ぎます。　よって、下記の例はコンパイルエラーとなります。

{% highlight c linenos %}
let i = 1
if i {
    // this example will not compile, and will report an error
}
{% endhighlight %}

しかし、下記の例は有効です。

{% highlight c linenos %}
let i = 1
if i == 1 {
    // this example will compile successfully
}
{% endhighlight %}

i == 1　の比較結果は Bool型なので、2番目の例は型チェックを無事通過します。
