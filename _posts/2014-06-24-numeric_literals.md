---
title: Swift
layout: post
postTitle: Numeric Literals
categories: basics
---

## 数字リテラル

### 整数リテラル

10進数　-- そのまま
	
2進数  -- 先頭に　0ｂ
	
8進数  -- 先頭に 0o
	
16進数 -- 先頭に 0x

{% highlight c%}
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 in binary notation
let octalInteger = 0o21           // 17 in octal notation
let hexadecimalInteger = 0x11     // 17 in hexadecimal notation
{% endhighlight %}

### 浮動小数点数リテラル

10進数　-- そのまま

16進数 -- 先頭に 0x

{% math %}
1.25e2 = 1.25 × 10^{2},  or = 125.0.
{% endmath %}
{% math %}
1.25e_{-2} = 1.25 × 10^{-2},  or =0.0125.
{% endmath %}


{% math %}
0xFp2 = 15 × 2^{2}, or =60.0.
{% endmath %}
{% math %}
0xFp_{-2} = 15 × 2^{-2}, or =3.75.
{% endmath %}

{% highlight c %}
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
{% endhighlight %}

数字リテラルは、読みやすくするために、フォーマットをして書くことができます。
{% highlight c %}
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
{% endhighlight %}

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>