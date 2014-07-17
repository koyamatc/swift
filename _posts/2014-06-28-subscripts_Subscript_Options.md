---
title: Swift
layout: post
postTitle:  Subscript Options
categories: subscripts
---

添え字は、入力パラメータをいくつでも受け取れます、
そのパラメータはどんな型でも構わない。
添え字は、どんな型も返すことができます。
添え字は、変数パラメータや可変長パラメータを使えます。
しかし、 in-outパラメータは使えず、初期値を与えることもできません。

クラスや構造体は必要に応じてｍ多くの添え字型を実装することができます。
複数の添え字型の定義のことを、添え字型のオーバーロードといいます。

１つのパラメータをとる添え字型が一般的ですが、複数のパラメータをとる添え字型を定義できます。
{% highlight c %}
struct Matrix {
    let rows: Int, columns: Int
    var grid: [Double]
    init(rows: Int, columns: Int) {
        self.rows = rows
        self.columns = columns
        grid = Array(count: rows * columns, repeatedValue: 0.0)
    }
    func indexIsValidForRow(row: Int, column: Int) -> Bool {
        return row >= 0 && row < rows && column >= 0 && column < columns
    }
    subscript(row: Int, column: Int) -> Double {
        get {
            assert(indexIsValidForRow(row, column: column), "Index out of range")
            return grid[(row * columns) + column]
        }
        set {
            assert(indexIsValidForRow(row, column: column), "Index out of range")
            grid[(row * columns) + column] = newValue
        }
    }
}
{% endhighlight %}

Matrixにはイニシャライザがあり、２つのパラメータ　rows と　colums　を受け取り、
初期値0.0で　rows * columns の配列を作ります。

{% highlight c %}
var matrix = Matrix(rows: 2, columns: 2)
{% endhighlight %}

２行２列の　Matrixインスタンスmatrixが生成されます。

matrixに値をセットするには
{% highlight c %}
matrix[0, 1] = 1.5
matrix[1, 0] = 3.2
{% endhighlight %}

添え字型のセッタを呼び出して、値をセットしています。

Matrixの添え字のゲッタとセッタは、添え字の行と列の値が有効であるか検査するための警告機能を持っています。
この警告機能を支援するために、　Matrixは、便利なメソッドindexIsValidForRow(_:column:)があり、与えられた行と列の値が、　matrixの範囲内に納まっているか検査できます。　
{% highlight c %}
func indexIsValidForRow(row: Int, column: Int) -> Bool {
    return row >= 0 && row < rows && column >= 0 && column < columns
}
{% endhighlight %}

An assertion is triggered if you try to access a subscript that is outside of the matrix bounds:
matrixの範囲外の添え字でアクセスしようとすると、　警告が表示されます。

{% highlight c %}
let someValue = matrix[2, 2]
// this triggers an assert, because [2, 2] is outside of the matrix bounds
{% endhighlight %}
