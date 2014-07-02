---
title: Swift
layout: post
postTitle:  Concatenating Strings and Characters
categories: strings_characters
---

文字列と文字を結合する
==============================

文字列と文字の値は and Character values can be added together (or concatenated) with the addition operator (+) to create a new String value:

let string1 = "hello"
let string2 = " there"
let character1: Character = "!"
let character2: Character = "?"
 
let stringPlusCharacter = string1 + character1        // equals "hello!"
let stringPlusString = string1 + string2              // equals "hello there"
let characterPlusString = character1 + string1        // equals "!hello"
let characterPlusCharacter = character1 + character2  // equals "!?"
You can also append a String or Character value to an existing String variable with the addition assignment operator (+=):

var instruction = "look over"
instruction += string2
// instruction now equals "look over there"
 
var welcome = "good morning"
welcome += character1
// welcome now equals "good morning!"
NOTE

You can’t append a String or Character to an existing Character variable, because a Character value must contain a single character only.