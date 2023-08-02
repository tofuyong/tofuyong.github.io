---
layout: post
title:  "Swift Part One: Swift Basics"
date:   2023-07-20 10:00:00 +0800
categories: programming
---
<p><i>
In this four-part series, I attempt to journal some cool things I learnt about Swift, the native iOS development language. I've been deployed to the mobile development team in my new role and will have to pick up Swift. My mentor at work told me that, "All languages are the same in semantics, they just differ in syntax." Really? I am frankly sceptical. Well, I am going to find out for myself. 
</i></p>
<p><i>
Having been trained in Java as my primary programming language prior, Swift, from what I've gathered so far, seems like a different ball game altogether. I am frankly feeling rather intimidated by how expressive it is, bordering on being almost too wild. It will understandably be impossible to write about every single feature of such a rich language, so I will focus on documenting features that are new or quirky. 
</i></p>
<p><i>
That also means getting up to speed with using Xcode. Goodbye for now beloved VS Code.
</i></p>
<p><i>
I am currently learning from 'Swift Apprentice - Beginning Programming with Swift' (Seventh Edition) by the raywenderlich Tutorial Team. This book was recommended to me by an iOS developer on my team. 
</i></p>


<p><b>10 Cool Things about Swift Basics</b></p>
<p><b>1. Commenting on codes</b></p>
In Swift, comments can be left alongside code using // and /* */, the latter of which span multiple lines. Nothing unique there. But what I discovered was a cool feature that permits the nesting of comments! A comment within a comment (think <i>Inception</i>) like this:

{% highlight swift %}
/* Coffee
What coffee shall I have today?
  /* Some ideas:
  - Latte
  - Long Black
  - Einspänner */
*/
{% endhighlight swift %}

