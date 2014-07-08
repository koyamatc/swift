---
title: Swift
layout: post
postTitle:  Function Parameter Names
categories: functions
---

{% highlight c linenos %}
func someFunction(parameterName: Int) {
    // function body goes here, and can use parameterName
    // to refer to the argument value for that parameter
}
{% endhighlight %}

ここで指定されたパラメータ名は、関数内部でだけ使うことができます。　

これをローカル・パラメータ名と呼びます。

<h3>External Parameter Names</h3>

関数を呼ぶときに関数に受け渡す引数の目的を表すような名前をパラメータに付けることは有益です。

ローカル・パラメータ名に加えて、外部パラメータ名を書くことができます。

{% highlight c linenos %}
func someFunction(externalParameterName localParameterName: Int) {
    // function body goes here, and can use localParameterName
    // to refer to the argument value for that parameter
}
{% endhighlight %}

<div class="panel">
	<div class="panel-heading">NOTE</div>
	パラメータに外部パラメータ名を設定したら、関数を呼ぶときには必ず外部パラメータ名を使わなければならない
</div>

以下の関数で考えてみましょう

{% highlight c linenos %}
func join(s1: String, s2: String, joiner: String) -> String {
    return s1 + joiner + s2
}
{% endhighlight %}

この関数を呼ぶ場合に、　関数に渡される３つの文字列の目的は不明確です

{% highlight c linenos %}
join("hello", "world", ", ")
// returns "hello, world"
{% endhighlight %}

文字列値の目的を明確にするために、　join関数の引数として外部引数名を定義します

{% highlight c linenos %}
func join(string s1: String, toString s2: String, withJoiner joiner: String)
    -> String {
        return s1 + joiner + s2
}
{% endhighlight %}

この join 関数では、　
第１引数は外部名　String と　ローカル名 s1 を持ちます。
第２引数は外部名　toString と　ローカル名 s2 を持ちます。
第１引数は外部名　withJoiner と　ローカル名 joiner を持ちます。

これらの外部パラメータ名を使うことで、明確な目的をもって、関数を呼び出すことができます。　

{% highlight c linenos %}
join(string: "hello", toString: "world", withJoiner: ", ")
// returns "hello, world"
{% endhighlight %}

<div class="panel">
    <div class="panel-heading">NOTE</div>    
    関数のパラメータの使用目的がはっきりとわかる場合には、外部パラメータ名を使う必要はない
</div>

###Shorthand External Parameter Names

関数のパラメータに外部パラメータ名を付けるとき、ローカルパラメータ名に適切な名前が使われているならば、
同じ名前を２度書く必要はなく、　ハッシュ記号 # を前に付ければよい。　
Swiftは、これで、外部パラメータ名とローカルパラメータ名の両方にその名前を使うことがわかります。 

{% highlight c linenos %}
func containsCharacter(#string: String, #characterToFind: Character) -> Bool {
    for character in string {
        if character == characterToFind {
            return true
        }
    }
    return false
}
{% endhighlight %}

この関数のパラメータ名の選び方は、明確で、わかりやすい

{% highlight c linenos %}
let containsAVee = containsCharacter(string: "aardvark", characterToFind: "v")
// containsAVee equals true, because "aardvark" contains a "v"
{% endhighlight %}

<br>
<h3>Default Parameter Values</h3>

パラメータには初期値を与えることができます。
初期値を与えられた関数を呼び出すときには、パラメータを外すことができます。

<div class="panel">
    <div class="panel-heading">NOTE</div>    
    初期値を持ったパラメータは、パラメータ・リストの最後に置きましょう。
    こうすることで、初期値を持たない引数はいつも同じ順番に書くことができます。
</div>


{% highlight c linenos %}
func join(string s1: String, toString s2: String,
    withJoiner joiner: String = " ") -> String {
        return s1 + joiner + s2
}
{% endhighlight %}

join関数を呼ぶときに、　joiner に値を設定していれば、その値を使って２つの文字列を結合します

{% highlight c linenos %}
join(string: "hello", toString: "world", withJoiner: "-")
// returns "hello-world"
{% endhighlight %}

しかし、　joiner に値を設定しなければ、初期値の空白１つが使われます

{% highlight c linenos %}
join(string: "hello", toString: "world")
// returns "hello world"
{% endhighlight %}

<h3>External Names for Parameters with Default Values</h3>

ほとんどの場合、初期値を持った外部パラメータ名を設定するのは役立つでしょう。

