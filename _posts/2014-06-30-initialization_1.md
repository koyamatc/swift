---
title: Swift
layout: post
postTitle:  Setting Initial Values for Stored Properties
categories: initialization
---

クラスと構造体は、これらが生成されるときにすべてのストアドプロパティに初期値が設定されていなければならない。

初期値はイニシャライザの中で設定するか、プロパティの定義の中で初期値を代入することができす。
<div class="panel">
	<div class="panel-heading">NOTE</div>
	イニシャライザの中で初期値がセットされた場合、プロパティオブザーバは呼び出されません。
</div>

### Initializers

イニシャライザは、特定の型の新しいインスタンスが生成されるときに呼ばれます。
最も簡単な形式は、　init キーワードを使った、パラメータのないインスタンスメソッドのようです。

構造体　Fahrenheit です。
Fahrenheitは、Double型のストアドプロパティ　temperature　があります。 
{% highlight c %}
struct Fahrenheit {
    var temperature: Double
    init() {
        temperature = 32.0
    }
}
var f = Fahrenheit()
println("The default temperature is \(f.temperature)° Fahrenheit")
// prints "The default temperature is 32.0° Fahrenheit"
{% endhighlight %}

この構造体には、パラメータをもたない１つのイニシャライザ　init があります。
これは、ストアドのtemperature　を　値　32.0　で初期化します。　

<h3>Default Property Values</h3>

一方、プロパティの宣言時に、初期プロパティ値を指定することができます。

<div class="panel">
	<div class="panel-heading">NOTE</div>
	もしプロパティがいつも同じ初期値をとるのなら、イニシャライザの中でセットするのではなく、
	プロパティの宣言で初期プロパティ値を与えるほうがよい。
	最終結果は同じでも、初期値が、イニシャライザよりも宣言と結びついていたほうが、
	イニシャライザを短く、明瞭にすることができ、初期値から、型推論をすることができる。
</div>

初期値を与えた　より短くなった　Fahrenheit 構造体です。
{% highlight c %}
struct Fahrenheit {
    var temperature = 32.0
}
{% endhighlight %}