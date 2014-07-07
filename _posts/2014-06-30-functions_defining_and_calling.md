---
title: Swift
layout: post
postTitle:  Defining and Calling Functions
categories: functions
---


func キーワード

sayHello 関数名

(personName: String) パラメータ名 : パラメータ型

-&gt; String 戻り値の型

{ .... } 命令文

return 戻り値をセットして終了

{% highlight c linenos %}
func sayHello(personName: String) -> String {
    let greeting = "Hello, " + personName + "!"
    return greeting
}

println(sayHello("Anna"))
// prints "Hello, Anna!"
println(sayHello("Brian"))
// prints "Hello, Brian!"
{% endhighlight %}



上記を簡単にすると
{% highlight c linenos %}
func sayHelloAgain(personName: String) -> String {
    return "Hello again, " + personName + "!"
}
println(sayHelloAgain("Anna"))
// prints "Hello again, Anna!"
{% endhighlight %}
