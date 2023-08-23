---
layout: post
title:  "Swift Part Three: A multi-paradigm programming language"
date:   2023-08-01 10:00:00 +0800
categories: programming
---
<p><i>
I've come to learn that Swift supports multiple programming paradigms namely object-oriented programming (OOP), functional programming (FP), and protocol-oriented programming (POP). This makes it a highly versatile language that allows programmers to write in a variety of styles, depending on the problem at hand, or I guess a matter of personal preference and flair.
</i></p>

<p><b>Protocol-Oriented Programming</b></p>

{% highlight swift %}
protocol Movable {
    func move()
}

struct Car: Movable {
    func move() {
    print("Car is moving")
    }
}

struct Bicycle: Movable {
    func move() {
    print("Bicycle is riding")
    }
}

let car = Car()
car.move() // Outputs: Car is moving

let bike = Bicycle()
bike.move() // Outputs: Bicycle is riding
{% endhighlight swift %}

By defining a Movable protocol, both Car and Bicycle structs can adopt and provide their implementation of the move function. This demonstrates how protocols can be used to define a contract that multiple structs or classes can conform to.

<p><b>Protocol extensions</b></p> are used to add functionality to protocols. This means we don’t need to copy that functionality across many structs and classes.

{% highlight swift %}
protocol Drivable {
    var speed: Int { get set }
    func drive()
}

extension Drivable {
    func drive() {
    print("Driving at (speed) mph.")
    }
}

struct Car: Drivable {
var speed: Int
}

let car = Car(speed: 60)
car.drive() // Outputs: Driving at 60 mph.
{% endhighlight swift %}

A protocol Drivable that declares a property speed and a function drive() is defined.cA default implementation for the drive function using a protocol extension is provided, allowing any type that conforms to Drivable to use this default implementation.

<p><b>Functional Programming</b></p>
{% highlight swift %}
let numbers = [1, 2, 3, 4, 5]
let squaredNumbers = numbers.map { $0 * $0 }
print(squaredNumbers) // Outputs: [1, 4, 9, 16, 25]
{% endhighlight %}

In this example, we use Swift's higher-order function map to transform each number in the array by squaring it. Functional programming in Swift regards functions as first-class citizens, making operations like transformations more concise and expressive.

<p><b>Object-Oriented Programming</b></p>

To summarise, we use:
- POP for sharing behaviour across different types
- FP for data transformation
- OOP for complex hierarchies, inheritance and encapsulation