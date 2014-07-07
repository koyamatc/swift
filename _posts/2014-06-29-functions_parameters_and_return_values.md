---
title: Swift
layout: post
postTitle:  Function Parameters and Return Values
categories: functions
---

### Multiple Input Parameters

{% highlight c linenos %}
func halfOpenRangeLength(start: Int, end: Int) -> Int {
    return end - start
}
println(halfOpenRangeLength(1, 10))
// prints "9"
{% endhighlight %}


<h3>Functions Without Parameters</h3>


関数は、パラメータを定義する必要はありません。

{% highlight c linenos %}
func sayHelloWorld() -> String {
    return "hello, world"
}
println(sayHelloWorld())
// prints "hello, world"
{% endhighlight %}

引数が無くても関数の後に() は必要です。

<h3>Functions Without Return Values</h3>

関数は、戻り値を定義しなくてもよい。

{% highlight c linenos %}
func sayGoodbye(personName: String) {
    println("Goodbye, \(personName)!")
}
sayGoodbye("Dave")
// prints "Goodbye, Dave!"
{% endhighlight %}

<div class="panel">
	<div class="panel-heading">NOTE</div>
	厳密にいうと、　sayGoodbye 関数は、戻り値を定義していないが、値を返しています。
	void型の特別な値を返します。　これは、空のタプルで、　() で書き表されます。
</div>

関数の戻り値を無視することができる

{% highlight c linenos %}
func printAndCount(stringToPrint: String) -> Int {
    println(stringToPrint)
    return countElements(stringToPrint)
}
func printWithoutCounting(stringToPrint: String) {
    printAndCount(stringToPrint)
}
printAndCount("hello, world")
// prints "hello, world" and returns a value of 12
printWithoutCounting("hello, world")
// prints "hello, world" but does not return a value
{% endhighlight %}

最初の関数 printAndCount　は文字列を出力します、そして 整数型で文字数を返します。
２つ目の関数　printWithoutCounting　は、最初の関数を呼びますが、その戻り値は無視します。
２つ目の関数が呼ばれるとき、最初の関数でメッセージは出力されています、が戻り値は使われていません。

<div class="panel">
	<div class="panel-heading">NOTE</div>
	戻り値を無視することはできます。値を返す関数は、常にそうします。
	戻り値の型を定義した関数は、戻り値を持たない関数から制御が降りてくることを許しません。
	これは、コンパイル時エラーとなります。
</div>

<h3>Functions with Multiple Return Values</h3>

関数の戻り値の型としてタプル型を使うことができます。

{% highlight c linenos %}
func count(string: String) -> (vowels: Int, consonants: Int, others: Int) {
    var vowels = 0, consonants = 0, others = 0
    for character in string {
        switch String(character).lowercaseString {
        case "a", "e", "i", "o", "u":
            ++vowels
        case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
        "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
            ++consonants
        default:
            ++others
        }
    }
    return (vowels, consonants, others)
}
{% endhighlight %}

この count 関数は任意の文字列の文字数を数えるのに使え、３つの名前の付いた整数型のタプルとして、
そのカウント数を取得できます。

{% highlight c linenos %}
let total = count("some arbitrary string!")
println("\(total.vowels) vowels and \(total.consonants) consonants")
// prints "6 vowels and 13 consonants"
{% endhighlight %}
