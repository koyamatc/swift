---
title: Swift
layout: post
postTitle:  Type Aliases
categories: basics
---

## 型エリアス

型エリアスは、既存の型に別名を与えます。

_typealias_ キーワードで型エリアスを定義します。

{% highlight c linenos %}
typealias AudioSample = UInt16
{% endhighlight %}

定義した型エリアスは、元の型名を使えるところならば、どこででも使えます。

{% highlight c linenos %}
var maxAmplitudeFound = AudioSample.min
// maxAmplitudeFound は、今は 0　です
{% endhighlight %}

AudioSample は、UInt16　のエリアスとして定義されています。　
それはエリアスなので, AudioSample.min を呼び出すことは、UInt16.min　を呼び出していることになります。
maxAmplitudeFound 変数の初期値を提供します。
