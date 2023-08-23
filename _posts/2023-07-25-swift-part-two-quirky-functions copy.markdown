---
layout: post
title:  "Swift Part Two: Quirky Functions"
date:   2023-07-20 10:00:00 +0800
categories: programming
---
<p><i>
Swift functions are so full of quirks. At this point, 1 week into Swift, I am ambivalent about whether I love Swift or hate it. Today, I attempt to chronicle interesting bits of Swift functions that I discovered.
</i></p>

<p><b>Quirky Swift functions</b></p>
<p><b>1. Default parameters in functions</b></p>
Functions in Swift can have default parameters. In the example below, the quantity parameter has a default value of 1. If unspecified, the function assumes a quantity of 1.
{% highlight swift %}
func orderCoffee(_ coffeeType: String, _ quantity: Int = 1) {
    print("Preparing \(quantity) cup(s) of \(coffeeType)...")
    print("Your \(coffeeType) is ready!")
}

orderCoffee("Cappuccino") // Ordering 1 cup of Cappuccino
orderCoffee("Latte", 2) // Ordering 2 cups of Latte
{% endhighlight swift %}

<p><b>2. No need for return statements if function contains one line!</b></p>
Both functions below are correct. The former does not require the word 'return' as function consists of only one line.
{% highlight swift %}
func makeCoffee(_ coffeeType: String, withCream: Bool = false) -> String {
    coffeeType + (withCream ? " with cream" : "")
}

func makeCoffee(_ coffeeType: String, withCream: Bool = false) -> String {
    let coffee = coffeeType + (withCream ? " with cream" : "")
    return "Your \(coffee) is ready! Enjoy!"
}

{% endhighlight swift %}

<p><b>3. Variadic functions</b></p>
A variadic function accepts a varying number of input arguments of the same type and is declared using an ellipsis (...). The function treats this as an array.

{% highlight swift %}
func coffeeRun(_ friends: String..., coffeeType: String) {
    print("Going on a coffee run with: ")
    for friend in friends {
        print("- \(friend)")
    }
    print("Ordering \(coffeeType) for everyone.")
}

coffeeRun("Annie", "Brad", "Charlie", coffeeType: "Americano")
/* 
Going on a coffee run with:
- Annie
- Brad
- Charlie
Ordering Americano for everyone. 
*/
{% endhighlight swift %}

By making that parameter variadic, a whole range of additional functionality is availed without having to change the way the function is called – how useful!

<p><b>4. External & Internal Parameter labels</b></p>
As if one parameter name is not enough, Swift allows two aliases for each parameter. The first (left hand side) is to be used externally when calling the function, and the second (right hand side) is to be used internally inside the function. This is done by writing two names, separated by a space like this:

{% highlight swift %}
func sayHello(to name: String) {
    print("Hello, \(name)!")
}
{% endhighlight swift %}

The parameter is given two aliases - 'to' and 'name'. This means that externally it’s called using 'to', but internally it’s called using 'name'. This gives variables a sensible name inside the function.

{% highlight swift %}
func setAge(for wine: String, to value: Int) {
    print("\(wine) is now \(value)")
}
{% endhighlight swift %}

When we call the function externally: 

{% highlight swift %}
setAge(for: "Brunello di Montalcino", to: 25)
{% endhighlight swift %}

The function becomes readable as a standard English statement: “Set age for Brunello di Montalcino to 25”. Using both internal and external labels is not a must, although functions read more naturally when we have them. I'm quite amused by Swift's attempt to connect with the human programmer.

<p><b>5. Mutating Functions</b></p>
A mutating function is a special function defined within a value type (such as a struct or enum) and is used to modify the properties of that value type. Otherwise, by default, functions defined within a value type are not allowed to modify the properties of the value type.

The code below represents a struct called CoffeeMachine, which has a coffeeAmount property representing the amount of coffee in the machine. A brewCoffee() method simulates the brewing of fresh coffee (yum). The catch here is that the coffee machine has a fixed capacity, and we want to avoid exceeding it when making coffee.

{% highlight swift %}
struct CoffeeMachine {
    var coffeeAmount: Int
    let maxCapacity: Int

    init(coffeeAmount: Int, maxCapacity: Int) {
        self.coffeeAmount = coffeeAmount
        self.maxCapacity = maxCapacity
    }

    mutating func brewCoffee(amount: Int) {
        let remainingSpace = maxCapacity - coffeeAmount
        if amount <= remainingSpace {
            coffeeAmount += amount
            print("Brewing \(amount) ml of coffee. Enjoy your coffee!")
        } else {
            print("Not enough space to brew \(amount) ml of coffee. Only \(remainingSpace) ml available.")
        }
    }
}

var coffeeMachine = CoffeeMachine(coffeeAmount: 200, maxCapacity: 500)
coffeeMachine.brewCoffee(amount: 300)
// Output: "Not enough space to brew 300 ml of coffee. Only 300 ml available."

coffeeMachine.brewCoffee(amount: 100)
// Output: "Brewing 100 ml of coffee. Enjoy your coffee!"

print(coffeeMachine.coffeeAmount)
// Output: 300
{% endhighlight swift %}

Without the mutating keyword, the brewCoffee(amount:) method would not be allowed to modify the coffeeAmount property of the CoffeeMachine. The mutating keyword is required in this scenario because the CoffeeMachine struct is a value type (struct) in Swift. The mutating function is said to be able to modify the state of the struct.

<p><b>6. Throwing Functions</b></p>
Throwing functions is Swift's way of handling errors in a structured and graceful manner during the execution of code.

The below function called brewCoffee takes an optional parameter coffeeBeans. This function simulates brewing coffee by grinding the coffee beans. However, if the coffee beans are nil, it means there are no coffee beans to brew, and we want to throw an error.

{% highlight swift %}
enum CoffeeError: Error {
    case noCoffeeBeans
}

func brewCoffee(coffeeBeans: String?) throws -> String {
    guard let beans = coffeeBeans else {
        throw CoffeeError.noCoffeeBeans
    }
    return "Enjoy your brewed coffee with \(beans)!"
}

do {
    let coffeeResult = try brewCoffee(coffeeBeans: "Arabica")
    print(coffeeResult)
} catch CoffeeError.noCoffeeBeans {
    print("Error: No coffee beans available. Cannot brew coffee.")
} catch {
    print("Unknown error occurred: \(error)")
}
{% endhighlight swift %}

An enum called CoffeeError is defined, which represents the errors that can occur during the coffee brewing process. It has a single case noCoffeeBeans, which indicates that there are no coffee beans available to brew.

The brewCoffee(coffeeBeans:) function is marked with throws, which means it can potentially throw an error. Inside the function, we use the guard statement to check if the coffeeBeans parameter is nil. If it is, we throw the customised CoffeeError.noCoffeeBeans error.

When calling a throwing function, the try keyword is necessary to indicate that we are aware of the possibility of an error being thrown, and handle the error using a do-catch block. If the function throws an error, it will be caught in the catch block based on the error type. 
