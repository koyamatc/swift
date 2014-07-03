---
title: Swift
layout: post
postTitle:  Comparing Strings
categories: strings_characters
---

文字列の比較
==============================

Swift は、文字列を比較する３つの方法を提供しています。
完全一致、前方一致、後方一致です。

### String Equality(完全一致)

２つの文字列は、　完全に同じ。
{% highlight c linenos %}
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    println("These two strings are considered equal")
}
// prints "These two strings are considered equal"
{% endhighlight %}

### Prefix and Suffix Equality(前方、後方一致)

文字列の中にに、調べたい文字列が先頭からまたは後方からあるかどうかを検査するのに
文字列メソッドの _hasPrefix_  または _hasSuffix_ を呼びます。

{% highlight c linenos %}
let romeoAndJuliet = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]
{% endhighlight %}

hasPrefix メソッドを使い romeoAndJuliet 配列の中に Act 1 シーンがいくつあるか数えます。

{% highlight c linenos %}
var act1SceneCount = 0
for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 1 ") {
        ++act1SceneCount
    }
}
println("There are \(act1SceneCount) scenes in Act 1")
// prints "There are 5 scenes in Act 1"
{% endhighlight %}

hasSuffix method を使って Capulet’s mansion と Friar Lawrence’s cell　の登場回数を数えます。

{% highlight c linenos %}
var mansionCount = 0
var cellCount = 0
for scene in romeoAndJuliet {
    if scene.hasSuffix("Capulet's mansion") {
        ++mansionCount
    } else if scene.hasSuffix("Friar Lawrence's cell") {
        ++cellCount
    }
}
println("\(mansionCount) mansion scenes; \(cellCount) cell scenes")
// prints "6 mansion scenes; 2 cell scenes"
{% endhighlight %}
