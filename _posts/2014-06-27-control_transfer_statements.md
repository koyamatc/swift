---
title: Swift
layout: post
postTitle:  Control Transfer Statements
categories: control_flow
---

+ continue
+ break
+ fallthrough
+ return  (Functionの項で説明)

### Continue

continue文は、　ループに、今行っている作業を止め、次の繰り返しの最初から開始せよと伝えます。

{% highlight c linenos %}
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
for character in puzzleInput {
    switch character {
    case "a", "e", "i", "o", "u", " ":
        continue
    default:
        puzzleOutput += character
    }
}
println(puzzleOutput)
// prints "grtmndsthnklk"
{% endhighlight %}


<h3>Break</h3>

break文は、 control flow 文全体の実行を即座に終了させます。

<h4>ループ文の中のBreak</h4>

break はコードの実行を即座に終了し、ループの閉じカッコ (})　の次のコードへ制御を移します。 

<h4>Switch文の中のbreak</h4>

break は、　switch 文の実行を即座に終了し　switch 文の閉じカッコ(})　の次のｺｰﾄﾞへ制御を移します。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    switch の　case の中に、コメントしか含まれていない場合は、コンパイル時エラーとなります。
    swich case を無視するには、　break 文を使う必要があります。
</div>

{% highlight c linenos %}
let numberSymbol: Character = "三"  // Simplified Chinese for the number 3
var possibleIntegerValue: Int?
switch numberSymbol {
case "1", "١", "一", "๑":
    possibleIntegerValue = 1
case "2", "٢", "二", "๒":
    possibleIntegerValue = 2
case "3", "٣", "三", "๓":
    possibleIntegerValue = 3
case "4", "٤", "四", "๔":
    possibleIntegerValue = 4
default:
    break
}
if let integerValue = possibleIntegerValue {
    println("The integer value of \(numberSymbol) is \(integerValue).")
} else {
    println("An integer value could not be found for \(numberSymbol).")
}
// prints "The integer value of 三 is 3."
{% endhighlight %}


<h3>Fallthrough</h3>

Swift の　switch 文は、次のcase には、降りてゆきません。 最初にマッチしたcase の文がが完了すると
switch 文全体が完了します。 

キーワード fallthrough を使うことで、　次のcase　または default に制御を移すことができます。

{% highlight c linenos %}
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
default:
    description += " an integer."
}
println(description)
// prints "The number 5 is a prime number, and also an integer."
{% endhighlight %}

<div class="panel">
    <div class="panel-heading">NOTE</div>
    fallthrough　キーワードは、　制御を下へ落とすだけで　case　の条件を検査しません。
</div>

<h3>ラベル</h3>
Swift の　ループやswitch文は入れ子にして複雑な制御構造を作ることができます。
そして、ループもswitch文も　break を使って、処理を終了することができます。
それゆえ、　どのループまたはどのswitchを　break文で終了させるかを明確にすることは有効です。
同様に、　複数の入れ子のループのどれを　continue させるのかを明確にすることも有効です。

このためにラベルを使います。

while の例です
{% highlight c linenos %}
label name: while condition {
    statements
}
{% endhighlight %}

{% highlight c linenos %}
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0

gameLoop: while square != finalSquare {
    if ++diceRoll == 7 { diceRoll = 1 }
    switch square + diceRoll {
    case finalSquare:
        // diceRoll will move us to the final square, so the game is over
        break gameLoop
    case let newSquare where newSquare > finalSquare:
        // diceRoll will move us beyond the final square, so roll again
        continue gameLoop
    default:
        // this is a valid move, so find out its effect
        square += diceRoll
        square += board[square]
    }
}
println("Game over!")
{% endhighlight %}
