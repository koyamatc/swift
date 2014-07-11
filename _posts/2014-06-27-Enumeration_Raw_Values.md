---
title: Swift
layout: post
postTitle:  Raw Values
categories: enumerations
---

関連値に対して、値を設定するもう一つの方法として、（raw value という)初期値を前もって設定することができます。

{% highlight c %}
enum ASCIIControlCharacter: Character {
    case Tab = "\t"
    case LineFeed = "\n"
    case CarriageReturn = "\r"
}
{% endhighlight %}

列挙値　ASCIIControlCharacter　のために　raw value が　Charactor型で宣言されています。
列挙値は、　ASCII制御文字が設定されています。

raw value は、関連値とは異なります。
raw value は、列挙を定義するときに前もって設定する値です。
決まった列挙のメンバの値は常に同じです。
関連値は。列挙のメンバの一つをもとに、新しい定数または変数が作られるときにセットされ、
そのたびに、その値は異なっていてかまいません。

raw valueの型は、文字列、文字、整数、浮動小数点数　です。
raw valueそれぞれは、列挙の宣言内でユニークでなくてはいけません。
raw valueとして整数が使われると、　列挙メンバのいくつかに値が指定されていないと、自動加算が行われます。

{% highlight c %}
enum Planet: Int {
    case Mercury = 1, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune
}
{% endhighlight %}

自動加算とは、　Planet.Venus　は　raw value ２　を持つということで、　その続きも同様です。

toRaw メソッド　で　列挙メンバの　raw value にアクセスできます

{% highlight c %}
let earthsOrder = Planet.Earth.toRaw()
// earthsOrder is 3
{% endhighlight %}

fromRaw メソッドで、　raw value を指定して　列挙メンバを見つけることができます。

{% highlight c %}
let possiblePlanet = Planet.fromRaw(7)
// possiblePlanet is of type Planet? and equals Planet.Uranus
{% endhighlight %}

すべての整数値で惑星を見つけられるわけではありません、
fromRawメソッドはオプショナルな列挙メンバを返します。
possiblePlanetの型は、　Planet? つまり、　オプショナルなPlanet　です。

9番を持った　Planet を探そうとすると、　fromRaw から返される値　オプショナルPlanet は　nil となります。

{% highlight c %}
let positionToFind = 9
if let somePlanet = Planet.fromRaw(positionToFind) {
    switch somePlanet {
    case .Earth:
        println("Mostly harmless")
    default:
        println("Not a safe place for humans")
    }
} else {
    println("There isn't a planet at position \(positionToFind)")
}
// prints "There isn't a planet at position 9"
{% endhighlight %}
この例では、　raw value 9 を持った惑星にアクセスするためにオプショナル　バインディングを使っています。
if let somePlanet = Planet.fromRaw(9)　文は、　オプショナル Planet を取り出します。
取り出すことができれば、　オプショナル Planet の内容に、　somePlanet を設定します。
この場合は、　9番目の惑星を取り出すことができないので　else 節が実行されます。
