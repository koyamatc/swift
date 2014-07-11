---
title: Swift
layout: post
postTitle:  Associated Values
categories: enumerations
---

前のセクションで、列挙型のメンバはどのように定義され、型を持った値となるかを見てきました。
Planet.Earth に対して、　定数や変数を設定できます、し後々その値をチェックできます。
もし、メンバの値とともに、ほかの型の関連した値を保持できれば役立つことがあります。
これは、メンバの値と一緒にカスタム情報を追加して持つことができるということですし、
コードを書く上で、そのメンバを使うたびにこの情報を変えることができる地うことです。

指定された型の関連値を保存するように　Swiftの列挙型は定義できます、
そして、列挙型のメンバそれぞれ異なる型の値にすることができます。

たとえば、商品追跡システムには、２つの異なるバーコード体系が必要であると仮定します。
ある商品には、１次元バーコードが　UPC-A　形式で張られています。

その他の商品には、２次元バーコードが、　QRコード形式ではらっれています。

商品追跡システムでは、　どちらのバーコードをも保存できれば便利でしょう。

Swift　では、　どちらの型でも使えるように　このように定義できます
{% highlight c %}
enum Barcode {
    case UPCA(Int, Int, Int, Int)
    case QRCode(String)
}
{% endhighlight %}

Barcodeという列挙型を定義し、
それは、(Int, Int, Int, Int)型の関連値を持つ UPCA の値　または
文字列型の関連値を持つQRCodeの値を持つことができるということです。

この定義は、実際の整数値や文字列値を表しているのではなく、
ただ、Barcode.UPCA か Barcode.QRCode　と一致する　Barcode型の定数と変数が保持できる
関連値の型を定義しているだけです。

どちらかの型を使い、　新しいバーコードを作れます。

{% highlight c %}
var productBarcode = Barcode.UPCA(8, 85909, 51226, 3)
{% endhighlight %}

新しい変数　productBarcode を作り、　
関連したタプル値　(8, 85909, 51226, 3)　を持つ　Barcode.UPCA　を代入しています。

同じ製品に異なるバーコード型を代入することができる

{% highlight c %}
productBarcode = .QRCode("ABCDEFGHIJKLMNOP")
{% endhighlight %}

この時点で、　元の整数値である　Barcode.UPCA　は、文字列の　Barcode.QRCode　で置き換わります。
Barcode型の定数と変数は、.UPCA または .QRCode　を関連値とともに保存できます。
しかし、どちらか１つの型のみが保存できます。

異なるバーコードの型を、　switch文を使いチェックできます。
この際に、関連値各々を　let を付けて定数として抜き取るか、　var を付けて変数として抜き取ります。

{% highlight c %}
switch productBarcode {
case .UPCA(let numberSystem, let manufacturer, let product, let check):
    println("UPC-A: \(numberSystem), \(manufacturer), \(product), \(check).")
case .QRCode(let productCode):
    println("QR code: \(productCode).")
}
// prints "QR code: ABCDEFGHIJKLMNOP."
{% endhighlight %}

抜き出される関連値がすべて定数のとき、またはすべて変数のとき、
メンバ名の前に、　let または　var を　１つだけ置くことができる

{% highlight c %}
switch productBarcode {
case let .UPCA(numberSystem, manufacturer, product, check):
    println("UPC-A: \(numberSystem), \(manufacturer), \(product), \(check).")
case let .QRCode(productCode):
    println("QR code: \(productCode).")
}
// prints "QR code: ABCDEFGHIJKLMNOP."
{% endhighlight %}