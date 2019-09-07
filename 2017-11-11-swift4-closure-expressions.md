---
layout: article
title: Guide to Closure Expressions in Swift 4
tags: SwiftDevelopment
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1567847171/kristofk-com/posts/2017-11-11-swift4-closure-expressions/thumbnail_guide_to_closure_expressions_in_swift_4.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1567847171/kristofk-com/posts/2017-11-11-swift4-closure-expressions/thumbnail_guide_to_closure_expressions_in_swift_4.png
---

Arguably one of the hardest concepts to grasp in swift is closures. Closures are placeholders for functions. They do the exact same thing as functions but closures are preferred for their speed and unique syntactical sugar.

This post will specifically focus on closure expressions.

> Closure expressions are unnamed closures written in a lightweight syntax that can capture values from their surrounding context. _-Apple_

## Understanding functions

Just a quick recap of the essentials of functions in order to understand closures. This is the syntax of a function:

![](https://res.cloudinary.com/kristofk-com/image/upload/v1567847272/kristofk-com/posts/2017-11-11-swift4-closure-expressions/func-syntax.png)

The **head** of the functions is made up of the name, parameters and the return type. The statements make up the **body** of a function.

![](https://res.cloudinary.com/kristofk-com/image/upload/v1567847272/kristofk-com/posts/2017-11-11-swift4-closure-expressions/eg-func.png)

Functions are **first-class citizens**, meaning that they behave similar to variables and constants. They can be assigned to var and let just like any value. This means that they have a **type**. The type is determined by the parameters (only the parameter’s type not the name) and the return type.

![](https://res.cloudinary.com/kristofk-com/image/upload/v1567847272/kristofk-com/posts/2017-11-11-swift4-closure-expressions/let-func.png)

In this case, the type of the greeting func is `(String) -> String`.

## Closures

### The Sorted Method

In the official Apple documentation closure expressions are explained via the `sorted(by:)` method so I’m going to use that in my examples too. Here is a quick explanation of the `sorted(by:)` method.

> Swift’s standard library provides a method called sorted(by:), which sorts an array of values of a known type, based on the output of a sorting closure that you provide. Once it completes the sorting process, the sorted(by:) method returns a new array of the same type and size as the old one, with its elements in the correct sorted order. The original array is not modified by the sorted(by:) method.
>
> The sorted(by:) method accepts a closure that takes two arguments of the same type as the array’s contents, and returns a Bool value to say whether the first value should appear before or after the second value once the values are sorted. The sorting closure needs to return true if the first value should appear before the second value, and false otherwise.

In the following examples, I’ll be using an Array of Strings that will be sorted in reverse alphabetical order. The initial array: `let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]` The method will take a function of type `(String, String) -> Bool`.

### Standard way to sort the array

One way we could sort the array is to write a function.

```
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}
```

Then we can pass it in and watch the magic happen.

```
var reversedNames = names.sorted(by: backward)
// reversedNames is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
```

This is the least efficient way to do it and arguably not the easiest to read either.

### Closure expression

![](https://res.cloudinary.com/kristofk-com/image/upload/v1567847272/kristofk-com/posts/2017-11-11-swift4-closure-expressions/closure-expression-syntax.png) The difference between the syntax of the closure expression and function is that the closure expression:

*   doesn’t have a name
*   written in curly braces
*   the head and the body is separated by `in` instead of curly braces

According to this the array can be sorted like so:

```
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```

Because there is only one line in the body let us do ourselves a favor and put the closure in one line:

```
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )
```

### Inferring type from context

Since the type is given `(String, String) -> Bool` we can leave out the following:

*   type of the parameters
*   return type and the arrow

So we could write:

```
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
```

### Implicit Returns from Single-Expression Closures

Since we have only one line of body we can leave out the return statement:

```
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```

### Shorthand Argument Names

The `s1` and `s2` in the previous examples were custom names for the arguments, but swift gives default names like: `$0, $1, $2, $3...`. This means that everything before `in` can be left out.

```
reversedNames = names.sorted(by: { $0 > $1 } )
```

### Operator Methods

Operator functions like `>` and `<` happened to have the same type as the `sorted(by:)` method requires so we could just pass that in:

```
reversedNames = names.sorted(by: >)
```

### Trailing closures

If the last parameter of the method expects a closure then you can leave out the name of the parameter and the closure and write it afterward in curly braces:

```
reversedNames = names.sorted() { $0 > $1 }
```

This is most useful when you want to write a bigger closure and writing it outside the parentheses is easier.

If the argument list consists only of the closure than the parentheses can be left out too:

```
reversedNames = names.sorted { $0 > $1 }
```

### A common mistake

Sometimes there is a confusion between the role of curly braces and parentheses and something like this can happen:

```
reversedNames = names.sorted() { > }
```

As a rule of thumb: when you pass in a function that is already written you don’t need `{}` but if you are writing the closure inline than you do it inside the `{}`.

## Conclusion

So in the post, I started with the least efficient and longes way to solve the problem and worked my way to the optimal way to do it. My advice is that you use the last example in your code for closures as it strikes a good balance between readability and efficiency.

## Further reading

There is a website dedicated to explaining closures called [fuckingswiftblocksyntax](http://fuckingswiftblocksyntax.com). This website is now outdated but it can still be useful. [Official Apple documentation](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Closures.html) is also available on the topic.
