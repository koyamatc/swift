---
title: Swift
layout: post
postTitle:  Computed Properties
categories: properties
---

クラス、定義体、列挙には、　計算プロパティを定義できます。
これは、実際に値を保存するものではありません。
間接的に、ほかのプロパティや値を取得したりセットする、　ゲッタとセッタを提供するものです。

{% highlight c %}
struct Point {
    var x = 0.0, y = 0.0
}
struct Size {
    var width = 0.0, height = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
    var center: Point {
    get {
        let centerX = origin.x + (size.width / 2)
        let centerY = origin.y + (size.height / 2)
        return Point(x: centerX, y: centerY)
    }
    set(newCenter) {
        origin.x = newCenter.x - (size.width / 2)
        origin.y = newCenter.y - (size.height / 2)
    }
    }
}
var square = Rect(origin: Point(x: 0.0, y: 0.0),
    size: Size(width: 10.0, height: 10.0))
let initialSquareCenter = square.center
square.center = Point(x: 15.0, y: 15.0)
println("square.origin is now at (\(square.origin.x), \(square.origin.y))")
// prints "square.origin is now at (10.0, 10.0)"
{% endhighlight %}
<br>

この例では、幾何図形を扱う３つの構造体を定義しています。
<br>
Point は　(x, y) 座標をカプセル化しています。
<br>
Size は、width と　height をカプセル化しています。
<br>
Rect は、　origin point と　size で　長方形を定義しています。
<br>
Rect 構造体は、　計算プロパティ center も提供しています。
Rect構造体の center 位置は、基点とsizeから決定されます、
したがって、明示的に　Point値として、　centerの点を保存する必要はない。
その代り、Rectは、計算プロパティcenter用に、　カスタム　ゲッタとセッタ　を定義して、
あたかも実際に保存されたプロパティであるかのように、長方形の center を扱えるのです。
<br>
Rect型の変数 square が作られています。
square変数は、基点(0,0)、width と　height は、10　で初期化されています。
<br>
square変数の center プロパティは、　(square.center)　でアクセスでき、
これが、　center のための　ゲッタです。
存在している値を返すのではなく、
ゲッタの計算結果として　square の center を表す新しい　Point型を返します。
この場合、ゲッタは (5,5) を返します。
<br>
次に、　centerプロパティは、　(15,15)　にセットされています、
これは　square の位置を移動させます。
centerプロパティをセットするということは、　center用のセッタを呼び出すことです、
それは、基点のストアード・プロパティ　x,y　の値を変更するので、
squareは新しい位置へ移動します。

<h3>Shorthand Setter Declaration</h3>

計算プロパティのセッタが、新しい値をセットするために名前を定義していないならば、
_newValue_　というデフォルト名が使われます。

{% highlight c %}
struct AlternativeRect {
    var origin = Point()
    var size = Size()
    var center: Point {
    get {
        let centerX = origin.x + (size.width / 2)
        let centerY = origin.y + (size.height / 2)
        return Point(x: centerX, y: centerY)
    }
    set {
        origin.x = newValue.x - (size.width / 2)
        origin.y = newValue.y - (size.height / 2)
    }
    }
}
{% endhighlight %}

<h3>Read-Only Computed Properties</h3>

セッタをはなくゲッタだけ持つ計算プロパティは、　リードオンリ計算プロパティです。
リードオンリ計算プロパティは値を返すが、異なる値を設定することはできません。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    計算プロパティは、リードオンリ計算プロパティも含め　変数プロパティとして宣言しなくてはならない。
    なぜなら、その値は固定されていないからです。
</div>

getキーワードとその波カッコを外すことで、リードオンリ計算プロパティの宣言を簡単にできます。
{% highlight c %}
struct Cuboid {
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double {
    return width * height * depth
    }
}
let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
println("the volume of fourByFiveByTwo is \(fourByFiveByTwo.volume)")
// prints "the volume of fourByFiveByTwo is 40.0"
{% endhighlight %}

この例では新しい構造体 Cuboid を定義していて、　
プロパティ　width, height, depth を持ち、３次元の箱を表しています。
この構造体は　volume というリードオンリ計算プロパティをもち、
その時の体積を計算し返します。