Swiftは、　初期値を設定したローカルパラメータを定義すると
自動的に、ローカル名と同じ名前で外部パラメータ名を使えるようになります。
まるで　ハッシュ記号 # を付けたの同じようにです。

{% highlight c linenos %}
func join(s1: String, s2: String, joiner: String = " ") -> String {
    return s1 + joiner + s2
}
{% endhighlight %}

Swiftは、自動的に外部パラメータ名 joiner を提供しています。

{% highlight c linenos %}
join("hello", "world", joiner: "-")
// returns "hello-world"
{% endhighlight %}

<div class="panel">
    <div class="panel-heading">NOTE</div>    
    パラメータを定義するときに、外部名を明示する代わりに、アンダースコア _ を書くことによって、
    この動作を避けることができますが、初期値を持ったパラメータの外部名は、使ったほうがいいです
</div>

###Variadic Parameters

可変長パラメータは、特定の型の０個または複数個の値を受け取ります。
関数が呼ばれるとき、数の決まっていない入力パラメータを渡せます。
可変長パラメータは型の後に ... を書きます

可変長パラメータに渡された値は、関数内部で指定された型の配列として利用できます。

{% highlight c linenos %}
func arithmeticMean(numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// returns 3.0, which is the arithmetic mean of these five numbers
arithmeticMean(3, 8, 19)
// returns 10.0, which is the arithmetic mean of these three numbers
{% endhighlight %}

<div class="panel">
    <div class="panel-heading">NOTE</div>    
    関数は１つの可変長パラメータを持てます。
    可変長パラメータは、パラメータリストの最後に置かなければいけません、
    それは、複数のパラメータを持つ関数を呼び出すときのあいまいさを避けるためです。

    関数に初期値を設定したパラメータが１つまたはそれ以上あり、
    さらに可変長パラメータもあるときには、
    可変長パラメータは、初期値を持ったパラメータの後ろ、リストの１番最後に置きます
</div>


###Constant and Variable Parameters

関数のパラメータはデフォルトでは定数です。
ときに、パラメータが変数であると便利です。
変数パラメータも利用可能です。

パラメータ名の前に　キーワード　var を付けることで定義します。

{% highlight c linenos %}
func alignRight(var string: String, count: Int, pad: Character) -> String {
    let amountToPad = count - countElements(string)
    for _ in 1...amountToPad {
        string = pad + string
    }
    return string
}
let originalString = "hello"
let paddedString = alignRight(originalString, 10, "-")
// paddedString is equal to "-----hello"
// originalString is still equal to "hello"
{% endhighlight %}

string "hello" は string "-----hello"　に変換されています。


<div class="panel">
    <div class="panel-heading">NOTE</div>    
    変数パラメータは、関数内部でのみ利用できます。関数外部から参照することはできません。
</div>

###In-Out Parameters

変数パラメータは、関数内部でのみ変更ができます。　
関数がパラメータの値を変更して、関数呼び出しを終了した後も、変更した値を使いたいとしたら
パラメータを　in-out　パラメータとして定義します。

in-out パラメータを書くには、　inout キーワードをパラメータ定義の前に置きます。
関数に渡された　in-out パラメータは、関数内部で変更され、関数外部から変更された値を使うことができます。

in-put パラメータのために引数である変数を受け渡すだけです。
変数名の直前に&を付けて、引数である入力パラメータに渡します。
これで関数は、その値を変更できるようになります。

<div class="panel">
    <div class="panel-heading">NOTE</div>    
    in-outパラメータは初期値を持てません、
    そして、可変長パラメータは in-outパラメータになれません。
    in-out と指定したら、　var も　let も付けられません。
</div>

例です
{% highlight c linenos %}
func swapTwoInts(inout a: Int, inout b: Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
{% endhighlight %}

swapTwoInts 関数は、　a と　b　の値を交換するだけです。

この関数を呼び出すときに、パラメータ someInt と　anotherInt の前に　アンパサンド & を付けます。

{% highlight c linenos %}
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
println("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// prints "someInt is now 107, and anotherInt is now 3"
{% endhighlight %}

someInt と　anotherInt の元の値は、　関数swapTwoInts によって変更されます。

<div class="panel">
    <div class="panel-heading">NOTE</div>    
    in-outパラメータは、関数の戻り値とは同じではありません。
    上記の swapTwoints のれいでは、戻り値の型も、戻り値も定義していませんが、整数の値は変更しています。
    in-out パラメータは、関数外部へ結果を伝える１つの方法です

</div>