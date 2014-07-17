---
title: Swift
layout: post
postTitle:  Overriding
categories: inheritance
---

サブクラスは、スーパークラスから継承してくる代わりに、サブクラス自体で、
インスタンスメソッド、クラスメソッド、インスタンスプロパティ、添え字型を実装できます。
これを _オーバーライド_ といいます。

オーバーライドするためには、　overrideキーワードを使います。

### Accessing Superclass Methods, Properties, and Subscripts

オーバーライドして、メソッド、プロパティ、添え字型をサブクラスに提供するときに、
オーバーライドしたコードの中で、すでにあるスーパークラスに実装されているものを使うことが役に立つこともあります。

スーパークラスのメソッド、プロパティ、添え字型にアクセスするには、　接頭語 super　を使います

+ オーバーライドされたメソッド someMethod は、　この中で　スーパークラスのメソッド　someMethodを
super.someMethod()　で呼び出せます。

+ オーバーライドされたプロパティ someProperty は　
オーバーライドしているゲッタまあはセッタの実装の中で　
スーパークラスのプロパティ　somePropertyを
super.someProperty　でアクセスできます。

+ オーバーライドされた　someIndex　用の添え字型は　
オーバーライドしている添え字型の実装の中で　
スーパークラスの添え字型を　super[someIndex]でアクセスできます。

### Overriding Methods

継承した　インスタンスうやクラス　メソッドをオーバーライドできます。

次の例は、　Vehicleのサブクラス Car を定義して、　
Vehicle から継承したメソッド　description をオーバーライドしています。
{% highlight c %}
class Car: Vehicle {
    var speed: Double = 0.0
    init() {
        super.init()
        maxPassengers = 5
        numberOfWheels = 4
    }
    override func description() -> String {
        return super.description() + "; "
            + "traveling at \(speed) mph"
    }
}
{% endhighlight %}

Car で新しく宣言された　ストアドのDouble型プロパティ　speed があり初期値は　0.0　です。
カスタム　イニシャライザがあり、中で　maxPassengers が　5　に、
numberOfWheels が　4 にセットされています。

Car は、description メソッドをオーバーライドしています。

{% highlight c %}
let car = Car()
println("Car: \(car.description())")
// Car: 4 wheels; up to 5 passengers; traveling at 0.0 mph
{% endhighlight %}

<h3>Overriding Properties</h3>

継承したインスタンス　または　クラスのプロパティをオーバーライドして、
独自のセッタとゲッタを提供できます。
また、プロパティ　オブザーバを追加してそのプロパティ値が変更されたかを監視できます。

<h3>Overriding Property Getters and Setters</h3>

継承したプロパティをオーバーライドして、独自のゲッタ（必要なら　セッタ）を提供できます。
継承元のプロパティが、ストアドでも計算型でも構いません。

継承もとのプロパティが　リードオンリでも、オーバーライドしてゲッタとセッタを提供することで
リードライト型にすることができます。
しかし、元がリードライト型のプロパティをリードオンリにはできません。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    プロパティをオーバーライドして、セッタを提供するならば。
    ゲッタも提供しまければならない。
    オーバーライドしているゲッタの中で、継承したプロパティ値を変更したくないのであれば、
    superの値を返して、継承された値を渡せばいい。
</div>

{% highlight c %}
class SpeedLimitedCar: Car {
    override var speed: Double  {
    get {
        return super.speed
    }
    set {
        super.speed = min(newValue, 40.0)
    }
    }
}
{% endhighlight %}

SpeedLimitedCar インスタンスの　プロパティspeedを　40mph以上にセットしようとしても、
descriptionメソッドの出力は、　speedは制限されているように表示されます。

{% highlight c %}
let limitedCar = SpeedLimitedCar()
limitedCar.speed = 60.0
println("SpeedLimitedCar: \(limitedCar.description())")
// SpeedLimitedCar: 4 wheels; up to 5 passengers; traveling at 40.0 mph
{% endhighlight %}

<h3>Overriding Property Observers</h3>

継承されたプロパティに、オーバーライドしてプロパティ　オブザーバを追加できます。
これにより、継承されたプロパティの値が変更されると、通知を受けることができます。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    プロパティオブザーバを継承した定数ストアドプロパティや継承したリードオンリ計算プロパティに追加することはできません。なぜならこれらのプロパティ値はセットできないからです。
</div>

セッタをオーバーライドしていてプロパティオブザーバもオーバーライドすることはできません。
プロパティの値が変化したことを監視したいならば、
そのプロパティ用に独自のセッタをすでに提供していると思うので、
単に、独自のセッタで　値の変化を監視することができます。

新しいクラス　AutomatiCar を　Carのサブクラスとして定義しています。

{% highlight c %}
class AutomaticCar: Car {
    var gear = 1
    override var speed: Double {
    didSet {
        gear = Int(speed / 10.0) + 1
    }
    }
    override func description() -> String {
        return super.description() + " in gear \(gear)"
    }
}
{% endhighlight %}

AutomaticCarインスタンスのspeedプロパティに値がセットされるたびに、
そのプロパティの　didSetオブザーバが自動的にgearプロパティをセットします。
{% highlight c %}
let automatic = AutomaticCar()
automatic.speed = 35.0
println("AutomaticCar: \(automatic.description())")
// AutomaticCar: 4 wheels; up to 5 passengers; traveling at 35.0 mph in gear 4
{% endhighlight %}