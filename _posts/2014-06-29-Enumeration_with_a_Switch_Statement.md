---
title: Swift
layout: post
postTitle:  Matching Enumeration Values with a Switch Statement
categories: enumerations
---

switch文で、個々の列挙値を使うことができます。

{% highlight c %}
directionToHead = .South
switch directionToHead {
case .North:
    println("Lots of planets have a north")
case .South:
    println("Watch out for penguins")
case .East:
    println("Where the sun rises")
case .West:
    println("Where the skies are blue")
}
// prints "Watch out for penguins"
{% endhighlight %}

switch文では、列挙型のメンバすべてを含んでいなければいけません。
case条件に　.Westが入っていないと、コンパイルエラーとなります。

すべてのメンバを　case に書けない場合は、　default case を書いて明示的に漏れがないようにすることができます。

{% highlight c %}
let somePlanet = Planet.Earth
switch somePlanet {
case .Earth:
    println("Mostly harmless")
default:
    println("Not a safe place for humans")
}
// prints "Mostly harmless"
{% endhighlight %}
