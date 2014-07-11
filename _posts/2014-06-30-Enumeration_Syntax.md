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

上記２つの列挙の定義は、それぞれにまったく新しい型を定義しています。　
Swiftの他の型同様に、型の名前は大文字で始めます。
列挙型の名前は見てわかる単一の名前を付けます。

{% highlight c %}
var directionToHead = CompassPoint.West
{% endhighlight %}

directiontoHeadの型は　CompassPointが有効な値で初期化されると推測されます。
CompassPoint として　directonToHead が宣言されたならば、
より短いドット構文を使い、別の　CompassPointの値を、　directionToHead に設定することができます。 

{% highlight c %}
directionToHead = .East
{% endhighlight %}

directionToHeadの型はすでにわかっているので、値を設定するときにその型を省くことができます。
型が明白な値を扱うときは、とても読みやすいコードとなります。