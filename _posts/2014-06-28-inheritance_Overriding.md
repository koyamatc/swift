---
title: Swift
layout: post
postTitle:  Overriding
categories: inheritance
---

A subclass can provide its own custom implementation of an instance method, class method, instance property, or subscript that it would otherwise inherit from a superclass. This is known as overriding.

To override a characteristic that would otherwise be inherited, you prefix your overriding definition with the override keyword. Doing so clarifies that you intend to provide an override and have not provided a matching definition by mistake. Overriding by accident can cause unexpected behavior, and any overrides without the override keyword are diagnosed as an error when your code is compiled.

The override keyword also prompts the Swift compiler to check that your overriding class’s superclass (or one of its parents) has a declaration that matches the one you provided for the override. This check ensures that your overriding definition is correct.

Accessing Superclass Methods, Properties, and Subscripts

When you provide a method, property, or subscript override for a subclass, it is sometimes useful to use the existing superclass implementation as part of your override. For example, you can refine the behavior of that existing implementation or store a modified value in an existing inherited variable.

Where this is appropriate, you access the superclass version of a method, property, or subscript by using the super prefix:

An overridden method named someMethod can call the superclass version of someMethod by calling super.someMethod() within the overriding method implementation.
An overridden property called someProperty can access the superclass version of someProperty as super.someProperty within the overriding getter or setter implementation.
An overridden subscript for someIndex can access the superclass version of the same subscript as super[someIndex] from within the overriding subscript implementation.
Overriding Methods

You can override an inherited instance or class method to provide a tailored or alternative implementation of the method within your subclass.

The following example defines a new subclass of Vehicle called Car, which overrides the description method it inherits from Vehicle:

class Car: Vehicle {
    var speed: Double = 0.0
    init() {
        super.init()
        maxPassengers = 5
        numberOfWheels = 4
    }
    override func description() -> String {
        return super.description() + "; "
            + "traveling at \(speed) mph"
    }
}
Car declares a new stored Double property called speed. This property defaults to 0.0, meaning “zero miles per hour”. Car also has a custom initializer, which sets the maximum number of passengers to 5, and the default number of wheels to 4.

Car overrides its inherited description method by providing a method with the same declaration as the description method from Vehicle. The overriding method definition is prefixed with the override keyword.

Rather than providing a completely custom implementation of description, the overriding method actually starts by calling super.description to retrieve the description provided by Vehicle. It then appends some additional information about the car’s current speed.

If you create a new instance of Car, and print the output of its description method, you can see that the description has indeed changed:

let car = Car()
println("Car: \(car.description())")
// Car: 4 wheels; up to 5 passengers; traveling at 0.0 mph
Overriding Properties

You can override an inherited instance or class property to provide your own custom getter and setter for that property, or to add property observers to enable the overriding property to observe when the underlying property value changes.

Overriding Property Getters and Setters

You can provide a custom getter (and setter, if appropriate) to override any inherited property, regardless of whether the inherited property is implemented as a stored or computed property at its source. The stored or computed nature of an inherited property is not known by a subclass—it only knows that the inherited property has a certain name and type. You must always state both the name and the type of the property you are overriding, to enable the compiler to check that your override matches a superclass property with the same name and type.

You can present an inherited read-only property as a read-write property by providing both a getter and a setter in your subclass property override. You cannot, however, present an inherited read-write property as a read-only property.

NOTE

If you provide a setter as part of a property override, you must also provide a getter for that override. If you don’t want to modify the inherited property’s value within the overriding getter, you can simply pass through the inherited value by returning super.someProperty from the getter, as in the SpeedLimitedCar example below.

The following example defines a new class called SpeedLimitedCar, which is a subclass of Car. The SpeedLimitedCar class represents a car that has been fitted with a speed-limiting device, which prevents the car from traveling faster than 40mph. You implement this limitation by overriding the inherited speed property:

class SpeedLimitedCar: Car {
    override var speed: Double  {
    get {
        return super.speed
    }
    set {
        super.speed = min(newValue, 40.0)
    }
    }
}
Whenever you set the speed property of a SpeedLimitedCar instance, the property’s setter implementation checks the new value and limits it to 40mph. It does this by setting the underlying speed property of its superclass to be the smaller of newValue and 40.0. The smaller of these two values is determined by passing them to the min function, which is a global function provided by the Swift standard library. The min function takes two or more values and returns the smallest one of those values.

If you try to set the speed property of a SpeedLimitedCar instance to more than 40mph, and then print the output of its description method, you see that the speed has been limited:

let limitedCar = SpeedLimitedCar()
limitedCar.speed = 60.0
println("SpeedLimitedCar: \(limitedCar.description())")
// SpeedLimitedCar: 4 wheels; up to 5 passengers; traveling at 40.0 mph
Overriding Property Observers

You can use property overriding to add property observers to an inherited property. This enables you to be notified when the value of the inherited property changes, regardless of how that property was originally implemented. For more information on property observers, see Property Observers.

NOTE

You cannot add property observers to inherited constant stored properties or inherited read-only computed properties. The value of these properties cannot be set, and so it is not appropriate to provide a willSet or didSet implementation as part of an override.

Note also that you cannot provide both an overriding setter and an overriding property observer. If you want to observe changes to a property’s value, and you are already providing a custom setter for that property, you can simply observe any value changes from within the custom setter.

The following example defines a new class called AutomaticCar, which is a subclass of Car. The AutomaticCar class represents a car with an automatic gearbox, which automatically selects an appropriate gear to use based on the current speed. AutomaticCar also provides a custom description method to print the current gear.

class AutomaticCar: Car {
    var gear = 1
    override var speed: Double {
    didSet {
        gear = Int(speed / 10.0) + 1
    }
    }
    override func description() -> String {
        return super.description() + " in gear \(gear)"
    }
}
Whenever you set the speed property of an AutomaticCar instance, the property’s didSet observer automatically sets the gear property to an appropriate choice of gear for the new speed. Specifically, the property observer chooses a gear which is the new speed value divided by 10, rounded down to the nearest integer, plus 1. A speed of 10.0 produces a gear of 1, and a speed of 35.0 produces a gear of 4:

let automatic = AutomaticCar()
automatic.speed = 35.0
println("AutomaticCar: \(automatic.description())")
// AutomaticCar: 4 wheels; up to 5 passengers; traveling at 35.0 mph in gear 4