Another cool feature is the triple forward slash (///) which documents a function. A quick way to do this is to highlight the function to be documented and hit Option + Command keys. Select 'add document' and Xcode will create a template for adding the documentation. Once documentation is complete, holding the Option key and clicking on function will display the documentation which is super useful.

{% highlight swift %}
/// Prepares a cup of coffee with the specified parameters.
/// - Parameters:
///   - coffeeType: The type of coffee to prepare.
///   - quantity: The number of cups of coffee to prepare.
/// - Returns: A string indicating the prepared coffee.
func prepareCoffee(coffeeType: String, quantity: Int) -> String {
    return "Prepared \(quantity) cup(s) of \(coffeeType) coffee"
}

let coffeeResult = prepareCoffee(coffeeType: "Espresso", quantity: 2)
print(coffeeResult)
{% endhighlight swift %}

<p><b>2. String Interpolation</b></p>
While string interpolation is not unique to Swift, it'll be helpful to quickly get used to its syntax as it's used frequently for creating dynamic strings by combining values with static text. 

{% highlight swift %}
let name = "Tofu"
let interest = "programming"

let message = "My name is \(name) and I enjoy \(interest)!"
print(message)
{% endhighlight swift %}

<p><b>3. Type Conversions</b></p>
Type conversions can be done in 3 ways in Swift. For instance, if I am trying to convert an Integer of 3 into a Double, I could write either of the following lines of code:

{% highlight swift %}
let doubleValue = Double(3)
let doubleValue: Double = 3
let doubleValue = 3 as Double
{% endhighlight swift %}

<p><b>4. Type Alias</b></p>
This is a pretty neat feature that allows me to create my own type, which is an alias of another type. 

{% highlight swift %}
typealias CupOfCoffee = String

func drink(coffee: CupOfCoffee) {
    print("Sipping on a delicious cup of \(coffee)!")
}

let myCoffee: CupOfCoffee = "Cappuccino"
drink(coffee: myCoffee)
{% endhighlight swift %}

This could potentially be helpful for situations where types are complex and creating an alias gives more clarity. 

<p><b>5. Toggle method</b></p>
In Swift, the .toggle() method is available on booleans (expressed as Bool). When called on a boolean variable or property, its value is toggled, or changed from true to false or vice versa.

{% highlight swift %}
var needCoffee = true
needCoffee.toggle() // toggles the value of needCoffee from 'true' to 'false'
{% endhighlight swift %}

<p><b>6. A few ways to unwrap Optionals</b></p>
Method 1: Optional Binding (if let)
Optional binding safely checks if the optional contains a value and, if so, assigns it to a new constant or variable (unwrappedCoffee) within the scope of the if-let block. If the optional is nil, then the else block will be executed.

{% highlight swift %}
let coffee: String? = nil
if let unwrappedCoffee = coffee {
  print("Drinking \(unwrappedCoffee) today!")
} else {
  print("No coffee today") 
}
{% endhighlight swift %}

Method 2: Using the guard clause (guard let)
An alternative to if let is guard let, which also unwraps optionals. The major difference between if let and guard let is that the unwrapped optional remains usable after the guard code.

{% highlight swift %}
func coffeeOrder(coffee: String?) {
    guard let coffee = coffee else {
        print("No coffee for me today.")
        return
    }
    print("I ordered a \(coffee) today.")
}

let myCoffeeToday = "flat white"
coffeeOrder(coffee: myCoffeeToday)

// Output: I ordered a flat white today.
{% endhighlight swift %}

Method 3: Forced unwrapping (!)
Forced unwrapping is the riskiest way to unwrap an optional; use it only when you are 100% sure the optional returns a value. The ! operator forcefully unwraps the optional value, assuming that it contains a value. If the optional is nil, a runtime error will occur, causing the app to crash.

{% highlight swift %}
let coffee: String? = "Cappuccino"
let unwrappedCoffee = coffee! // Using ! for forced unwrapping
print("Forced Unwrapping: \(unwrappedCoffee)") // Output: "Forced Unwrapping: Cappuccino"
{% endhighlight swift %}

Method 4: Nil coalescing operator (??)
A fancy name for something denoted by two question marks. The nil coalescing operator is a handy way to unwrap an optional. We can use it to get a value out of the optional no matter what. An example of how it can be used:

{% highlight swift %}
let coffee: String? = nil
let defaultCoffee = "Espresso"
let unwrappedCoffee = coffee ?? defaultCoffee
print("Nil Coalescing: \(unwrappedCoffee)") // Output: "Nil Coalescing: Espresso"
{% endhighlight swift %}

<p><b>7. Countable Ranges</b></p>
Countable Ranges represent a sequence of <b>countable integers</b>. There are two types of countable ranges - open and half-open. One thing to remember is that ranges must always be increasing.

{% highlight swift %}
// Countable closed range
for i in 1...5 {
  print(i) // Prints 1, 2, 3, 4, 5
}

// Countable half-open range
for j in 1..<5 {
  print(j) // Prints 1, 2, 3, 4
}
{% endhighlight swift %}

<p><b>8. Control Flow</b></p>
When it comes to control flow, Swift's for loop is less verbose than Java's.

{% highlight swift %}
// Swift For Loop
for i in 1...count {
  sum += i 
}

// Java For Loop
for (int i = 1; i <= count; i++) {
  sum += i;
}
{% endhighlight swift %}

Interestingly, Swift has a useful <b>where</b> clause that Java lacks which greatly improves how concise the code is.

{% highlight swift %}
// where clause in action in Swift
sum = 0
for row in 0..<8 where row % 2 == 1 {
  for column in 0..<8 {
    sum += row * column
  }
}
// the equivalent if written in Java
sum = 0
for row in 0..<8 {
if row % 2 == 0 {
continue
  }
  for column in 0..<8 {
    sum += row * column
  }
}
{% endhighlight swift %}

<p><b>9. Stride (from:to:by:)</b></p>
Countable ranges are limited in that they must always increase by one. The Swift stride offers much more flexibility and can be used as such:

{% highlight swift %}
// Print even numbers from 0 to 10 (inclusive)
for number in stride(from: 0, through: 10, by: 2) {
    print(number)
}

// Output: 0 2 4 6 8 10
{% endhighlight swift %}

<p><b>10. The Wildcard Underscore</b></p>
The wildcard underscore in Swift can match anything without revealing its true identity. It's used when we don't explicitly want to care about certain values and its usefulness is captured in the 3D example below.

{% highlight swift %}
let coordinates = (x: 3, y: 4, z: 5)
switch coordinates {
case (0, 0, 0):
  print("Origin")
case (_, 0, 0):
  print("On the x-axis.")
case (0, _, 0):
  print("On the y-axis.")
case (0, 0, _):
  print("On the z-axis.")
default:
  print("Somewhere in space")
}
{% endhighlight swift %}

I'm excited to see how this plays out in actual production code, as I can imagine it being a powerful feature when paired with switch statements, that allows for the handling of multiple cases concisely without having to write separate conditions for every possible value. 