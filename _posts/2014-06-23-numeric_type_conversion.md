---
title: Swift
layout: post
postTitle: Numeric Type Conversion
categories: basics
---

## 数値の型変換

###整数の型変換

整数が保持できる数値範囲は、その整数の型によって異なります。

Int8 は、 -128 から　127　の範囲で、
UInt8 は、 0 から 255 の範囲です。

範囲外の数値を代入しようとすると、コンパイル時にエラーとなります。

{% highlight c linenos %}
let cannotBeNegative: UInt8 = -1
// UInt8 は、負の数を持つことができないのでエラーとなります
let tooBig: Int8 = Int8.max + 1
// Int8 は、最大値より大きな値を持てないのでエラーとなります
{% endhighlight %}

したがって、適宜、型変換をすることで、エラーを回避できます。

変換するには、今ある値を、新しい型で初期化します。

{% highlight c linenos %}
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
{% endhighlight %}

SomeType(ofInitialValue) が、初期値を渡し、　Swiftの型イニシャライザーを呼び出す方法です

###Integer and Floating-Point Conversion

整数と浮動小数点数間の型変換は、はっきりとさせなくてはいけません。

{% highlight c linenos %}
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi は 3.14159　です、 型 Double が推測されます。
{% endhighlight %}

ここでは、定数 three の値は型 Double　として新しく作られ使われています、その結果、足し算の2つの値はどちらも同じ型になっています。
この変換がなければ、この足し算は許されません。

浮動小数点数を整数に変換するのも可能です。

{% highlight c linenos %}
let integerPi = Int(pi)
// integerPi は 3で、 型 Int が推測されます。
{% endhighlight %}

浮動小数点数を新しく整数で初期化すると、小数点以下が切り捨てられます。

4.75 は 4 に、　-3.9 は　-3 になります。

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>