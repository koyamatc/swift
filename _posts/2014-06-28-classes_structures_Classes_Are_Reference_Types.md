---
title: Swift
layout: post
postTitle:  Classes Are Reference Types
categories: classes_and_structures
---

_value 型_ とは違い、 _参照型_  は、　変数や定数に代入されるときや、関数へ受け渡されるとき複製されるのではない。
同じ存在しているインスタンスへの参照が使われます。

{% highlight c %}
let tenEighty = VideoMode()
tenEighty.resolution = hd
tenEighty.interlaced = true
tenEighty.name = "1080i"
tenEighty.frameRate = 25.0
{% endhighlight %}

この例では、定数　tenEighty を定義し、　VideoMode クラスの新しいインスタンスへの参照を設定しています。

次に、　新しい定数　alsoTenEighty に　tenEight　を代入して、　
aolsoTenEighty の　frame rate を　変更します。

{% highlight c %}
let alsoTenEighty = tenEighty
alsoTenEighty.frameRate = 30.0
{% endhighlight %}

クラスは参照型なので、tenEighty と　alsoTenEighty は同じ　VideoMode インスタンスを参照しています。
つまり、１つの同じインスタンスに対して２つの異なる名前があるということです。

{% highlight c %}
println("The frameRate property of tenEighty is now \(tenEighty.frameRate)")
// prints "The frameRate property of tenEighty is now 30.0"
{% endhighlight %}

tenEighty と alsoTenEightyは、変数としてではなく定数として宣言されています。
しかし、tenEighty.frameRate と alsoTenEighty.frameRate を変更することができます、
それは　tenEighty と alsoTenEighty　定数それ自身の値が変更されている訳ではないのです。
tenEighty と alsoTenEighty自体は　VideoModeインスタンスを保持しているのではなく、参照しているだけです。
元なるVideoModeの frameRateプロパティが変更されているのであって、
そのVideoModeにたいして定数が参照している値を変更しているのではない。

### Identity Operators

クラスは参照型なので、複数の定数、変数が、１つの同じ九sラスのインスタンスを参照することができます。

２つの定数または変数が、まったく同じクラスのインスタンスを参照しているかを調べることが役立つ時があります。

Swiftには２つのidentity演算子があります。
+ identical to (===)
+ Not identical to (!==)

{% highlight c %}
if tenEighty === alsoTenEighty {
    println("tenEighty and alsoTenEighty refer to the same VideoMode instance.")
}
// prints "tenEighty and alsoTenEighty refer to the same VideoMode instance."
{% endhighlight %}

“Identical to” は、　２つのクラス型の定数または変数が、まったく同じクラスのインスタンスを参照していることです。

“Equal to” は、　値において２つのインスタンスは同じであるとということです。

どちらの性質を持たせるかは、　カスタムクラスまたは構造体を定義するときに決まります。

###Pointers

C, C++, や Objective-C　では、　メモリ上のアドレスを参照するのに　ポインターを使います。
Swiftで参照型のインスタンスを参照する定数や変数は　C における　ポインターと似ていますが、
メモリ上のアドレスへのダイレクトポインターではありません。
