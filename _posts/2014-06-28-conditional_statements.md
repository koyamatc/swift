---
title: Swift
layout: post
postTitle:  Conditional Statements
categories: control_flow
---


### If

{% highlight c linenos %}
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
}
// prints "It's very cold. Consider wearing a scarf."
{% endhighlight %}

if - else 

{% highlight c linenos %}
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else {
    println("It's not that cold. Wear a t-shirt.")
}
// prints "It's not that cold. Wear a t-shirt."
{% endhighlight %}

複数の if 文をつなげる

{% highlight c linenos %}
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    println("It's really warm. Don't forget to wear sunscreen.")
} else {
    println("It's not that cold. Wear a t-shirt.")
}
// prints "It's really warm. Don't forget to wear sunscreen."
{% endhighlight %}

条件の組合せが完全である必要がない場合には、最後の　else　はオプションであり、とりさることができます。

{% highlight c linenos %}
temperatureInFahrenheit = 72
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    println("It's really warm. Don't forget to wear sunscreen.")
}
{% endhighlight %}

この例では、温度が低すぎても高すぎてもメッセージは出力されません。

### Switch

同じ型の値を１つまたは複数に対して比較をする　swich 文の　単純な形です。

{% highlight c linenos %}
switch some value to consider {
case value 1:
    respond to value 1
case value 2,
value 3:
    respond to value 2 or 3
default:
    otherwise, do something else
}
{% endhighlight %}

例
{% highlight c linenos %}
let someCharacter: Character = "e"
switch someCharacter {
case "a", "e", "i", "o", "u":
    println("\(someCharacter) is a vowel")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
"n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    println("\(someCharacter) is a consonant")
default:
    println("\(someCharacter) is not a vowel or a consonant")
}
// prints "e is a vowel"
{% endhighlight %}


### No Implicit Fallthrough

C と Objective-C　とは対照的に、　
Swift の　swich 文は、　case 文の最後から　次の　case 文へと落ちていきません。
最初にマッチした　swich case が完了すると　break 文を書く必要なく、　その swich文全体が終了します。 
このことは c よりも安全で簡単に　swich　文を使えるし、　間違って複数の　case　文を実行するのを防げます。 

<div class="panel">
	<div class="panel-heading">NOTE</div>
	必要ならば、　マッチした　swich case 文が完了する前に、　break　文で抜けることもできます。
</div>

case の中身には少なくとも１つの実行可能な文が無ければいけません。
下記のｺｰﾄﾞは許されません。　コンパイルエラーとなります。

{% highlight c linenos %}
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a":
case "A":
    println("The letter A")
default:
    println("Not the letter A")
}
// this will report a compile-time error
{% endhighlight %}

C　の場合と異なり、　"a" と "A"　のどちらにもマッチしませんし、　それよりも、コンパイルエラーとなります。

複数個の検査値を書く場合には、カンマで区切ります。長くなれば、複数行にわたり書くことができます。

{% highlight c linenos %}
switch some value to consider {
case value 1,
value 2:
    statements
}
{% endhighlight %}

<div class="panel">
	<div class="panel-heading">NOTE</div>
	fallthrough キーワードを使って、 switch case を下へと降りていくことができます。	
</div>

### Range Matching

値が範囲に含まれているか検査できます
{% highlight c linenos %}
let count = 3_000_000_000_000
let countedThings = "stars in the Milky Way"
var naturalCount: String
switch count {
case 0:
    naturalCount = "no"
case 1...3:
    naturalCount = "a few"
case 4...9:
    naturalCount = "several"
case 10...99:
    naturalCount = "tens of"
case 100...999:
    naturalCount = "hundreds of"
case 1000...999_999:
    naturalCount = "thousands of"
default:
    naturalCount = "millions and millions of"
}
println("There are \(naturalCount) \(countedThings).")
// prints "There are millions and millions of stars in the Milky Way."
{% endhighlight %}

###Tuples

複数の値を検査するのにタプルを使えます。　
アンダースコア　(_)　を使い、可能な値すべてにマッチさせることができます。
{% highlight c linenos %}
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    println("(0, 0) is at the origin")
case (_, 0):
    println("(\(somePoint.0), 0) is on the x-axis")
case (0, _):
    println("(0, \(somePoint.1)) is on the y-axis")
case (-2...2, -2...2):
    println("(\(somePoint.0), \(somePoint.1)) is inside the box")
default:
    println("(\(somePoint.0), \(somePoint.1)) is outside of the box")
}
// prints "(1, 1) is inside the box"
{% endhighlight %}

C　とは違い、 Swift は、　複数の case で同じ値の検査を許します。
上記の例では、４つのcase すべてで　point(0,0) はマッチします。
複数のcase でマッチが可能だとしても、最初にマッチした　case が使われ、他は無視されます。

### Value Bindings

switch case で、　マッチした値を一時的に定数や変数に紐づけできして、case 文の中で使うことができます。
これを　値のバインディングといいます。

{% highlight c linenos %}
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    println("on the x-axis with an x value of \(x)")
case (0, let y):
    println("on the y-axis with a y value of \(y)")
case let (x, y):
    println("somewhere else at (\(x), \(y))")
}
// prints "on the x-axis with an x value of 2"
{% endhighlight %}

３つのswich文で　保存場所として　定数 x と　y　が宣言されていて、
一時的に、　anotherPoint から値が入ります。　

最初のcaseのcase (let x, 0)　は、　y=0 のすべての x とマッチし、その 点　x　の値が、一時的定数のxに代入されます。

２番目ののcaseのcase (0, let y)　は、　x=0 のすべての y とマッチし、その 点　y　の値が、一時的定数のxに代入されます。

宣言された一時的定数は、　case コード。ブロック内で使うことができます。

上記のswich文には、　default case がありません、
それは　最後の case、case let (x, y)　はすべての点とマッチするため　default case を必要としません。

上記の例では　let キーワードで定数として宣言されていますが、　
var キーワードで変数として宣言しcase 内で編集することができます。

### Where

条件を追加するために　where 節を使えます。

{% highlight c linenos %}
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    println("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    println("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    println("(\(x), \(y)) is just some arbitrary point")
}
// prints "(1, -1) is on the line x == -y"
{% endhighlight %}

３つの　switch case では、　一時的定数 x と　y　が宣言され　点の値が入っています。
この定数は、動的フィルターを作るために　where 節の一部として使われています。
switch case は、　where節の条件が真のときだけ点とマッチします。　
