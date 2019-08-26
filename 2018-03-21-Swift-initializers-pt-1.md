---
layout: article
title: struct init – Swift initializers pt. 1
tags: SwiftDevelopment
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1565952435/kristofk-com/posts/2018-03-21-Swift-initializers-pt-1/init-1-thumbnail-com-min.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1565952435/kristofk-com/posts/2018-03-21-Swift-initializers-pt-1/init-1-thumbnail-com-min.png
---

The topic of initialization in Swift if very important. You come across it every day. It is not a hard topic at all but there are many types of initalizers. This is a no-nonsense, in-depth look at initializer.

The process of initialization in Swift encapsulates everything that is needed to prepare a type for use. Reference and Value types differ in how they use initializers.

An initializer method sets up all the stored properties of a type and makes sure that the instance is ready to be used for the first time.

Let’s look at initializers in structs. I made a small diagram of all the topics I’m going to mention about struct initialization. The diagram includes example code too.

![struct init diagram](https://res.cloudinary.com/kristofk-com/image/upload/v1565952435/kristofk-com/posts/2018-03-21-Swift-initializers-pt-1/initialization-types-min.png)

<div>{%- include extensions/youtube.html id='xDDBN9xko00' -%}</div>

# Struct init

A struct is a value type just like an enum. For this reason, structs behave differently compared to classes, since a <span color="#c1349a" style="color: #c1349a;">class</span> is a reference type.

## Default <span color="#aa0d2d"><span color="#c1349a" style="color: #c1349a;">init</span></span>

Default initializers are generated for you by Xcode. By default, Xcode generates **memberwise initialization** for you for each property with the properties’ names.

    struct ShoppingListItem {
    	var name: String?
    	var quantity = 1
    	var purchased = false
    }
    var item2 = ShoppingListItem(name: "", quantity: 1, purchased: false)

Otherwise, you can give **default values for your properties** in which case the memberwise initializer will be an empty init method.

    struct ShoppingListItem {
    	var name: String?
    	var quantity = 1
    	var purchased = false
    }
    var item = ShoppingListItem()

Keep in mind that if you have an optional property without a default value then Xcode will assume that value is `nil`by default.

## Custom init

Whenever you specify a custom initializer you override the default memberwise initializer.

    struct Celsius {
    	var temperatureInCelsius: Double
    	init(fromFahrenheit fahrenheit: Double) {
    		temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }

Custom initializer methods behave much the same was as standard methods do.  
You can give

*   the same name for the parameter name and the argument label

        init(fahrenheit: Double) {
        		temperatureInCelsius = (fahrenheit - 32.0) / 1.8
        	}

*   separate names for the parameter name and the argument label

        init(fromFahrenheit fahrenheit: Double) {
        		temperatureInCelsius = (fahrenheit - 32.0) / 1.8
        	}

*   omit the argument label

        init(_ fahrenheit: Double) {
        		temperatureInCelsius = (fahrenheit - 32.0) / 1.8
        	}

*   assign default values to the arguments

        init(fromFahrenheit fahrenheit: Double = 32) {
        		temperatureInCelsius = (fahrenheit - 32.0) / 1.8
        	}

Alternatively, if you do not want to override the memberwise initializer then you can put all your custom initializers in an`extension`. This way you can choose from all the initializers later on.

    struct Misc {
    	let something: String
    }

    extension Misc {
    	init(sth: String = "") {
    		self.something = sth
    	}
    }

![](https://res.cloudinary.com/kristofk-com/image/upload/v1565952434/kristofk-com/posts/2018-03-21-Swift-initializers-pt-1/Screen-Shot-2018-03-15-at-20.09.02-min-1024x268.png)

## Initializer delegation

If you are creating multiple initializers but all of them initialize the same properties then it is a good practice to utilize initializer delegation. This means that you create a main initializer (this could be the memberwise initializer) and all the other initializers call this one. This helps us maintain the DRY (Don’t Repeat Yourself) principle.

    struct Name {
    	var prefix: String
    	let fullName: String
    	var prefixName: String
    }

    extension Name {
    	init(prefix: String = "Mr.", fullName: String) {
    		let prefixName = "\(prefix) \(fullName)"
    		self.init(prefix: prefix, fullName: fullName, prefixName: prefixName)
    	}

    	init(prefix: String = "Mr.", firstName: String, lastName: String) {
    		let fullName = "\(firstName) \(lastName)"
    		self.init(prefix: prefix, fullName: fullName)
    	}
    }

Be aware that <span color="#c1349a" style="color: #c1349a;">init</span> delegation leads to another concept and that is the **2 phase initialization**. This basically means that in an initialization method that calls another initializer you cannot use <span color="#c1349a" style="color: #c1349a;">self</span> before <span color="#c1349a" style="color: #c1349a;">self.init</span>. This splits up the init method into two distinct parts:

*   Phase 1 is before the <span color="#c1349a" style="color: #c1349a;">self.init</span> call and you cannot use self
*   Phase 2 is after the <span color="#c1349a" style="color: #c1349a;">self.init</span> call where you can use self

    init(prefix: String = "Mr.", fullName: String) {
    		let prefixName = "\(prefix) \(fullName)"
    		// self.greet is inaccessiable here
    		self.init(prefix: prefix, fullName: fullName, prefixName: prefixName)
    		self.greet()
    	}

## Failable <span color="#c1349a" style="color: #c1349a;">init</span>

In some cases, types cannot be initialized. This can be due to invalid or missing data or many other reasons too. In this case, you don’t want to work with invalid types. For this reason, Swift has failable initializers that can either return nil or throw an error.

**Failing initializers** are the ones that return nil. This is a very simple approach and you won’t necessarily know what caused the error. You can specify a failing initializer with the a “?” (`init?`).

    struct Animal {
    	let species: String
    	init?(species: String) {
    		if species.isEmpty { return nil }
    		self.species = species
    	}
    }

**Throwing initializers** are somewhat more sophisticated as they can give you an actual error instead of just nil. For this, you also need an Error type to throw. You specify a throwing initializer with the `throws`keyword (`init() throws`).

    enum AnimalError: Error {
    	case noSpeciesDefined
    }

    struct Animal {
    	let species: String
    	init(species: String) throws {
    		if species.isEmpty { throw AnimalError.noSpeciesDefined }
    		self.species = species
    	}
    }

There are of course multiple ways can deal with throwing functions but here is one.

    do {
    	try Animal(species: "")
    } catch {
    	print("error")
    }

# Partial conclusion

This was just part 1 of the no-nonsense guide to initialization in Swift. Now you know all the ins and outs of initializing `structs`in Swift.

Stay tuned for part 2 in which I’ll be looking into initializers for classes.

References:[](https://www.raywenderlich.com/119922/swift-tutorial-initialization-part-1)

[RayWenderlich – Initialization In Depth](https://www.raywenderlich.com/119922/swift-tutorial-initialization-part-1)

[Official Apple Documentation](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Initialization.html)
