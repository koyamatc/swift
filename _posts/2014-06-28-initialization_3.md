---
title: Swift
layout: post
postTitle:  Default Initializers
categories: initialization
---

Swift は構造体または基本クラス用にデフォルト・イニシャライザを提供し、
プロパティすべての初期値を設定します。
デフォルト・イニシャライザは単に、プロパティに初期値がセットされた新しいインスタンスを生成するだけです。

ShoppingListItemクラスを定義し、
ショッピング・リストの商品の名前、数量、購入状態をカプセル化する例です。

{% highlight c %}
class ShoppingListItem {
    var name: String?
    var quantity = 1
    var purchased = false
}
var item = ShoppingListItem()
{% endhighlight %}

ShoppingListItemクラスのすべてのプッロパティは初期値を持ち、
またスーパークラスを持たない基本クラスなので、
ShoppingListItemは、プロパティに初期値がセットされた新しいインスタンスを生成する
デフォルト・イニシャライザを自動的に実装することになります。

### Memberwise Initializers for Structure Types

構造体は独自のイニシャライザを定義していなくても、自動的にメンバワイズ・イニシャライザを受けとります。
構造体のストアド・プロパティに初期値が無くてもかまいません。

メンバワイズ・イニシャライザは、新しい構造体インスタンスのメンバ・プロパティを初期化する簡単な方法です。
新しいインスタンスのプロパティへの初期値は、名前によってメンバワイズ・イニシャライザに渡すことができます。

構造体　Sizeは、　width と height の２つのプロパティを持つと定義されています。
初期値 0.0 から　Double型と推測されます。

Size 構造体は自動的に　init(width:height:)　メンバワイズ・イニシャライザを得て、
新しいSizeインスタンスを初期化するのに利用できます。

{% highlight c %}
struct Size {
    var width = 0.0, height = 0.0
}
let twoByTwo = Size(width: 2.0, height: 2.0)
{% endhighlight %}