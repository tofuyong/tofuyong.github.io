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

<p><b>2. No need for return statements if method contains one line!</b></p>

<p><b>3. External & Internal Parameter labels</b></p>

<p><b>4. Variadic functions</b></p>