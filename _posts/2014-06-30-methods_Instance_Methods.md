---
title: Swift
layout: post
postTitle:  Instance Methods
categories: methods
---

インスタンス　メソッドは、　クラス、構造体、列挙に属する関数です。
インスタンスの機能を提供しています、
インスタンス　プロパティにアクセスし変更する方法を提供し、
インスタンスの目的に関連する機能を提供します。
インスタンス　メソッドの構文は、関数と同じです。

{% highlight c %}
class Counter {
    var count = 0
    func increment() {
        count++
    }
    func incrementBy(amount: Int) {
        count += amount
    }
    func reset() {
        count = 0
    }
}
{% endhighlight %}

Counterクラスは３つのインスタンス　メソッドを定義しています

+ increment は　counter の値を１増やします
+ incrementBy(amount: Int) は　整数値amount分　counterの値を増やします
+ reset は、　counterの値をゼロにリセットします

Counterクラスには変数プロパティcountが、現在のcounter値を保持するために宣言されています。

{% highlight c %}
let counter = Counter()
// the initial counter value is 0
counter.increment()
// the counter's value is now 1
counter.incrementBy(5)
// the counter's value is now 6
counter.reset()
// the counter's value is now 0
{% endhighlight %}

###Local and External Parameter Names for Methods

関数のパラメータは、関数内部で使うローカル名と、関数を呼ぶときに使う外部名を持てます。
メソッドのパラメータ名についても同じです。
しかし、関数とメソッドではローカル名と外部名とでは、デフォルトの動作が異なります。


Swiftのメソッドは　Objective-C　のものとよく似ています。
Swiftのメソッド名で前置詞　with, for, by などを使っているものは、決まってそのメソッドの１番目のパラメータを参照しています。
前置詞を使うことで、そのメソッドを呼ぶときに文章のように読めます。

Swiftはデフォルトで、メソッドの１番目のパラメータ名をローカルパラ名とし、
２番目とそれ以後のパラメータ名をローカルパラメータ名、外部パラメータ名どちらとも扱います。

{% highlight c %}
class Counter {
    var count: Int = 0
    func incrementBy(amount: Int, numberOfTimes: Int) {
        count += amount * numberOfTimes
    }
}
{% endhighlight %}

この　incrementBy メソッドは、２つのパラメータ　amount と numberOfTimes を持ちます。
デフォルトでは、　Swiftは　amount をローカル名としてだけ扱います、
しかし numberOfTimes を、ローカル、外部名どちらとしても扱います。

{% highlight c %}
let counter = Counter()
counter.incrementBy(5, numberOfTimes: 3)
// counter value is now 15
{% endhighlight %}

１番目の引数に対する外部パラメータ名を定義する必要はありません、
なぜなら、関数名 incrementBy により、その役割は明らかだからです。
しかし、２番目の引数は、メソッドが呼ばれたときに、その役割がはっきりするように、
外部パラメータ名を使うのです。

