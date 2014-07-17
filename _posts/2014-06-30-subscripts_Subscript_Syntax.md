---
title: Swift
layout: post
postTitle:  Subscript Syntax
categories: subscripts
---

添え字型の定義
{% highlight c %}
subscript(index: Int) -> Int {
    get {
        // return an appropriate subscript value here
    }
    set(newValue) {
        // perform a suitable setting action here
    }
}
{% endhighlight %}

newValueの型は、　添え字の戻り値の型と同じです。
セッタの　newValue パラメータは、記述しなくてもよい、
デフォルトパラメータ　newValueはセッタ用に提供される。

getキーワードを省いて、　リードオンリの添え字型とすることができる。 
{% highlight c %}
subscript(index: Int) -> Int {
    // return an appropriate subscript value here
}
{% endhighlight %}


Here’s an example of a read-only subscript implementation, which defines a TimesTable structure to represent an n-times-table of integers:

{% highlight c %}
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
let threeTimesTable = TimesTable(multiplier: 3)
println("six times three is \(threeTimesTable[6])")
// prints "six times three is 18"
{% endhighlight %}

three-times-tableを表すために、　TimeTableのインスタンスを作成しています。
値３を構造体TimesTableのイニシャライザに渡し、インスタンスの multiplier パラメータとして使っています。

threeTimesTableインスタンスに、添え字を付けて呼び出すことで問い合わせができます。
threeTimesTable[6]　は、　three-times-tableに　６回のエントリを求めています。
返される値は　18、　または　3 x 6 です。
