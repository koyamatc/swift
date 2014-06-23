---
title: Swift
layout: post
postTitle: Constants & Variables
categories: basics
---

## 定数と変数の宣言
{% highlight c linenos %}
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0 
{% endhighlight %}

__let__ 定数の宣言 

__var__ 変数の宣言

複数の定数、複数の変数を1行で、カンマで区切って宣言できます
{% highlight c %}
var x = 0.0, y = 0.0, z = 0.0
{% endhighlight %}

## 型指定　(Type Annotations)
宣言した定数、変数に型を指定します

定数名または変数名の後にコロンを置き、空白を1つ、そのあとに型名を指定します
{% highlight c %}
var welcomeMessage: String 
{% endhighlight %}

変数 welcomeMessage は、エラーなく文字列をセットできます
{% highlight c %}
welcomeMessage = "Hello" 
{% endhighlight %}

## 定数と変数の名前付け
定数と変数の名前は、Unicode文字を含め、ほとんどの文字を使うことができます
{% highlight c linenos %}
let π = 3.14159
let ハロー = "ハローワールド"
let □□　= "dogcow"
{% endhighlight %}

名前として使えない文字は、数学の記号、矢印、個人的に使用している（または無効な）Unicodeの点、線、ボックスを描くための文字。先頭が数字の名前。ほかの位置なら数字はつかえます

型付きで宣言した定数と変数は同じ名前で再度宣言することはできません
また、異なる型の値を保存することもできません。

定数を変数に、変数を定数に変えることもできません。

変数は、互換性のある型の値で変更できます
{% highlight c linenos %}
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome is now "Bonjour!"
{% endhighlight %}

変数とは異なり、定数は1度値がセットされると、その値を変更できません。下記はコンパイル時にエラーとなります
{% highlight c linenos %}
let languageName = "Swift"
languageName = "Swift++"
// this is a compile-time error - languageName cannot be changed
{% endhighlight %}

## 定数と変数を出力する
{% highlight c linenos %}
println(friendlyWelcome)
// prints "Bonjour!"
println("This is a string")
// prints "This is a string"
{% endhighlight %}

*println* 関数は改行コードを付けて出力します

*print* 関数は改行コード無しで出力します

*println*　関数は、定数と変数の現在の値を含めて出力することができます

出力したい定数または変数を()で囲み、カッコの先頭に バックスラッシュ\ を置きエスケープします
{% highlight c linenos %}
println("The current value of friendlyWelcome is \(friendlyWelcome)")
// prints "The current value of friendlyWelcome is Bonjour!"
{% endhighlight %}


## コメント

#### 行コメント (//)
// this is a comment

#### 複数行コメント
You can also write multiline comments, which start with a forward-slash followed by an asterisk (/*) and end with an asterisk followed by a forward-slash (*/):

/* this is also a comment,
but written over multiple lines */
Unlike multiline comments in C, multiline comments in Swift can be nested inside other multiline comments. You write nested comments by starting a multiline comment block and then starting a second multiline comment within the first block. The second block is then closed, followed by the first block:

/* this is the start of the first multiline comment
/* this is the second, nested multiline comment */
this is the end of the first multiline comment */
Nested multiline comments enable you to comment out large blocks of code quickly and easily, even if the code already contains multiline comments.

Semicolons