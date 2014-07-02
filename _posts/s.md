---
title: Swift
layout: post
postTitle:  Arithmetic Operators
categories: basicoperators
---


算術演算子
==============================

Swift は、すべての数値型に対して４つの基本の演算子を提供しています

* 加算 (+)
* 引き算 (-)
* 乗算 (*)
* 割り算 (/)

{% highlight c linenos %}
1 + 2       // equals 3
5 - 3       // equals 2
2 * 3       // equals 6
10.0 / 2.5  // equals 4.0
{% endhighlight %}
Swift の算術演算子はそのままでは値のオーバーフローを許可していません。
Swift のオーバーフロー演算子(a &+ b)　を使うことで、　オーバーフロー時の対応ができます。

加算演算子は、文字列の結合も提供しています。

{% highlight c linenos %}
"hello, " + "world"  // equals "hello, world"

let dog: Character = "犬"
let cow: Character = "牛"
let dogCow = dog + cow
// dogCow is equal to "犬牛"
{% endhighlight %}

### 剰余演算子
剰余演算子 (a % b) は、　a を　b で割った余りを計算します。

{% highlight c %}
9 % 4    // equals 1
{% endhighlight %}

a % b の答えを決めるのに、　%　演算子は下記の等式を計算して余りを求めます。

a = (b × some multiplier) + remainder

some multiplier は、 a の中に納まる b の戸数の最大値です。

9 と 4 を等式に挿入すると

9 = (4 × 2) + 1

負の数 a に対して余りを計算するときにも同じメソッドが適用されます。 

{% highlight c %}
-9 % 4   // equals -1
{% endhighlight %}

-9 と 4 を等式に入れると

-9 = (4 × -2) + -1

余りは　-1　となります。

b が負の数のとき、 b の符号は無視されます。
つまり a % b と　1 % -b は同じ結果となります。

### 浮動小数点数の余りの計算

Swift　の 剰余演算子は浮動小数点数に対しても機能します。
{% highlight c %}
8 % 2.5   // equals 0.5
{% endhighlight %}

8 割る 2.5 は　3 と、余りが　0.5


### 増減演算子

Swift は、値を　１　増やしたり減らしたりする　インクリメント演算子 (++) と デクリメント演算子 (--) を提供しています。 この演算子は、整数型、浮動小数点型の変数に使うことができます。

{% highlight c linenos %}
var i = 0
++i      // i now equals 1
{% endhighlight %}


++ と -- 記号は、変数の前にも後ろにも付けることができます。
 
+ ++　を変数の前に付けたときは、値が返される前に変数に　1　足されます。

+ ++　を変数の後ろに付けたときは、値が返された後、変数に　1　足されます。


{% highlight c linenos %}
var a = 0
let b = ++a
// a and b are now both equal to 1
let c = a++
// a is now equal to 2, but c has been set to the pre-increment value of 1
{% endhighlight %}

i++ の特別な動作を必要としないのであれば、 ++i と --i をどんな場合にも使うべきです、
なぜなら、　i　を変更して、その結果が返されるとわかるからです。

### 単項 マイナス 演算子
先頭に付けた - 記号は、　数値の符号を変換します。

{% highlight c linenos %}
let three = 3
let minusThree = -three       // minusThree equals -3
let plusThree = -minusThree   // plusThree equals 3, or "minus minus three"
{% endhighlight %}

### 単項プラス演算子

単項プラス演算子は (+) 単にその値を返します。

{% highlight c linenos %}
let minusSix = -6
let alsoMinusSix = +minusSix  // alsoMinusSix equals -6
{% endhighlight %}

単項プラス演算子は、実際何もしませんが、　
負の数に単項マイナス演算子を使うとき、
正の数に単項プラス演算子を付けて、対称性を持ったコードを書くときに使えます。
