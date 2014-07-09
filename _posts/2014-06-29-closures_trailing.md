---
title: Swift
layout: post
postTitle:  Trailing Closures
categories: closures
---

長いクロージャ表現を関数の最後の引数として渡す必要があるなら、　後付クロージャとして書くのが役立ちます。

{% highlight c %}
func someFunctionThatTakesAClosure(closure: () -> ()) {
    // function body goes here
}
 
// here's how you call this function without using a trailing closure:
 
someFunctionThatTakesAClosure({
    // closure's body goes here
    })
 
// here's how you call this function with a trailing closure instead:
 
someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}
{% endhighlight %}

<div class="panel">
    <div class="panel-heading">NOTE</div>
    クロージャが関数の唯一の引数であり、後付のクロージャとして書くならば、
    関数を呼ぶときに、関数名の後のカッコを書く必要はありません
</div>

前出の文字列の並べ替えクロージャを後付クロージャとして関数のカッコの外に書くと

{% highlight c %}
reversed = sort(names) { $0 > $1 }
{% endhighlight %}

後付クロージャが最も役立つのは、クロージャが長すぎて一行に書ききれないときです。
Swiftの　配列型には　map メソッドがあり、　１つだけの引数として　クロージャを受け取ります。

{% highlight c %}
let digitNames = [
    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",
    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"
]
let numbers = [16, 58, 510]

let strings = numbers.map {
    (var number) -> String in
    var output = ""
    while number > 0 {
        output = digitNames[number % 10]! + output
        number /= 10
    }
    return output
}
// strings is inferred to be of type String[]
// its value is ["OneSix", "FiveEight", "FiveOneZero"]
{% endhighlight %}

map 関数は配列の要素ごとにクロージャを呼び出します。
その時に、クロージャの入力パラメータと数を指定する必要はありません。
型は割り当てられる配列の値から推測されます。
