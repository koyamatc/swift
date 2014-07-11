---
title: Swift
layout: post
postTitle:  Comparing Classes and Structures
categories: classes_and_structures
---

クラス と 構造体 は、　Swiftでは多くの共通点を持っています

+ Define properties to store values
+ Define methods to provide functionality
+ Define subscripts to provide access to their values using subscript syntax
+ Define initializers to set up their initial state
+ Be extended to expand their functionality beyond a default implementation
+ Conform to protocols to provide standard functionality of a certain kind

クラスには、構造体が持っていないものがあります

+ Inheritance enables one class to inherit the characteristics of another.
+ Type casting enables you to check and interpret the type of a class instance at runtime.
+ Deinitializers enable an instance of a class to free up any resources it has assigned.
+ Reference counting allows more than one reference to a class instance.

<div class="panel">
	<div class="panel-heading">NOTE</div>
	構造体は常にコピーされて使われるので、　リファレンス・カウンティングを使いません
</div>

###Definition Syntax

{% highlight c %}
class SomeClass {
    // class definition goes here
}
struct SomeStructure {
    // structure definition goes here
}
{% endhighlight %}

<div class="panel">
	<div class="panel-heading">NOTE</div>
	新しいクラスや構造体を定義するときは、　まったく新しい　Swift の型を定義していることになります。
	名前は、　UpperCamelCase　で与えす　（SomeClass、 SomeStructureのように）。
	一方、プロパティやメソッド名は、形名と区別するために、　lowerCamelCase で付けます（frameRate や incrementCountのように）
</div>

{% highlight c %}
struct Resolution {
    var width = 0
    var height = 0
}
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
{% endhighlight %}

### Class and Structure Instances

Resolution　構造体の定義と　VideMode クラスの定義は、それらがどのようなものかを表しているだけです。
それ自体が、特定の解像度やビデオモードを表してはいません。　
そうするためには、構造体やクラスのインスタンスを作る必要があります。

　　
インスタンスを作成す構文は、構造体とクラスでよく似ています。

{% highlight c %}
let someResolution = Resolution()
let someVideoMode = VideoMode()
{% endhighlight %}

###Accessing Properties

ドット構文で、インスタンスのプロパティにアクセスできます。

{% highlight c %}
println("The width of someResolution is \(someResolution.width)")
// prints "The width of someResolution is 0"
{% endhighlight %}

プロパティが持つプロパティへと辿って諭告とができます、
VideoMode のプロパティ　resolution の中の width プロパティへと。

{% highlight c %}
println("The width of someVideoMode is \(someVideoMode.resolution.width)")
// prints "The width of someVideoMode is 0"
{% endhighlight %}

ドット構文を使い、変数プロパティに新しい値を代入することができます。

{% highlight c %}
someVideoMode.resolution.width = 1280
println("The width of someVideoMode is now \(someVideoMode.resolution.width)")
// prints "The width of someVideoMode is now 1280"
{% endhighlight %}

<div class="panel">
	<div class="panel-heading">NOTE</div>
	Swiftは、構造体のプロパティであるサブプロパティに直接設定できます。　
</div>

### Memberwise Initializers for Structure Types

すべての構造体は、自動で生成されるイニシャライザを持ち、
新しいインスタンスのメンバプロパティを初期化するのに使えます。
新しインスタンスのプロパティに初期値は、名前によって、イニシャライザに渡されます。

{% highlight c %}
let vga = Resolution(width: 640, height: 480)
{% endhighlight %}

構造体とは異なり、クラスのインスタンスはデフォルトのプロパティメンバでのイニシャライザはありません。
