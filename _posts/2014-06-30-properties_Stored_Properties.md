---
title: Swift
layout: post
postTitle:  Stored Properties
categories: properties
---

ストアード・プロパティは、定数または変数で、クラスや構造体のインスタンスの内部に保存されているものです。

ストアード・プロパティは初期値を設定できます。

{% highlight c %}
struct FixedLengthRange {
    var firstValue: Int
    let length: Int
}
var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)
// the range represents integer values 0, 1, and 2
rangeOfThreeItems.firstValue = 6
// the range now represents integer values 6, 7, and 8
{% endhighlight %}

インスタンス　FixedLengthRange　には、　
変数ストアード・プロパティ　firstValue と定数ストアード・プロパティの　length　があります。
length は新しい　range が作成されると初期化され、定数プロパティなのでそれ以後変更できません。

<h3>Stored Properties of Constant Structure Instances</h3>

構造体のインスタンスを生成して、そのインスタンスを定数に代入すると、
そのインスタンスのプロパティを変数として定義していても変更することはできません。

{% highlight c %}
let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
// this range represents integer values 0, 1, 2, and 3
rangeOfFourItems.firstValue = 6
// this will report an error, even though firstValue is a variable property
{% endhighlight %}

ここれは、　構造体が、　value型のためです。
value型のインスタンスが、定数として指定されるとそのプロパティすべてが定数となります。

参照型であるクラスは、同じではありません。
参照型のインスタンスを定数に代入しても、そのインスタンスの変数プロパティは変更できます。

<h3>Lazy Stored Properties</h3>

レイジー・ストアード・プロパティはは、そのプロパティが最初に使われるまで値が計算されないプロパティです。
@lazy属性を宣言の前に書くことで指定できます。

<div class="panel">
	<div class="panel-heading">NOTE</div>
	レイジー・プロパティは、変数として宣言しなくてはいけません、
	なぜなら、インスタンスの初期化が完了するまでは、初期値は取得されなくてもかまいません。
	しかし、定数プロパティは、初期化が完了する前に値を持っていなければなりません、
	したがって、　定数はレイジーとして宣言できません。
</div>


The example below uses a lazy stored property to avoid unnecessary initialization of a complex class. This example defines two classes called DataImporter and DataManager, neither of which is shown in full:

{% highlight c %}
class DataImporter {
    /*
    DataImporter is a class to import data from an external file.
    The class is assumed to take a non-trivial amount of time to initialize.
    */
    var fileName = "data.txt"
    // the DataImporter class would provide data importing functionality here
}
 
class DataManager {
    @lazy var importer = DataImporter()
    var data = [String]()
    // the DataManager class would provide data management functionality here
}
 
let manager = DataManager()
manager.data += "Some data"
manager.data += "Some more data"
// the DataImporter instance for the importer property has not yet been created
{% endhighlight %}
The DataManager class has a stored property called data, which is initialized with a new, empty array of String values. Although the rest of its functionality is not shown, the purpose of this DataManager class is to manage and provide access to this array of String data.

Part of the functionality of the DataManager class is the ability to import data from a file. This functionality is provided by the DataImporter class, which is assumed to take a non-trivial amount of time to initialize. This might be because a DataImporter instance needs to open a file and read its contents into memory when the DataImporter instance is initialized.

It is possible for a DataManager instance to manage its data without ever importing data from a file, so there is no need to create a new DataImporter instance when the DataManager itself is created. Instead, it makes more sense to create the DataImporter instance if and when it is first used.

Because it is marked with the @lazy attribute, the DataImporter instance for the importer property is only created when the importer property is first accessed, such as when its fileName property is queried:

{% highlight c %}
println(manager.importer.fileName)
// the DataImporter instance for the importer property has now been created
// prints "data.txt"
{% endhighlight %}

###Stored Properties and Instance Variables

Objective-C を扱ったことがあるなら、クラスのインスタンスの機能の一部として値を保存したり
参照する方法がほかにもあります。
プロパティに加えて、インスタンス変数というを使えます。

Swift は、プロパティ宣言を１つにまとめ、１か所で定義できるようにしています。
	