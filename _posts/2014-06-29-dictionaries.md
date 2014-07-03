---
title: Swift
layout: post
postTitle:  Dictionaries
categories: collection_types
---

## ディクショナリ

ディクショナリは、　同じ型の値を複数個保持できる入れ物です。
各値はユニークなキーと関連づいていて、そのキーでもってディクショナリ内の値を探すことができます。　項目には特定の順番はありません。

Swift　のディクショナリは、キーと値の型を指定できます。

Swift　のディクショナリの型は、 Dictionary&lt;KeyType, ValueType&gt; と書けます。

唯一の制限は KyeType は　ハッシュ可能でなければならないということです。つまり、　その keyType で、　ユニークな値を表すことができる必要があるということです。

Swift　の基本の型　(String, Int, Double, and Bool)　は　ハッシュ可能です。 

### Dictionary Literals

ディクショナリを初期化するのに、　ディクショナリ・リテラルを使えます。
ディクショナリ・リテラルは、　key-value ペア　で書く簡単な方法です。

key-value ペアは キーと値の組合せです。 ディクショナリ・リテラルでは、　各々の key と value の間は
コロンで区切られます。 key-value ペアは。　カンマで区切られ、全体を　([]) で囲います。　
{% highlight c %}
[key 1: value 1, key 2: value 2, key 3: value 3]

var airports: Dictionary<String, String> = ["TYO": "Tokyo", "DUB": "Dublin"]

var airports = ["TYO": "Tokyo", "DUB": "Dublin"]
// 型は書かなくてもよい　型推測が行われます
{% endhighlight %}


### Accessing and Modifying a Dictionary

ディクショナリの項目数は count プロパティで
{% highlight c linenos %}
println("The dictionary of airports contains \(airports.count) items.")
// prints "The dictionary of airports contains 2 items."
{% endhighlight %}

指標を使って新し項目を追加する
{% highlight c linenos %}
airports["LHR"] = "London"
// the airports dictionary now contains 3 items
{% endhighlight %}


キーを使って値を変更する
{% highlight c linenos %}
airports["LHR"] = "London Heathrow"
// the value for "LHR" has been changed to "London Heathrow"
{% endhighlight %}

ディクショナリの updateValue(forKey:) メソッドで値をセットまたは更新する。

updateValue(forKey:) メソッドは、更新前の古い値を返します。 
これで、更新が行われたかどうかを検査できます。

updateValue(forKey:) メソッドが返す型は、　ディクショナリの型のオプショナルです。

ディクショナリの型が　String ならば、　String? が帰ります。

キーが存在していれば、　更新前の古い値が返り、　キーが無ければ　nil が返ります。

{% highlight c linenos %}
if let oldValue = airports.updateValue("Dublin International", forKey: "DUB") {
    println("The old value for DUB was \(oldValue).")
}
// prints "The old value for DUB was Dublin."
{% endhighlight %}


指標を使って、値を取り出す。　そのキーに対する値が存在していれば、その値が返り、そうでなければ　nil　が返ります。
{% highlight c linenos %}
if let airportName = airports["DUB"] {
    println("The name of the airport is \(airportName).")
} else {
    println("That airport is not in the airports dictionary.")
}
// prints "The name of the airport is Dublin International."
{% endhighlight %}


key-value ペアを　ディクショナリから取り除くには、　キーに対して、　nil を代入する。
{% highlight c linenos %}
airports["APL"] = "Apple International"
// "Apple International" is not the real airport for APL, so delete it
airports["APL"] = nil
// APL has now been removed from the dictionary
{% endhighlight %}

removeValueForKey　メソッドで　取り除く

取り除けたら、その取り除いた値が戻り、　できなければ　nil が戻ります。
{% highlight c linenos %}
if let removedValue = airports.removeValueForKey("DUB") {
    println("The removed airport's name is \(removedValue).")
} else {
    println("The airports dictionary does not contain a value for DUB.")
}
// prints "The removed airport's name is Dublin International."
{% endhighlight %}

### Iterating Over a Dictionary

for-in loop で、ディクショナリの個々の要素に順番にアクセス。

項目は　(key, value) タプルとして戻ります。
{% highlight c linenos %}
for (airportCode, airportName) in airports {
    println("\(airportCode): \(airportName)")
}
// TYO: Tokyo
// LHR: London Heathrow
{% endhighlight %}

keys と　values プロパティにアクセスして、　ディクショナリのキーと値の集まりを取り出せます。
{% highlight c linenos %}
for airportCode in airports.keys {
    println("Airport code: \(airportCode)")
}
// Airport code: TYO
// Airport code: LHR
 
for airportName in airports.values {
    println("Airport name: \(airportName)")
}
// Airport name: Tokyo
// Airport name: London Heathrow
{% endhighlight %}


ディクショナリのキーや値の集まりを使って、　配列を初期化できます。
{% highlight c linenos %}
let airportCodes = Array(airports.keys)
// airportCodes is ["TYO", "LHR"]
 
let airportNames = Array(airports.values)
// airportNames is ["Tokyo", "London Heathrow"]
{% endhighlight %}


###Creating an Empty Dictionary

空のディクショナリを作る

{% highlight c linenos %}
var namesOfIntegers = Dictionary<Int, String>()
// namesOfIntegers is an empty Dictionary<Int, String>

namesOfIntegers[16] = "sixteen"
// namesOfIntegers now contains 1 key-value pair
namesOfIntegers = [:]
// namesOfIntegers is once again an empty dictionary of type Int, String
{% endhighlight %}