このデフォルトの動作は、　numberOfTimes パラメータの前に　ハッシュ記号(#)を書いた時のようになります

{% highlight c %}
func incrementBy(amount: Int, #numberOfTimes: Int) {
    count += amount * numberOfTimes
}
{% endhighlight %}


###Modifying External Parameter Name Behavior for Methods

時には、メソッドの第１パラメータに外部パラメータ名を付けることは役立ちます。
明示的に名前を付けることもできますし、ハッシュ記号を第１パラメータ名の前に付けて
ローカル名を外部名として使うことができます。

逆に、２番目、それ以降のパラメータに外部名を与えたくない場合は、
そのパラメータの外部パラメータ名として　アンダースコア(_)を明示してデフォルトの動作をオーバーライドします。

###The self Property

すべてのインスタンスは、　self というプロパティを暗黙の裡に持っています。
selfは、インスタンスそれ自身です。
インスタンスのメソッド内で、自分自身を参照するときに、　self　を使います。

increment メソッドはこのように書けます

{% highlight c %}
func increment() {
    self.count++
}
{% endhighlight %}

self を書くことは多くはないでしょう。
selfを明示的に書かないのであれば、　
Swiftは仮定します、メソッド内の分かっているプロパティやメソッド名を使えば、
それは現在のインスタンスのプロパティやメソッドを参照しているのだと。
この仮定により、Counter のインスタンス　メソッド内で　self.count ではなく count が使われているのです。

例外は、インスタンスメソッドのパラメータ名と同じ、そのインスタンスのプロパティ名があるときです。
この場合、パラメータ名が優先されるので、プロパティを参照するためには、特別な方法が必要です。
パラメータ名かプロパティ名かを区別するために、暗黙のselfを使います。

ここでは、メソッドパラメータ　ｘ　と、　インスタンス　プロパティ　x を　selfがはっきりとさせています。

{% highlight c %}
struct Point {
    var x = 0.0, y = 0.0
    func isToTheRightOfX(x: Double) -> Bool {
        return self.x > x
    }
}
let somePoint = Point(x: 4.0, y: 5.0)
if somePoint.isToTheRightOfX(1.0) {
    println("This point is to the right of the line where x == 1.0")
}
// prints "This point is to the right of the line where x == 1.0"
{% endhighlight %}

接頭語selfが無いと、　Swiftは　どちらのxも、メソッドパラメータを参照していると仮定します。

###Modifying Value Types from Within Instance Methods

構造体と列挙は　value型です。
デフォルトでは、value型のプロパティはインスタンスメソッド内からは変更できません。

しかし、特定のメソッド内で、構造体や列挙のプロパティを変更する必要がある場合、
そのメソッドの動作を変更することができます。
そのメソッドは、メソッド内から自身のプロパティを変更でき、
メソッドが行う変更は、メソッドが終了すると元の構造に書き戻される。
メソッドは、新しいインスタンスを暗黙のselfプロパティに代入することもできます、
この新しいインスタンスは、メソッドが終了すると既存のインスタンスを置き換えます。

mutatingキーワードを　メソッドのfuncキーワードの前に付けることで、この動作をするようにできます。

{% highlight c %}
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveByX(deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveByX(2.0, y: 3.0)
println("The point is now at (\(somePoint.x), \(somePoint.y))")
// prints "The point is now at (3.0, 4.0)"
{% endhighlight %}

Point構造体は、　mutating moveByXメソッドを定義しています。
このメソッドは、　amount分　Pointインスタンスを動かします。
このメソッドは、新しい点を返すのではなく、実際に点を修正します。
mutatingキーワードを定義に付け加えることで、プロパティを変更することが可能になります。

構造型を定数にした場合は、　mutatingメソッドを呼べません、　
定数のプロパティを変更できないからです。

{% highlight c %}
let fixedPoint = Point(x: 3.0, y: 3.0)
fixedPoint.moveByX(2.0, y: 3.0)
// this will report an error
{% endhighlight %}

###Assigning to self Within a Mutating Method

mutating メソッドは、　暗黙のselfプロパティに新しいインスタンスを代入することができます。

{% highlight c %}
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveByX(deltaX: Double, y deltaY: Double) {
        self = Point(x: x + deltaX, y: y + deltaY)
    }
}
{% endhighlight %}

列挙の　mutatingメソッドは、同じ列挙内の異なるメンバになるように
暗黙のselfパラメタをセットできます。
{% highlight c %}
enum TriStateSwitch {
    case Off, Low, High
    mutating func next() {
        switch self {
        case Off:
            self = Low
        case Low:
            self = High
        case High:
            self = Off
        }
    }
}
var ovenLight = TriStateSwitch.Low
ovenLight.next()
// ovenLight is now equal to .High
ovenLight.next()
// ovenLight is now equal to .Off
{% endhighlight %}

この例では、スイッチの３つの状態を列挙しています。
スイッチは３つの異なる電気の状態(Off, Low,High)を、　nextメソッドが呼ばれるたびに移り変わります。
