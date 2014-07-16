---
title: Swift
layout: post
postTitle:  Defining a Base Class
categories: inheritance
---

他のクラスから継承をしていないクラスのことを基底クラスという。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    Swiftのクラスは、共通の基底クラスからの継承をしていない。
    スーパークラスを指定しないで定義したクラスは、自動的に基底クラスとなる。
</div>

基底クラス　Vehicleを定義。
すべてのvehicleに共通なプロパティ　numberOfWheels と　maxPassengers を宣言している。
２つのプロパティはメソッドdescriptionで使われている。

{% highlight c %}
class Vehicle {
    var numberOfWheels: Int
    var maxPassengers: Int
    func description() -> String {
        return "\(numberOfWheels) wheels; up to \(maxPassengers) passengers"
    }
    init() {
        numberOfWheels = 0
        maxPassengers = 1
    }
}
{% endhighlight %}

Vehicleクラスは、プロパティに値をセットするイニシャライザを定義している。

インスタンスを作成するためにイニシャライザを使います。
イニシャライザは、新しいインスタンスを使えるように準備し、
インスタンスのすべてのプロパティに、有効な初期値が与えられていることを保証します。

initキーワードを使って書かれた、もっともシンプルな形です。
{% highlight c %}
init() {
    // perform some initialization here
}
{% endhighlight %}

Vehicleインスタンスを作成します。
{% highlight c %}
let someVehicle = Vehicle()
{% endhighlight %}

Vehicleのイニシャライザは、任意の乗り物のために、
プロパティの初期値をセットしています(numberOfWheels = 0 and maxPassengers = 1)

Vehicleクラスは、任意の乗り物用に、共通の性質を定義していますが、
それ自体そのまま使うことはほとんどありません。
