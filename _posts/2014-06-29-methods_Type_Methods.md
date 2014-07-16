---
title: Swift
layout: post
postTitle:  Type Methods
categories: methods
---

インスタンス　メソッドは、特定の型のインスタンス上にあるメソッドです。
型自体にあるメソッドを定義することができます。
このようなメソッドを型メソッドといいます。
型メソッドを指定するには、
クラスでは、メソッドの funcキーワードの前に、class キーワードを書きます、
構造体と列挙では、　funcキーワードの前に、static キーワードを書きます。

<div class="panel">
    <div class="panel-heading">NOTE</div>
    Objective-Cでは、タイプれべるのメソッドは、クラスにしか定義できません。
    Swiftでは、クラス、構造体、列挙とすべてに定義できます。
</div>

型メソッドは、ドット構文で呼び出します。
しかし、その型に定義した型メソッドを呼ぶのであって、型のインスタンスのメソッドをよぶのではない。
クラス someClassの型メソッドの呼び出し方です。
{% highlight c %}
class SomeClass {
    class func someTypeMethod() {
        // type method implementation goes here
    }
}
SomeClass.someTypeMethod()
{% endhighlight %}

型メソッド本体内にある、暗黙のselfプロパティは、型それ自体を参照しています、
型のインスタンスではありません。
構造体と列挙では、selfを使うことで、静的なプロパティと静的なメソッドパラメータをはっきりと区別できます。


More generally, any unqualified method and property names that you use within the body of a type method will refer to other type-level methods and properties. A type method can call another type method with the other method’s name, without needing to prefix it with the type name. Similarly, type methods on structures and enumerations can access static properties by using the static property’s name without a type name prefix.

下の例は、構造体　LevelTracker を定義し、
プレイヤの進行状況をレベルの違いやゲームのステージを通じて追跡します。
１人遊び用のゲームですが、１つの端末で、複数のプレイヤ情報を保存できます。

ゲームのレベルは、ゲーム開始時点で、レベル１を除きすべてロックされています。
プレイヤがレベルをクリアするたびに、その端末のすべてのプレイヤにそのレベルは解放されます。
LevelTracker構造体は、静的プロパティとメソッドを使い解放されたゲームのレベルを管理します。
個人プレイヤの現在のレベルも管理しています。

{% highlight c %}
struct LevelTracker {
    static var highestUnlockedLevel = 1
    static func unlockLevel(level: Int) {
        if level > highestUnlockedLevel { highestUnlockedLevel = level }
    }
    static func levelIsUnlocked(level: Int) -> Bool {
        return level <= highestUnlockedLevel
    }
    var currentLevel = 1
    mutating func advanceToLevel(level: Int) -> Bool {
        if LevelTracker.levelIsUnlocked(level) {
            currentLevel = level
            return true
        } else {
            return false
        }
    }
}
{% endhighlight %}

LevelTracker構造体は、解放された最高レベルを保持しています。
この値は、静的プロパティhighestUnlockedLevelに保存されています。

LevelTrackerはhighestUnlockedLevelプロパティを扱うために
２つの型関数を定義しています。
最初の型関数は、　unLockLevelで、
新しいレベルが解放されるとhighestUnlockedLevelを更新します。
２番目は、便利な型関数　levelIsUnlocked　で、
特定の番号のレベルが解放されているときに　trueを返します。
（これらの型メソッドは　LevelTracker.highestUnlockedLevel　と書く必要無しに
静的プロパティhighestUnlockedLevelにアクセスできます。）

staticなプロパティと型メソッドに加えて、　LevelTrackerは個人プレイヤの進捗を追跡します。
そのために、インスタンス　プロパティcurrentLevelを使い、現在プレイしているレベルを記録しています。

currentLevelプロパティを管理するために、
LevelTrackerは、インスタンス　メソッド　advanceToLevel を定義しています。
currentLeveが更新される前に、このメソッドが、要求された新しいレベルがすでに解放されているかどうかを検査します。
advanceToLevel メソッドは、　currentLevelをセットできるかどうかの論理値を返します。

下記の　Playerクラスでは、　LevelTrafker構造体が使われていて、
個々のプレイヤ進捗状況を追跡し更新しています。

{% highlight c %}
class Player {
    var tracker = LevelTracker()
    let playerName: String
    func completedLevel(level: Int) {
        LevelTracker.unlockLevel(level + 1)
        tracker.advanceToLevel(level + 1)
    }
    init(name: String) {
        playerName = name
    }
}
{% endhighlight %}

Playerクラスは、プレイヤの進捗を管理するため LevelTrackerの新しいインスタンスを生成します。　
プレイヤがレベルをクリアしたときに呼ばれるメソッド　completedLevel も提供します。
このメソッドは、すべてのプレイヤのために次のレベルを解放し、
また、プレイヤの進捗を次のレベルへと移動させます。

新しいプレイヤのために、　Playerクラスのインスタンスを作れます。
そのプレイヤがレベル１をクリアすると何が起きるか見てみましょう。

{% highlight c %}
var player = Player(name: "Argyrios")
player.completedLevel(1)
println("highest unlocked level is now \(LevelTracker.highestUnlockedLevel)")
// prints "highest unlocked level is now 2"
{% endhighlight %}

２番目のプレイヤを作り、まだ解放されていないレベルへ移動しようとします、
そのプレイヤの現在のレベルをセットする試みは失敗します。

{% highlight c %}
player = Player(name: "Beto")
if player.tracker.advanceToLevel(6) {
    println("player is now on level 6")
} else {
    println("level 6 has not yet been unlocked")
}
// prints "level 6 has not yet been unlocked"
{% endhighlight %}
