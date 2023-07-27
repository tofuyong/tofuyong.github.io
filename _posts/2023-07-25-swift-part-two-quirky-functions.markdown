---
layout: post
title:  "Swift Part Two: Quirky Functions"
date:   2023-07-20 10:00:00 +0800
categories: programming
---
<p><i>
Swift functions are so full of quirks. At this point, 1 week into Swift, I can't quite decide if I love it or hate it.
</i></p>

<p><b>Quirky Swift functions</b></p>
<p><b>1. Default parameters in functions</b></p>
Functions in Swift can have default parameters. In the example below, the quantity parameter has a default value of 1. If unspecified, the function assumes a quantity of 1.
{% highlight swift %}
func orderCoffee(_ coffeeType: String, _ quantity: Int = 1) {
    print("Preparing \(quantity) cup(s) of \(coffeeType)...")
    // Add code to prepare the coffee here
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
As if one name for one parameter is not enough, I find it rather cute that Swift allows us to provide two names for each parameter. One is to be used externally when calling the function, and the second one to be used internally inside the function. This is done by writing two names, separated by a space like this:

{% highlight swift %}
func sayHello(to name: String) {
    print("Hello, \(name)!")
}
{% endhighlight swift %}

The parameter is called 'to name', which means externally it’s called 'to', but internally it’s called 'name'. This gives variables a sensible name inside the function, and also means calling the function reads more naturally:

{% highlight swift %}
sayHello(to: "Taylor")
{% endhighlight swift %}

Swift even takes it a step further by allowing us to write our labels twice, like:

{% highlight swift %}
func setAge(for person: String, to value: Int) {
    print("\(person) is now \(value)")
}
{% endhighlight swift %}

When we call the function: 

{% highlight swift %}
setAge(for: "Paul", to: 40)
{% endhighlight swift %}

The function becomes readable as a standard English statement: “Set age for Paul to 40”. Using both internal and external labels is not a must, although our functions read more naturally when we have them. I'm quite amused by Swift's attempt to connect with the human programmer.