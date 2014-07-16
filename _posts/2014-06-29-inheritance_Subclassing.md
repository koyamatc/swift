---
title: Swift
layout: post
postTitle:  Subclassing
categories: inheritance
---

サブクラス化は、新しいクラスを既存のクラスを基にして作成する行為です。
サブクラスは既存のクラスから性質を継承し、直すことができます。
サブクラスに新たな性質を与えることもできます。

クラスがスーパークラスを持つようにするには、
{% highlight c %}
class SomeClass: SomeSuperclass {
    // class definition goes here
}
{% endhighlight %}


新しいクラスBicycleを定義し、それはVehicleの性質を継承する
{% highlight c %}
class Bicycle: Vehicle {
    init() {
        super.init()
        numberOfWheels = 2
    }
}
{% endhighlight %}

Bicycleは　Vehicleのサブクラスです。
Vehicleは　Bicycleのスーパークラスです。
新しいBicycleクラスは、Vehicleのすべての性質を引き継ぎます。
また、Bicycleクラスの必要に応じて、性質を調整したり、追加したりできます。

Bicycleクラスは、イニシャライザを定義して、適した性質になるようにセットアップしています。
Bicycleのイニシャライザは、 bicycleクラスのスーパークラスVehicleのイニシャライザである
super.init() を呼び出し、　Vehecleにより継承するすべてのプロパティは初期化されます。

<div class="panel">
	<div class="panel-heading">NOTE</div>
	Swiftでは、デフォルトで、イニシャライザは継承されません。
</div>

Vehicleにある　maxPassengers の初期値は、自転車でも正しいので変更しません。
しかし、numberOfWheelsは、正しくないので、２に置き換えています。

Vehicleのプロパティを継承するのと同様に、Bicycleはメソッドも継承します。
Bicycleのインスタンスを生成し、継承したメソッド descriptionを呼ぶことができます。
{% highlight c %}
let bicycle = Bicycle()
println("Bicycle: \(bicycle.description())")
// Bicycle: 2 wheels; up to 1 passengers
{% endhighlight %}

サブクラスはそれ自身サブクラスとなれます。
{% highlight c %}
class Tandem: Bicycle {
    init() {
        super.init()
        maxPassengers = 2
    }
}
{% endhighlight %}

<div class="panel">
	<div class="panel-heading">NOTE</div>
	サブクラスは、初期化処理において、スーパークラスの変数プロパティだけ変更することを許されています。
	スーパークラスから継承した定数プロパティは修正できません。
</div>

{% highlight c %}
let tandem = Tandem()
println("Tandem: \(tandem.description())")
// Tandem: 2 wheels; up to 2 passengers
{% endhighlight %}

descriptionメソッドは　Tandemにより継承されています。　
クラスのインスタンスメソッドはそのクラスのすべてのサブクラスによって継承されます。
