---
title: Swift
layout: post
postTitle:  Logical Operators
categories: basicoperators
---

論理演算子
==============================

+ Logical NOT (!a)
+ Logical AND (a && b)
+ Logical OR (a || b)

### 論理 NOT 演算子

論理 NOT 演算子 (!a) は、　論理値を反対にします。　true は false に、　false は　true に。

{% highlight c linenos %}
let allowedEntry = false
if !allowedEntry {
    println("ACCESS DENIED")
}
// prints "ACCESS DENIED"
{% endhighlight %}

論理定数や変数の名前付けには注意しましょう、コードが読みにくく分かりにくくなります。

また、２重否定や複雑な論理条件文も避けましょう。

### 論理 AND 演算子

論理 AND 演算子 (a && b) は、２つの値がともに　true のとき、この表現で示される値は true となります。creates logical expressions where both values must be true for the 

どちらかの値が false ならば、　この値は　false　となります。

実際、最初の値が false　なら、２番目の値は評価されません。　
なぜならこの演算は　true にならないからです。
これは　*short-circuit evaluation* として知られています。

{% highlight c linenos %}
let enteredDoorCode = true
let passedRetinaScan = false
if enteredDoorCode && passedRetinaScan {
    println("Welcome!")
} else {
    println("ACCESS DENIED")
}
// prints "ACCESS DENIED"
{% endhighlight %}

###　論理 OR　演算子

論理 OR 演算子 (a || b) は、　２つのうちどちらかが　true ならば　式は　true となります。

論理 AND 演算子と同様に、論理 OR 演算子も short-circuit evaluation です。.

{% highlight c linenos %}
let hasDoorKey = false
let knowsOverridePassword = true
if hasDoorKey || knowsOverridePassword {
    println("Welcome!")
} else {
    println("ACCESS DENIED")
}
// prints "Welcome!"
{% endhighlight %}

### 論理演算子の結合

{% highlight c linenos %}
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
    println("Welcome!")
} else {
    println("ACCESS DENIED")
}
// prints "Welcome!"
{% endhighlight %}

### 明確化のカッコ

複合した論理演算をカッコを付けて、わかりやすくできます。

{% highlight c linenos %}
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
    println("Welcome!")
} else {
    println("ACCESS DENIED")
}
// prints "Welcome!"
{% endhighlight %}
