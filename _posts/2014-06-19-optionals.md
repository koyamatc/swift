---
title: Swift
layout: post
postTitle:  Optionals
categories: basics
---

## オプショナル


値が無いかもしれない状況のときオプショナルを使います。

オプショナルは言います

値があり、それは3です

または

値はありません

たとえば、　SwiftのString型には、メソッド toInt があり、文字列を整数に変換しようとします。　
しかし、すべての文字列を整数に変換できるわけではありません。
文字列"123"は、数値123に変換できますが、"hello,world"は変換できません。

{% highlight c linenos %}
let possibleNumber = "123"
let convertedNumber = possibleNumber.toInt()
// convertedNumber は　"Int?"型、または "optional Int"型と推測されます
{% endhighlight %}
toIntメソッドは、整数ではなく、オプショナル整数を返すと失敗します。
オプショナル整数は、　Intではなく Int? 書きます。
疑問符は、値がオプショナルであることを示しています。
つまり、値は整数であるかもしれないし、値は無いかもしれないということです。

### If Statements and Forced Unwrapping

if文でオプショナルが値を持っているか、いないかがわかります。
値があれば、 true を返し、 値が無ければ、 false を返します。

オプショナルに値があることが分かれば、
オプショナルの名前の最後に感嘆符（!）を付けて、その値にアクセスすることができます。

これをオプショナル値の　forced unwrapping　といいます。
{% highlight c linenos %}
if convertedNumber {
    println("\(possibleNumber) has an integer value of \(convertedNumber!)")
} else {
    println("\(possibleNumber) could not be converted to an integer")
}
// prints "123 has an integer value of 123"
{% endhighlight %}

### Optional Binding

optional binding は、オプショナルが値を持っているかどうかを調べるのに使います。
もし持っていれば、その値を一時的に定数または変数として利用できるようにします。

optional binding は、if文やwhile文とともに使い、値をチェックし、定数まてゃ変数に取り出します。
{% highlight c linenos %}
if let constantName = someOptional {
    statements
}
{% endhighlight %}

上の possibleNumber の例を　forced unwrapping　ではなく　optional binding で書き直すと
{% highlight c linenos %}
if let actualNumber = possibleNumber.toInt() {
    println("\(possibleNumber) has an integer value of \(actualNumber)")
} else {
    println("\(possibleNumber) could not be converted to an integer")
}
// prints "123 has an integer value of 123"
{% endhighlight %}

これは

「possibleNumber.toInt　から返された　オプショナル Int　に値があるならば、　その値を新しい定数　actualNumber　にセットしなさい」

と読めます。

変換が成功すれが、　接尾語 ! を使わずに、　定数 actualNumber を利用できます。

optional bindingでは、定数も変数も使用できます。

### nil

オプショナル変数に、特別な値 _nil_ をセットして、値のない状態にすることができます。

{% highlight c linenos %}
var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value
{% endhighlight %}

#### NOTE
nil は、オプショナルではない定数、変数で使用できません。　
もし定数や変数をどうしても値のない状態に対応させるのであれば、
適したオプショナル型として宣言しなければいけません。

初期値を与えずにオプショナル定数または変数を宣言すると、自動的に nil が設定されます。
{% highlight c linenos %}
var surveyAnswer: String?
// surveyAnswer is automatically set to nil
{% endhighlight %}

### Implicitly Unwrapped Optionals

オプショナルは、　*値が無い* 定数や変数を許します。
if文で、値の存在検査ができ、存在していれば、その値に optional binding でアクセスできます。

プログラムによっては、オプショナルが必ず値を持つ場合があります、
この場合、アクセスするたびに値の存在チェックを省くほうが便利です。

このようなときにはオプショナルを、 *implicitly unwrapped optionals* として宣言します。
オプショナルにしたい型の最後に疑問符　(String?)ではなく、感嘆符　(String!)を付けます。

{% highlight c linenos %}
let possibleString: String? = "An optional string."
println(possibleString!) // 値にアクセスするには感嘆符が必要です
// prints "An optional string."
 
let assumedString: String! = "An implicitly unwrapped optional string."
println(assumedString)  // 値にアクセスするのに感嘆符は不要です
// prints "An implicitly unwrapped optional string."
{% endhighlight %}


#### NOTE

implicitly unwrapped optional にアクセスしようとして、値が無かった時には、ランタイムエラーが発生します。

implicitly unwrapped optional　を, if文で値の存在チェックをするときに、通常のオプショナルとして扱えます。

{% highlight c linenos %}
if assumedString {
    println(assumedString)
}
// prints "An implicitly unwrapped optional string."
{% endhighlight %}

implicitly unwrapped optional　を　optional bindingで使うこともできます。

{% highlight c linenos %}
if let definiteString = assumedString {
    println(definiteString)
}
// prints "An implicitly unwrapped optional string."
{% endhighlight %}

####NOTE

Implicitly unwrapped optionals は、　nil になる可能背がある場合には使ってはいけません。
その場合には、通常のオプショナル型を使い値の存在チェックをする必要があります。
