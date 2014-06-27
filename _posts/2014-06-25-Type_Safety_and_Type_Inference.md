---
title: Swift
layout: post
postTitle: Type Safety and Type Inference
categories: basics
---

## 型の安全性　と　型の推測

Swift は、　_type safe_ な言語です。　文字列を整数型に入れることはできません。

Swift　は、コンパイル時に型チェックを行い、間違いを早い段階で見つけることができます。

型チェックの機能は、異なる型の値を扱う際にエラーを防ぐのに役立ちます。
しかし、宣言するすべての定数と変数に型を指定する必要はありません。
型を指定しなくても、　Swift は、 _型推論_ を使い、適した型を導き出します。
 
型推論は、初期値を与えて定数や変数を先天するときに特に便利です。

{% highlight c %}
let meaningOfLife = 42
// meaningOfLife は　Int型と推測されます
{% endhighlight %}
同様に、浮動小数点数の型を指定することもありません。Swiftは倍精度数(Double)を推測します
{% highlight c %}
let pi = 3.14159
// pi is inferred to be of type Double
{% endhighlight %}
Swift は常に、Float ではなく　Double を選択します。

整数と浮動小数点数が混ざっているときは、　Double が選択されます。
{% highlight c %}
let anotherPi = 3 + 0.14159
// anotherPi もDoubleと推測されます
{% endhighlight %}
