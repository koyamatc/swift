---
title: Swift
layout: post
postTitle:  Enumeration Syntax
categories: enumerations
---

列挙型を導入するには　enum キーワードを付けて、波カッコの中に定義をします。

{% highlight c %}
enum SomeEnumeration {
    // enumeration definition goes here
}
{% endhighlight %}

方位の４方向の例です。

{% highlight c %}
enum CompassPoint {
    case North
    case South
    case East
    case West
}
{% endhighlight %}

列挙して定義された値　（North, South, East, West） は、その列挙のメンバ値（またはメンバ）です。
case キーワードは、新しいメンバ値を定義することを指定します。

<div class="panel">
	<div class="panel-heading">NOTE</div>
	C や　Objective-C とは異なり、　Swiftの列挙メンバは、初期整数値に関連づけられていません。
	CompassPointの例でいうと、　North, South, East, West　は、　暗黙のうちに　0,1,2,3 
	と等しくありません。
</div>

複数のメンバ値をカンマ区切りで一行に設定することができます

{% highlight c %}
enum Planet {
    case Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune
}
{% endhighlight %}

Each enumeration definition defines a brand new type. Like other types in Swift, their names (such as CompassPoint and Planet) should start with a capital letter. Give enumeration types singular rather than plural names, so that they read as self-evident:

{% highlight c %}
var directionToHead = CompassPoint.West
{% endhighlight %}

The type of directionToHead is inferred when it is initialized with one of the possible values of CompassPoint. Once directionToHead is declared as a CompassPoint, you can set it to a different CompassPoint value using a shorter dot syntax:

{% highlight c %}
directionToHead = .East
{% endhighlight %}
The type of directionToHead is already known, and so you can drop the type when setting its value. This makes for highly readable code when working with explicitly-typed enumeration values.