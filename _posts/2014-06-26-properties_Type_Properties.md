---
title: Swift
layout: post
postTitle:  Type Properties
categories: properties
---

インスタンス　プロパティは、特定の型のインスタンスに属するプロパティです。
その型のインスタンスを新しく作ると、そのインスタンスは、独自にプロパティ値を持ちます。

型自体に属するプロパティを定義することもできます。
どんなにたくさんのインスタンスを作っても、たった１つのプロパティのコピーしか存在しません。
このようなプロパティを型プロパティといいます。

型プロパティは、すべてに共通な値を定義するのに役立ちます。
すべてのインスタンスが使える定数プロパティや、
すべてのインスタンスに対しグローバルな値を保存する変数プロパティなど。

バリュー型（構造体、列挙）では、ストアドと計算型プロパティを定義できます。
クラスには、計算型プロパティだけができぎできます。

ヴァリュー型のストアド型プロパティは変数か定数になれます。
研鑽型プロパティは常に変数プロパティとして宣言されなければなりません。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    ストアド　インスタンス　プロパティとは違い、
    ストアド型プロパティには、初期値を与えなければならない。
    なぜなら、型それ自体はイニシャライザーを持たないので、
    初期化時にストアド型プロパティに値を設定することができないからです。
</div>


###Type Property Syntax

In C and Objective-C, you define static constants and variables associated with a type as global static variables. In Swift, however, type properties are written as part of the type’s definition, within the type’s outer curly braces, and each type property is explicitly scoped to the type it supports.

型プロパティを定義するには、
ヴァリュー型には、　static キーワードを付けます。
クラスには、　classキーワードを付けます
{% highlight c %}
struct SomeStructure {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
    // return an Int value here
    }
}
enum SomeEnumeration {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
    // return an Int value here
    }
}
class SomeClass {
    class var computedTypeProperty: Int {
    // return an Int value here
    }
}
{% endhighlight %}

<div class="panel">
    <div class="panel-heading">NOTE</div>
    上記の、計算型プロパティは、リードオンリですが、
    リードライトの計算型プロパティを定義することもできます。
</div>


###Querying and Setting Type Properties

Type properties are queried and set with dot syntax, just like instance properties. However, type properties are queried and set on the type, not on an instance of that type. For example:

{% highlight c %}
println(SomeClass.computedTypeProperty)
// prints "42"
 
println(SomeStructure.storedTypeProperty)
// prints "Some value."
SomeStructure.storedTypeProperty = "Another value."
println(SomeStructure.storedTypeProperty)
// prints "Another value."
{% endhighlight %}

The examples that follow use two stored type properties as part of a structure that models an audio level meter for a number of audio channels. Each channel has an integer audio level between 0 and 10 inclusive.

The figure below illustrates how two of these audio channels can be combined to model a stereo audio level meter. When a channel’s audio level is 0, none of the lights for that channel are lit. When the audio level is 10, all of the lights for that channel are lit. In this figure, the left channel has a current level of 9, and the right channel has a current level of 7:

image: ../Art/staticPropertiesVUMeter_2x.png
The audio channels described above are represented by instances of the AudioChannel structure:

{% highlight c %}
struct AudioChannel {
    static let thresholdLevel = 10
    static var maxInputLevelForAllChannels = 0
    var currentLevel: Int = 0 {
    didSet {
        if currentLevel > AudioChannel.thresholdLevel {
            // cap the new audio level to the threshold level
            currentLevel = AudioChannel.thresholdLevel
        }
        if currentLevel > AudioChannel.maxInputLevelForAllChannels {
            // store this as the new overall maximum input level
            AudioChannel.maxInputLevelForAllChannels = currentLevel
        }
    }
    }
}
{% endhighlight %}

The AudioChannel structure defines two stored type properties to support its functionality. The first, thresholdLevel, defines the maximum threshold value an audio level can take. This is a constant value of 10 for all AudioChannel instances. If an audio signal comes in with a higher value than 10, it will be capped to this threshold value (as described below).

The second type property is a variable stored property called maxInputLevelForAllChannels. This keeps track of the maximum input value that has been received by any AudioChannel instance. It starts with an initial value of 0.

The AudioChannel structure also defines a stored instance property called currentLevel, which represents the channel’s current audio level on a scale of 0 to 10.

The currentLevel property has a didSet property observer to check the value of currentLevel whenever it is set. This observer performs two checks:

If the new value of currentLevel is greater than the allowed thresholdLevel, the property observer caps currentLevel to thresholdLevel.
If the new value of currentLevel (after any capping) is higher than any value previously received by any AudioChannel instance, the property observer stores the new currentLevel value in the maxInputLevelForAllChannels static property.

NOTE

In the first of these two checks, the didSet observer sets currentLevel to a different value. This does not, however, cause the observer to be called again.

You can use the AudioChannel structure to create two new audio channels called leftChannel and rightChannel, to represent the audio levels of a stereo sound system:

{% highlight c %}
var leftChannel = AudioChannel()
var rightChannel = AudioChannel()
{% endhighlight %}

If you set the currentLevel of the left channel to 7, you can see that the maxInputLevelForAllChannels type property is updated to equal 7:

{% highlight c %}
leftChannel.currentLevel = 7
println(leftChannel.currentLevel)
// prints "7"
println(AudioChannel.maxInputLevelForAllChannels)
// prints "7"
{% endhighlight %}
If you try to set the currentLevel of the right channel to 11, you can see that the right channel’s currentLevel property is capped to the maximum value of 10, and the maxInputLevelForAllChannels type property is updated to equal 10:
{% highlight c %}
rightChannel.currentLevel = 11
println(rightChannel.currentLevel)
// prints "10"
println(AudioChannel.maxInputLevelForAllChannels)
// prints "10"
{% endhighlight %}