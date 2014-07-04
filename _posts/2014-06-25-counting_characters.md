---
title: Swift
layout: post
postTitle:  Counting Characters
categories: strings_characters
---

文字を数える
==============================

文字列内の文字数を取得するには、グローバル関数　 _countElements_  をその文字列を引数として呼び出します 
{% highlight c linenos %}
let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
println("unusualMenagerie has \(countElements(unusualMenagerie)) characters")
// prints "unusualMenagerie has 40 characters"
{% endhighlight %}

<div class="panel">
	<div class="panel-heading">NOTE</div>
Different Unicode characters and different representations of the same Unicode character can require different amounts of memory to store. Because of this, characters in Swift do not each take up the same amount of memory within a string’s representation. As a result, the length of a string cannot be calculated without iterating through the string to consider each of its characters in turn. If you are working with particularly long string values, be aware that the countElements function must iterate over the characters within a string in order to calculate an accurate character count for that string.
</div>



Note also that the character count returned by countElements is not always the same as the length property of an NSString that contains the same characters. The length of an NSString is based on the number of 16-bit code units within the string’s UTF-16 representation and not the number of Unicode characters within the string. To reflect this fact, the length property from NSString is called utf16count when it is accessed on a Swift String value.