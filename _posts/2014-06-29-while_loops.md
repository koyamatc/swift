---
title: Swift
layout: post
postTitle:  While Loops
categories: control_flow
---

while loop　の　一般的な形式

{% highlight c linenos %}
while condition {
    statements
}
{% endhighlight %}

This example plays a simple game of Snakes and Ladders (also known as Chutes and Ladders):

image: ../Art/snakesAndLadders_2x.png
The rules of the game are as follows:

The board has 25 squares, and the aim is to land on or beyond square 25.
Each turn, you roll a six-sided dice and move by that number of squares, following the horizontal path indicated by the dotted arrow above.
If your turn ends at the bottom of a ladder, you move up that ladder.
If your turn ends at the head of a snake, you move down that snake.
The game board is represented by an array of Int values. Its size is based on a constant called finalSquare, which is used to initialize the array and also to check for a win condition later in the example. The board is initialized with 26 zero Int values, not 25 (one each at indices 0 through 25 inclusive):

{% highlight c linenos %}
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)
{% endhighlight %}

Some squares are then set to have more specific values for the snakes and ladders. Squares with a ladder base have a positive number to move you up the board, whereas squares with a snake head have a negative number to move you back down the board:

{% highlight c linenos %}
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
{% endhighlight %}

Square 3 contains the bottom of a ladder that moves you up to square 11. To represent this, board[03] is equal to +08, which is equivalent to an integer value of 8 (the difference between 3 and 11). The unary plus operator (+i) balances with the unary minus operator (-i), and numbers lower than 10 are padded with zeros so that all board definitions align. (Neither stylistic tweak is strictly necessary, but they lead to neater code.)

The player’s starting square is “square zero”, which is just off the bottom left corner of the board. The first dice roll always moves the player on to the board:

{% highlight c linenos %}
var square = 0
var diceRoll = 0
while square < finalSquare {
    // roll the dice
    if ++diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
    if square < board.count {
        // if we're still on the board, move up or down for a snake or a ladder
        square += board[square]
    }
}
println("Game over!")
{% endhighlight %}

This example uses a very simple approach to dice rolling. Instead of a random number generator, it starts with a diceRoll value of 0. Each time through the while loop, diceRoll is incremented with the prefix increment operator (++i), and is then checked to see if it has become too large. The return value of ++diceRoll is equal to the value of diceRoll after it is incremented. Whenever this return value equals 7, the dice roll has become too large, and is reset to a value of 1. This gives a sequence of diceRoll values that is always 1, 2, 3, 4, 5, 6, 1, 2 and so on.

After rolling the dice, the player moves forward by diceRoll squares. It’s possible that the dice roll may have moved the player beyond square 25, in which case the game is over. To cope with this scenario, the code checks that square is less than the board array’s count property before adding the value stored in board[square] onto the current square value to move the player up or down any ladders or snakes.

Had this check not been performed, board[square] might try to access a value outside the bounds of the board array, which would trigger an error. If square is now equal to 26, the code would try to check the value of board[26], which is larger than the size of the array.

The current while loop execution then ends, and the loop’s condition is checked to see if the loop should be executed again. If the player has moved on or beyond square number 25, the loop’s condition evaluates to false, and the game ends.

A while loop is appropriate in this case because the length of the game is not clear at the start of the while loop. Instead, the loop is executed until a particular condition is satisfied.

### Do-While

do-while loop の一般的な形式
{% highlight c linenos %}
do {
    statements
} while condition
{% endhighlight %}

Here’s the Snakes and Ladders example again, written as a do-while loop rather than a while loop. The values of finalSquare, board, square, and diceRoll are initialized in exactly the same way as with a while loop:

{% highlight c linenos %}
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0
{% endhighlight %}

In this version of the game, the first action in the loop is to check for a ladder or a snake. No ladder on the board takes the player straight to square 25, and so it is not possible to win the game by moving up a ladder. Therefore, it is safe to check for a snake or a ladder as the first action in the loop.

At the start of the game, the player is on “square zero”. board[0] always equals 0, and has no effect:

{% highlight c linenos %}
do {
    // move up or down for a snake or ladder
    square += board[square]
    // roll the dice
    if ++diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
} while square < finalSquare
println("Game over!")
{% endhighlight %}

After the code checks for snakes and ladders, the dice is rolled, and the player is moved forward by diceRoll squares. The current loop execution then ends.

The loop’s condition (while square < finalSquare) is the same as before, but this time it is not evaluated until the end of the first run through the loop. The structure of the do-while loop is better suited to this game than the while loop in the previous example. In the do-while loop above, square += board[square] is always executed immediately after the loop’s while condition confirms that square is still on the board. This behavior removes the need for the array bounds check seen in the earlier version of the game.
