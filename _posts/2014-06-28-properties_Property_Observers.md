---
title: Swift
layout: post
postTitle:  Property Observers
categories: properties
---

_プロパティ オブザーバ_ は、　プロパティ値の変更を監視し、それがあったことを知らせます。
プロパティ値がセットされるたびに（たとえ同じ値がセットされたとしても）　
プロパティ　オブザーバは呼び出されます。

ストアド・プロパティに　プロパティ・オブザーバを追加できるし、継承したプロパティに対しても追加できる。

willSet は、値が保存される直前に呼び出されます。

didSet は、新しい値が保存された直後に呼び出されます。

willSetオブザーバを実装したなら、それは定数パラメータとして新しいプロパティ値に渡されます。
willSetを実装するときに、このパラメータに名前を付けることができます。
もし名前を指定せずカッコも書かないときには、デフォルトパラメータ名　newValueで
そのパラメータを利用できます。

同様に、　didSetオブザーバを実装すれば、　古いプロパティ値を持った定数パラメータに渡されます。
パラメータに名前を付けられるし、さまなければ、　デフォルトプロパティ名　oldValue を使えます。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    willSet と　didSetオブザーバは、プロパティが最初に初期化されるときには呼ばれません。
    初期化処理の外側でプロパティ値がセットされるときだけ呼ばれます。
</div>

{% highlight c %}
class StepCounter {
    var totalSteps: Int = 0 {
    willSet(newTotalSteps) {
        println("About to set totalSteps to \(newTotalSteps)")
    }
    didSet {
        if totalSteps > oldValue  {
            println("Added \(totalSteps - oldValue) steps")
        }
    }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// About to set totalSteps to 200
// Added 200 steps
stepCounter.totalSteps = 360
// About to set totalSteps to 360
// Added 160 steps
stepCounter.totalSteps = 896
// About to set totalSteps to 896
// Added 536 steps
{% endhighlight %}

StepCounterクラスでは、整数型のプロパティ　totalSteps が宣言されちいます。
totalStepsは、　willSet と didSet オブザーバを持つストアド・プロパティです。
<br>
totalStepsに対する　willSet と didSetオブザーバは、　
プロパティtotalSteps に値が代入されるたびに呼ばれます（値が現在値と同じであっても）。
<br>
この例では、　willSetオブザーバは　これからセッされる新しい値のために 
カスタム　パラメータ名に　newTotalSteps を使います。
<br>
didSetオブザーバは、　totalStepsの値が更新された後に呼ばれます。
didSetオブザーバは、前の値に対してカスタムパラメータ名を提供していないので、
デフォルト名である　oldValue が使われます。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    didSetオブザーバ内のプロパティに値を代入すると、
    その新しい値は、以前の値を置き換えます。
</div>