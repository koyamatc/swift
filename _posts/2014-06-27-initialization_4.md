---
title: Swift
layout: post
postTitle:  Initializer Delegation for Value Types
categories: initialization
---

イニシャライザは、別のイニシャライザを呼び出して、インスタンスの初期化の１部分を実行することができます。
この処理を、イニシャライザ委譲といい、複数のイニシャライザに同じコードを記述するのを避けられます。

イニシャライザ委譲はどのように働くのか、どのような委譲の形式が許可されるのかというルールは、
値型とクラス型で異なります。
値型（構造体と列挙型）は継承をサポートしませんので、イニシャライザ委譲は比較的単純です。
他のイニシャライザに、自分自身を委譲するだけで済むからです。

しかし、クラスは他のクラスを継承します。
このことは、クラスは初期化中に継承したすべてのプロパティに適切な値が代入されることを保証する責任がさらにあるということです。

値型では、　カスタム・イニシャライザを書くときは、
self.init を使い、同じ値型の別のイニシャライザを参照します。

次の例では、長方形を表す　Rect構造体を定義し、　Size と Point構造体を必要としています。
{% highlight c%}
struct Size {
    var width = 0.0, height = 0.0
}
struct Point {
    var x = 0.0, y = 0.0
}
{% endhighlight %}

Rect構造体は、３つのうちの１つを使って初期化できます。

初期値ゼロで初期化された　origin と size プロパティ。

origin と　sizeを指定して。

中心点とsizeを指定して。

これらの初期化処理は構造体Rectの定義の１部分です。

{% highlight c %}
struct Rect {
    var origin = Point()
    var size = Size()
    init() {}
    init(origin: Point, size: Size) {
        self.origin = origin
        self.size = size
    }
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}
{% endhighlight %}

１番目のイニシャライザ init() は、　カスタム・イニシャライザが無いときに実行される
デフォルト・イニシャライザと機能的には同じです。
このイニシャライザには中身がありませんし、初期化処理は行いません。
このイニシャライザを呼ぶと、初期値Point(x: 0.0, y: 0.0) と Size(width: 0.0, height: 0.0)で初期化されたorigin と　sizeプロパティを持つ　Rectインスタンスが返ります。

{% highlight c %}
let basicRect = Rect()
// basicRect's origin is (0.0, 0.0) and its size is (0.0, 0.0)
{% endhighlight %}

２つ目のイニシャライザ　init(origin:size:)は、メンバワイズ・イニシャライザと機能的に同じです。
このイニシャライザは、origin と　size　の引数値をプロパティに代入するだけです。

{% highlight c%}
let originRect = Rect(origin: Point(x: 2.0, y: 2.0),
    size: Size(width: 5.0, height: 5.0))
// originRect's origin is (2.0, 2.0) and its size is (5.0, 5.0)
{% endhighlight %}

３つ目のイニシャライザ　init(center:size:)　は、少し複雑です。
まず、中心点とsize値から、origin点を計算し、
init(origin:size:)イニシャライザを呼び出し（委譲し）、
origin と　size プロパティを設定しています。

{% highlight c %}
let centerRect = Rect(center: Point(x: 4.0, y: 4.0),
    size: Size(width: 3.0, height: 3.0))
// centerRect's origin is (2.5, 2.5) and its size is (3.0, 3.0)
{% endhighlight %}
