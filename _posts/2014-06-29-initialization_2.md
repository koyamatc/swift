---
title: Swift
layout: post
postTitle:  Customizing Initialization
categories: initialization
---

You can customize the initialization process with input parameters and optional property types, or by modifying constant properties during initialization, as described in the following sections.

Initialization Parameters

You can provide initialization parameters as part of an initializer’s definition, to define the types and names of values that customize the initialization process. Initialization parameters have the same capabilities and syntax as function and method parameters.

The following example defines a structure called Celsius, which stores temperatures expressed in the Celsius scale. The Celsius structure implements two custom initializers called init(fromFahrenheit:) and init(fromKelvin:), which initialize a new instance of the structure with a value from a different temperature scale:

struct Celsius {
    var temperatureInCelsius: Double = 0.0
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
}
let boilingPointOfWater = Celsius(fromFahrenheit: 212.0)
// boilingPointOfWater.temperatureInCelsius is 100.0
let freezingPointOfWater = Celsius(fromKelvin: 273.15)
// freezingPointOfWater.temperatureInCelsius is 0.0
The first initializer has a single initialization parameter with an external name of fromFahrenheit and a local name of fahrenheit. The second initializer has a single initialization parameter with an external name of fromKelvin and a local name of kelvin. Both initializers convert their single argument into a value in the Celsius scale and store this value in a property called temperatureInCelsius.

Local and External Parameter Names

As with function and method parameters, initialization parameters can have both a local name for use within the initializer’s body and an external name for use when calling the initializer.

However, initializers do not have an identifying function name before their parentheses in the way that functions and methods do. Therefore, the names and types of an initializer’s parameters play a particularly important role in identifying which initializer should be called. Because of this, Swift provides an automatic external name for every parameter in an initializer if you don’t provide an external name yourself. This automatic external name is the same as the local name, as if you had written a hash symbol before every initialization parameter.

NOTE

If you do not want to provide an external name for a parameter in an initializer, provide an underscore (_) as an explicit external name for that parameter to override the default behavior described above.

The following example defines a structure called Color, with three constant properties called red, green, and blue. These properties store a value between 0.0 and 1.0 to indicate the amount of red, green, and blue in the color.

Color provides an initializer with three appropriately named parameters of type Double:

struct Color {
    let red = 0.0, green = 0.0, blue = 0.0
    init(red: Double, green: Double, blue: Double) {
        self.red   = red
        self.green = green
        self.blue  = blue
    }
}
Whenever you create a new Color instance, you call its initializer using external names for each of the three color components:

let magenta = Color(red: 1.0, green: 0.0, blue: 1.0)
Note that it is not possible to call this initializer without using the external names. External names must always be used in an intializer if they are defined, and omitting them is a compile-time error:

let veryGreen = Color(0.0, 1.0, 0.0)
// this reports a compile-time error - external names are required
Optional Property Types

If your custom type has a stored property that is logically allowed to have “no value”—perhaps because its value cannot be set during initialization, or because it is allowed to have “no value” at some later point—declare the property with an optional type. Properties of optional type are automatically initialized with a value of nil, indicating that the property is deliberately intended to have “no value yet” during initialization.

The following example defines a class called SurveyQuestion, with an optional String property called response:

class SurveyQuestion {
    var text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        println(text)
    }
}
let cheeseQuestion = SurveyQuestion(text: "Do you like cheese?")
cheeseQuestion.ask()
// prints "Do you like cheese?"
cheeseQuestion.response = "Yes, I do like cheese."
The response to a survey question cannot be known until it is asked, and so the response property is declared with a type of String?, or “optional String”. It is automatically assigned a default value of nil, meaning “no string yet”, when a new instance of SurveyQuestion is initialized.

Modifying Constant Properties During Initialization

You can modify the value of a constant property at any point during initialization, as long as it is set to a definite value by the time initialization finishes.

NOTE

For class instances, a constant property can only be modified during initialization by the class that introduces it. It cannot be modified by a subclass.

You can revise the SurveyQuestion example from above to use a constant property rather than a variable property for the text property of the question, to indicate that the question does not change once an instance of SurveyQuestion is created. Even though the text property is now a constant, it can still be set within the class’s initializer:

class SurveyQuestion {
    let text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        println(text)
    }
}
let beetsQuestion = SurveyQuestion(text: "How about beets?")
beetsQuestion.ask()
// prints "How about beets?"
beetsQuestion.response = "I also like beets. (But not with cheese.)