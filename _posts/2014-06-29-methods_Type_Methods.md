---
title: Swift
layout: post
postTitle:  Type Methods
categories: methods
---


Instance methods, as described above, are methods that are called on an instance of a particular type. You can also define methods that are called on the type itself. These kinds of methods are called type methods. You indicate type methods for classes by writing the keyword class before the method’s func keyword, and type methods for structures and enumerations by writing the keyword static before the method’s func keyword.

NOTE

In Objective-C, you can define type-level methods only for Objective-C classes. In Swift, you can define type-level methods for all classes, structures, and enumerations. Each type method is explicitly scoped to the type it supports.

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

型メソッド本体内にある、暗黙のselfプロパティは、型それ自体を暗誦しています、
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

In addition to its static property and type methods, LevelTracker tracks an individual player’s progress through the game. It uses an instance property called currentLevel to track the level that a player is currently playing.

To help manage the currentLevel property, LevelTracker defines an instance method called advanceToLevel. Before updating currentLevel, this method checks whether the requested new level is already unlocked. The advanceToLevel method returns a Boolean value to indicate whether or not it was actually able to set currentLevel.

The LevelTracker structure is used with the Player class, shown below, to track and update the progress of an individual player:

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

The Player class creates a new instance of LevelTracker to track that player’s progress. It also provides a method called completedLevel, which is called whenever a player completes a particular level. This method unlocks the next level for all players and updates the player’s progress to move them to the next level. (The Boolean return value of advanceToLevel is ignored, because the level is known to have been unlocked by the call to LevelTracker.unlockLevel on the previous line.)

You can create a instance of the Player class for a new player, and see what happens when the player completes level one:

{% highlight c %}
var player = Player(name: "Argyrios")
player.completedLevel(1)
println("highest unlocked level is now \(LevelTracker.highestUnlockedLevel)")
// prints "highest unlocked level is now 2"
{% endhighlight %}

If you create a second player, whom you try to move to a level that is not yet unlocked by any player in the game, the attempt to set the player’s current level fails:

{% highlight c %}
player = Player(name: "Beto")
if player.tracker.advanceToLevel(6) {
    println("player is now on level 6")
} else {
    println("level 6 has not yet been unlocked")
}
// prints "level 6 has not yet been unlocked"
{% endhighlight %}
