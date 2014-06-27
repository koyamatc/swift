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
// UInt8 cannot store negative numbers, and so this will report an error
let tooBig: Int8 = Int8.max + 1
// Int8 cannot store a number larger than its maximum value,
// and so this will also report an error
{% endhighlight %}

したがって、適宜、型変換をすることで、エラーを回避できます。

変換するには、今ある値を、新しい型で初期化します。

{% highlight c linenos %}
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
{% endhighlight %}

SomeType(ofInitialValue) is the default way to call the initializer of a Swift type and pass in an initial value. Behind the scenes, UInt16 has an initializer that accepts a UInt8 value, and so this initializer is used to make a new UInt16 from an existing UInt8. You can’t pass in any type here, however—it has to be a type for which UInt16 provides an initializer. Extending existing types to provide initializers that accept new types (including your own type definitions) is covered in Extensions.

###Integer and Floating-Point Conversion

Conversions between integer and floating-point numeric types must be made explicit:
{% highlight c linenos %}
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi equals 3.14159, and is inferred to be of type Double
{% endhighlight %}
Here, the value of the constant three is used to create a new value of type Double, so that both sides of the addition are of the same type. Without this conversion in place, the addition would not be allowed.

The reverse is also true for floating-point to integer conversion, in that an integer type can be initialized with a Double or Float value:

{% highlight c linenos %}
let integerPi = Int(pi)
// integerPi equals 3, and is inferred to be of type Int
{% endhighlight %}

浮動小数点数を新しく整数で初期化すると、小数点以下が切り捨てられます。

4.75 は 4 に、　-3.9 は　-3 になります。

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>