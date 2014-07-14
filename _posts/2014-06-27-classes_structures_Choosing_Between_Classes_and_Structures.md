---
title: Swift
layout: post
postTitle:  Choosing Between Classes and Structures
categories: classes_and_structures
---

データ構造を定義する際に、クラスにするか構造体にするか決めなければなりません。

構造体を作るのであれば

+ The structure’s primary purpose is to encapsulate a few relatively simple data values.
+ It is reasonable to expect that the encapsulated values will be copied rather than referenced when you assign or pass around an instance of that structure.
+ Any properties stored by the structure are themselves value types, which would also be expected to be copied rather than referenced.
+ The structure does not need to inherit properties or behavior from another existing type.

Examples of good candidates for structures include:

+ The size of a geometric shape, perhaps encapsulating a width property and a height property, both of type Double.
+A way to refer to ranges within a series, perhaps encapsulating a start property and a length property, both of type Int.
+A point in a 3D coordinate system, perhaps encapsulating x, y and z properties, each of type Double.

その他の場合は、クラスを定義しましょう。実際、ほとんどのカスタムデータ構造は、構造体ではなくクラスとなります。
