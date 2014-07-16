---
title: Swift
layout: post
postTitle:  Preventing Overrides
categories: inheritance
---

You can prevent a method, property, or subscript from being overridden by marking it as final. Do this by writing the @final attribute before its introducer keyword (such as @final var, @final func, @final class func, and @final subscript).

Any attempts to override a final method, property, or subscript in a subclass are reported as a compile-time error. Methods, properties or subscripts that you add to a class in an extension can also be marked as final within the extension’s definition.

You can mark an entire class as final by writing the @final attribute before the class keyword in its class definition (@final class). Any attempts to subclass a final class will be reported as a compile-time error.