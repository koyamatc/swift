---
title: Swift
layout: post
postTitle:  Capturing Values
categories: closures
---

クロージャは、それが定義されている周囲から定数や変数を受け取れます。
クロージャは、そのクロージャ内で定数や変数の値を参照したり変更したりできます。
それはたとえ定数や変数を定義した元のスコープがすでに存在していないとしても。

Swiftで最もシンプルなクロージャの形は、入れ子の関数です。
入れ子の関数は、外側の関数の引数や、外側の関数で定義された定数、変数を受け取れます。

{% highlight c %}
func makeIncrementor(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementor() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementor
}
{% endhighlight %}

makeIncrementor の戻り値の型は　() -> Int　ですから、　関数を戻すという意味です。
makeIncrementor　が戻す関数にはパラメータは無く、呼ばれるたびに整数値を返します。

makeIncrementor 関数は、整数型変数　runningTotl を定義して　incrementorの戻り値であるの途中の合計を保存しています。
この変数は0で初期化されています。

makeIncrementor 関数は、１つの整数パラメータを持ち、
その外部名は　forIncrement　で、ローカル名は amount です。

makeIncrementor　は、　入れ子の関数 incrementor を定義し、実際の加算を行います。
incrementor 関数は　runningTotal に　amount を加え、その結果を返すだけです。

この入れ子の関数だけを見てみると、　普通ではありません。

{% highlight c %}
func incrementor() -> Int {
    runningTotal += amount
    return runningTotal
}
{% endhighlight %}

incrementor 関数にはパラメータがありません、
しかし、関数の中から　runningTotal と amount を参照しています。

amount を変更していないので、　incrementorは　amount に保存された値のコピーを受け取り、保持しています。
このあ値は　新しい incrementor関数が存在している間保持されます。

しかし、 runningTotal 変数は、incrementorが呼ばれるたびに変更されているので、
初期値のコピーではなく、　現在の　runningTotal変数への参照を受け取ります。
参照を受け取ることは、　makeIncrementorへの呼び出しが終了したときに、
runningTotalが消滅しないことを確約します、
つまり、incrementor関数が次に呼ばれたときにも　runningTotla変数を使い続けることができるのです。

動作を見てみましょう
{% highlight c %}
let incrementByTen = makeIncrementor(forIncrement: 10)
{% endhighlight %}

この例では、　
定数　incrementByTen　に、呼ばれるたびに　10　を　runningTotal変数に加える関数　incrementor を参照させています。

{% highlight c %}
incrementByTen()
// returns a value of 10
incrementByTen()
// returns a value of 20
incrementByTen()
// returns a value of 30
{% endhighlight %}

ほかのincrementor を作るならば、そのincrementorは、
新しい、別の runningTotal変数への参照を　incrementor自体が持ちます。
下記の例の　incrementBySeven　は　新しい runningTotal変数を参照していて、
incrementByTenで参照されている　runningtotal とは繋がっていません。

{% highlight c %}
let incrementBySeven = makeIncrementor(forIncrement: 7)
incrementBySeven()
// returns a value of 7
incrementByTen()
// returns a value of 40
{% endhighlight %}
