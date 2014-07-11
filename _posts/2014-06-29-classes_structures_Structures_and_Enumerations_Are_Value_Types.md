---
title: Swift
layout: post
postTitle:  Structures and Enumerations Are Value Types
categories: classes_and_structures
---

_value type_ は、その値が定数や変数に代入されるときや、関数に受け渡されるときに、
複製される型です。
 
実際これまでの章で、　value型を使ってきました。
事実、Swiftのすべての基本型（整数、浮動小数点数、論理値、文字列、ディクショナリ）は　value型であり、構造体として実装しています。

Swift では、　すべての構造体と列挙型は　value型です。
複製されて使われます。

{% highlight c %}
let hd = Resolution(width: 1920, height: 1080)
var cinema = hd
{% endhighlight %}

定数hdを宣言し、Resolutionのインスタンスである hd に、width と height に　1920 と　1080 を与えて
初期化しています。 　

そして、　変数　cinema を宣言し、　cinemaに　hdの現在の値をセットしています。
Resolution は構造体なので、既存のインスタンスの複製が作られ、この新しい複製が　cinemaに代入されます。
今は、 cinema と　hd は同じ値を持っていたとしても、まったく異なるインスタンスです。

次にcinemaのwidthを返納します。
{% highlight c %}
cinema.width = 2048
println("cinema is now \(cinema.width) pixels wide")
// prints "cinema is now 2048 pixels wide"
{% endhighlight %}

hd　インスタンスの　widthプロパティは、　今も　1920　です。　

{% highlight c %}
println("hd is still \(hd.width) pixels wide")
// prints "hd is still 1920 pixels wide"
{% endhighlight %}

列挙型に対しても同じことが適用されます

{% highlight c %}
enum CompassPoint {
    case North, South, East, West
}
var currentDirection = CompassPoint.West
let rememberedDirection = currentDirection
currentDirection = .East
if rememberedDirection == .West {
    println("The remembered direction is still .West")
}
// prints "The remembered direction is still .West"
{% endhighlight %}

rememberedDirection　が　currentDirection で代入されたとき、
currentDirectionの複製がセットされています。
したがって、currentDirectionの値を変更しても、
rememberedDirection に保存された元の値の複製には影響しません。