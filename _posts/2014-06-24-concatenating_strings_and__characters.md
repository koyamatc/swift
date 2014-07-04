---
title: Swift
layout: post
postTitle:  Concatenating Strings and Characters
categories: strings_characters
---

文字列と文字を結合する
==============================

文字列と文字を、　加算演算子　(+) でつなぎ合わせて新しい文字列を作ることができます。 

{% highlight c linenos %}
let string1 = "hello"
let string2 = " there"
let character1: Character = "!"
let character2: Character = "?"
 
let stringPlusCharacter = string1 + character1        // equals "hello!"
let stringPlusString = string1 + string2              // equals "hello there"
let characterPlusString = character1 + string1        // equals "!hello"
let characterPlusCharacter = character1 + character2  // equals "!?"
{% endhighlight %}

すでにある文字列変数に、文字列や文字を加算代入演算子 (+=) で付け加えることができます。

{% highlight c linenos %}
var instruction = "look over"
instruction += string2
// instruction now equals "look over there"
 
var welcome = "good morning"
welcome += character1
// welcome now equals "good morning!"
{% endhighlight %}

<div class="panel">
	<div class="panel-header">NOTE</div>
	すでにある文字変数に、文字列や文字を付け加えることはできません。
	文字値は１文字しか持つことができないからです。
</div>