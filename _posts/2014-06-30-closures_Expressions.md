---
title: Swift
layout: post
postTitle:  Closure Expressions
categories: closures
---

クロージャは、コードを書く中で、受け渡したり使ったりできる機能を含んでいるコードのブロックです。
クロージャは、クロージャのコンテキスト内に定義された定数と変数への参照を受け取り、保持することができます。
これは、それらの定数と変数を閉じ込める（closing over）として知られています。
それゆえ、名前を"クロージャ" といいます。 

グローバルや入れ子の関数は、クロージャの特別な場合です。クロージャは３つの形式をとります。

+ グローバル関数は名前は持ているが、どの値もキャプチャしないクロージャです。
+ 入れ子の関数は、名前があり、入れ子の関数を内包する関数から値を受け取るクロージャです。
+ クロージャの表現は、周囲のコンテキストから値を受け取れる簡単な文法で書かれた名前のないクロージャです・

Swiftのクロージャは、最適化された短く、迷いのない構文でわかりやすく書くことができます。
最適化には以下を含みます

+ Inferring parameter and return value types from context
+ Implicit returns from single-expression closures
+ Shorthand argument names
+ Trailing closure syntax

### Closure Expressions

入れ子の関数は、より大きな関数の１部分として自己完結したコードブロックを定義し、名前を付けることができる便利な方法です。　しかし時には、関数みたいな構造で、完全な宣言はいらず、名前もなく、短く書けるものがあると役に立ちます。
特に、ほかの関数を引数として受け取る関数を扱うときです。

クロージャ表現は、短く埋め込み型クロージャを書く方法です。
クロージャ表現は、明確さやその意図を失うことのないもっともシンプルな形式でクロージャを書くための最適な文法を提供しています。

### The Sort Function

Swiftの標準ライブラリは　sortという関数を提供しています、　
それはあなたが書いた並び換えクロージャの出力結果をもとに、
わかっている型の配列の値を並び替えます。
並び替えのプロセスを完了するたびに、　
sort 関数はもとの配列と同じ型、同じサイズの新しい配列を正しく並び替えて返します。

下記のクロージャの書き方の例では、　sort関数を使い、文字列の配列値を逆順に並べ替えをしています。

{% highlight c %}
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
{% endhighlight %}

sort 関数は２つ引数をとります

+ 型のわかっている配列
+ クロージャ : 配列の要素と同じ型の２つの引数をとり、　並び替えがされたときに、１番目にあった値が２番目の値の前か後ろかを表す真偽値を返します。１番目の値が２番目の値の前にあれば　true を返し、そうでなければ　false をかえします。

例は、文字列値の配列を並び替えます。
並び替えクロージャは、(String, String) -> Bool　型の関数である必要があります。

１つは、　正しい型の普通の関数を書き、それを　sort 関数の２番目の引数とする方法です。

{% highlight c linenos %}
func backwards(s1: String, s2: String) -> Bool {
    return s1 > s2
}
var reversed = sort(names, backwards)
// reversed is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
{% endhighlight %}

１番目の文字列 s1 が、　２番目の文字列 s2 より大きければ、　backwards 関数は true を返します。
これは、 ならび換えられた配列の中で、　s1 は　s2 の前にあるということです。　

しかし、これは　(a > b)　ということだけを表す関数を長々と書いています。
ここでは、クロージャ表現文法を使って、　埋め込み型の並び替えクロージャを書くほうがいいでしょう。　　

### Closure Expression Syntax

クロージャ表現の文法は　下記の一般形式をしています

{% highlight c %}
{ (parameters) -> return type in
    statements
}
{% endhighlight %}

クロージャ書くときに、　定数パラメータ、変数パラメータ、 inout パラメータを使えます。
初期値は与えられません。
可変長パラメータは、　名前を付けて、パラメータリストの最後に置けば使えます。
タプルも引数の型として、また返り値の型として使えます。

下記は　backwards 関数の　クロージャ表現です。

{% highlight c %}
reversed = sort(names, { (s1: String, s2: String) -> Bool in
    return s1 > s2
    })
{% endhighlight %}

パラメータと戻り値の型宣言は　埋め込みクロージャと　backwards 関数とで一致しています。
どちらも　(s1: String, s2: String) -> Bool　です。
異なるのは、埋め込みクロージャでは、　パラメータと戻り値の型は　波カッコ{} の中に書かれていることです。

クロージャ本体は　in キーワードで始まります。
このキーワードは、クロージャのパラメータと戻り値の型宣言が終わり、クロージャ本体が始まることを表します。

クロージャ本体が短ければ、１行で書くこともできます。

{% highlight c %}
reversed = sort(names, { (s1: String, s2: String) -> Bool in return s1 > s2 } )
{% endhighlight %}

sort関数の呼び出し方は前と同じです。
関数の引数全体はカッコで挟まれています。
ただし、引数の１つは埋め込みクロージャです。

### Inferring Type From Context

並び替えクロージャは関数に引数として渡されているので、
Swiftは、　sort関数の２番目のパラメータから、クロージャのパラメータの型と戻り値の型を推測します。
このパラメータは(String, String) -> Bool型の関数であると期待します。
このことは、　クロージャを定義するときに、　String、 String、 と Bool 型を書く必要はないという意味です。
すべての型は推測されるので、戻り値の矢印(->) やパラメータ名を囲うカッコも取り去ることができます。

{% highlight c %}
reversed = sort(names, { s1, s2 in return s1 > s2 } )
{% endhighlight %}

埋め込みクロージャという書き方で書いたクロージャを関数に渡せは、常にパラメータと戻り値の型は推測されます。
結果として、埋め込みクロージャを必要十分な形式で書くだけです。

言うまでもなく、型を明確に指定することもできますし、コードの読み手がわかりずらくなることを避けられます。


### Implicit Returns from Single-Expression Closures

単一表現のクロージャは、宣言から　return キーワードを外すことによって結果を返すことができます。

{% highlight c %}
reversed = sort(names, { s1, s2 in s1 > s2 } )
{% endhighlight %}

sort 関数の第２引数である関数型から、クロージャが返す値が論理値であることは明らかです。
クロージャ本体には、　論理値を返す単一表現　(s1 > s2)があるので、
不明瞭さはなく　キーワード　return を省くことができます。 

### Shorthand Argument Names

Swift は埋め込みクロージャに短縮引数名を自動的に与えます。
$0, $1, $2　... という名前でクロージャの引数を参照できます 

クロージャを書くときに、短縮引数名を使うときは、　クロージャの引数リストを省くことができます。
短縮引数名の番号と型は、期待された関数の型から推測されます。
in キーワードも省けます、なぜならクロージャは本体のみから成り立っているからです。

{% highlight c %}
reversed = sort(names, { $0 > $1 } )
{% endhighlight %}

$0 と $1 は　クロージャの　１番目と２番目の文字列引数を参照しています。

### Operator Functions

上記のクロージャの書き方を短くする方法があります。
Swift の文字列型は、２つの文字列型のパラメータをとり、真偽値を返す関数として　（>） を
文字列型特有に実装しています。
これは sort 関数の２番目のパラメータとして必要な関数型にぴったりです。
それゆえ、　> 演算子を受け渡すと、　Swiftは、文字列特有の実装された機能を使いたいのだと推測します。

{% highlight c %}
reversed = sort(names, >)
{% endhighlight %}
