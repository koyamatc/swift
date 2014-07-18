---
title: Swift
layout: post
postTitle:  Customizing Initialization
categories: initialization
---

初期化処理をカスタマイズできます

### Initialization Parameters

イニシャライザの定義時に、パラメータを渡せます。

構造体Celsiusには、２つのイニシャライザがあり、
異なる温度体系の値をとり新しい構造体のインスタンスを初期化します。
{% highlight c %}
struct Celsius {
    var temperatureInCelsius: Double = 0.0
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
}
let boilingPointOfWater = Celsius(fromFahrenheit: 212.0)
// boilingPointOfWater.temperatureInCelsius is 100.0
let freezingPointOfWater = Celsius(fromKelvin: 273.15)
// freezingPointOfWater.temperatureInCelsius is 0.0
{% endhighlight %}

<h3>Local and External Parameter Names</h3>

関数とメソッドパラメータと同様に、初期化パラメータは、ローカル名と外部名を持ちます。

しかし、イニシャライザには、固有の名前はありません。なので、イニシャライザのパラメータの名前と型は、どのイニシャライザを呼ぶのか重要な役割を持っています。そのため　Swiftは、外部名を付けなかった場合に自動的に外部名をすべてのパラメータに与えます。自動的付けられた外部名は、ローカル名と同じになります。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    もしパラメータに外部名を付けたくなければ、　明示的な外部名としてアンダースコア(_)を書きます。
</div>

３つの定数プロパティを持つ構造体　Color です。
{% highlight c %}
struct Color {
    let red = 0.0, green = 0.0, blue = 0.0
    init(red: Double, green: Double, blue: Double) {
        self.red   = red
        self.green = green
        self.blue  = blue
    }
}
{% endhighlight %}

Colorインスタンスを生成するときには、３つの構成要素の外部名を使ってイニシャライザを呼びます。

{% highlight c %}
let magenta = Color(red: 1.0, green: 0.0, blue: 1.0)
{% endhighlight %}

注　外部名を使わずにイニシャライザを呼ぶことはできません。
外部名が定義されているなら、使わなければならない。

{% highlight c %}
let veryGreen = Color(0.0, 1.0, 0.0)
// this reports a compile-time error - external names are required
{% endhighlight %}

### Optional Property Types

初期化処理中に値の決められないストアドプロパティがあるとき、
または、のちに、値が無い状態が起こる場合、
そのプロパティは、オプショナル型として宣言します。
オプショナル型のプロパティは自動的に　nil で初期化されます。

{% highlight c %}
class SurveyQuestion {
    var text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        println(text)
    }
}
let cheeseQuestion = SurveyQuestion(text: "Do you like cheese?")
cheeseQuestion.ask()
// prints "Do you like cheese?"
cheeseQuestion.response = "Yes, I do like cheese."
{% endhighlight %}

質問に対する答えは、最初わかりません、そのため　response プロパティは、オプショナル型で宣言しています。

<h3>Modifying Constant Properties During Initialization</h3>

初期化処理中ならば、定数プロパティのあ値を変更できます。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    クラスインスタンスでは、定数プロパティは初期化処理中にだけ変更ができます。
    サブクラスによる変更はできません。。
</div>

textプロパティは定数ですが、クラスイニシャライザの中で値をセットできます。

{% highlight c %}
class SurveyQuestion {
    let text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        println(text)
    }
}
let beetsQuestion = SurveyQuestion(text: "How about beets?")
beetsQuestion.ask()
// prints "How about beets?"
beetsQuestion.response = "I also like beets. (But not with cheese.)
{% endhighlight %}