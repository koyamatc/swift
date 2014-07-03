---
title: Swift
layout: post
postTitle:  Mutability of Collections
categories: collection_types
---

## コレクションの可変性

配列とディクショナリは１つのコレクションに複数の値を保持します。　
変数として、配列またはディクショナリを作成すれば、　そのコレクションは変更可能です。
コレクションが作成された後に、項目の追加や削除をしてサイズの変更ができるということです。
反対に、定数として作成した場合には、変更不可となり、サイズを変更することはできません。

ディクショナリにとって変更不可とは、一度セットされた内容を変更することはでき無いということです。

配列にとっての変更不可とは、ディクショナリとは少し違います。
サイズの変更はできませんが、存在している指標に対して新しい値をセットすることは許されます。