---
layout: article
title: class init – Swift initializers pt. 2
tags: SwiftDevelopment
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1565861982/kristofk-com/posts/2018-03-28-class-init%E2%80%93Swift-initializers-pt-2/init-2-thumbanil-com-min.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1565861982/kristofk-com/posts/2018-03-28-class-init%E2%80%93Swift-initializers-pt-2/init-2-thumbanil-com-min.png
---

This is part 2 of Swift initializers. [You can find part 1 here](https://old.kristofk.com//swift-initializers-1/). This post is going to be an exhaustive guide to initializers for Classes in Swift.

I created a diagram about all the topics I am going to discuss here.

![class initialization diagramm](https://res.cloudinary.com/kristofk-com/image/upload/v1565861982/kristofk-com/posts/2018-03-28-class-init%E2%80%93Swift-initializers-pt-2/initialization-types-transparent-min.png)

# Class

A class is a reference type in Swift meaning that each time you copy the instance it is going copy only the reference to the original instance. So if you change one instance then all the others will change as well.

Classes support inheritance. The subclasses must initializer all the superclasses before use. This is going to be the trickiest part.

# Root classes

If your class doesn’t inherit from any other class then it is called a root class. This is the simplest form of a class. You don’t have to worry about initializing any other classes.

## Designated initializers

Designated initializers must set up an instance of the type so that it is ready to be used for the first time. This initializer is most similar to an initializer in a struct.

All the properties get initializer before this init method completes.


```
class Person {
	let name: String
	let height: String
	let weight: String

	init(name: String, height: String, weight: String) {
		self.name = name
		self.height = height
		self.weight = weight
	}
}
```

## Convenience initializers

Convenience initializers don’t initialize the properties of the type directly. Rather they call the designated initializer. Convenience initializers are great if you’d like to accept different types of certain arguments or if you want to do some conversion. You can do these things in a convenience initializer and then call the designated initializer for the actual initialization.

```
convenience init(firstName: String, lastName: String, height: String, weight: String) {
    let fullName = "\(firstName) \(lastName)"
    self.init(name: fullName, height: height, weight: weight)
}
```

## Failable initialization

Just like in pt. 1 of initializers where I discussed initializers for structs, there are failable initializers for classes too. The purpose here is to not let a corrupted instance of a Type occur at any point of out code. You can use failing and throwing initializers. The behaviour is dependent on wether the initializer is a designated or a convenience initializer.

### Failing init

You use the `init?`keyword in order to create a failing designated initializer. This allows you to return nil at any point in the initializer in order to render that instance unusable aka nil.

```
// Designated init
init?(name: String, height: String, weight: String) {
	if name.isEmpty || height.isEmpty || weight.isEmpty { return nil }
	self.name = name
	self.height = height
	self.weight = weight
}

// Convenience init
convenience init?(firstName: String, lastName: String, height: String, weight: String) {
	let fullName = "\(firstName) \(lastName)"
	if fullName.isEmpty || height.isEmpty || weight.isEmpty { return nil }
	self.init(name: fullName, height: height, weight: weight)
}
```

It is a good practice to have non-failing designated initializers and to encapsulate all your failing logic inside a convenience init. This makes the implementation clearer.

# Subclasses

Subclasses do everything that superclasses do, initialize their own properties. On top of that, they have to make sure that the initialize the superclasses too.

## Designated and convenience initializers

Subclasses, just like a superclass can define designated and convenience initializers. However, because superclasses have to be initialized, two-step initialization comes into the picture.

In case of a designated initializer you have to do the following

1.  initializer all the stored properties (you cannot directly initialize the superclass’s properties, only the ones that the class introduces)
2.  Call the initializer method of the superclass (this makes sure that the superclass gets initialized properly)

```
class Male: Person {
	let gender = "M"
	var hairLength: String

	init(hairLength: String, name: String, height: String, weight: String) {
		self.hairLength = hairLength
		print(self.hairLength)
		super.init(name: name, height: height, weight: weight)
		print(self.name)
	}
}
```

Convenience initializers cannot call the the designated initializer of the superclass, but rather it can call the designated initializer of its’s class. So basically in the convenience initializer you should do all the failing and other logic and then delegate to the designated initializer in order to do the actual initialization. The designated initializer will also call the the superclass’s init so you are covered.

```
class Male: Person {
	let gender = "M"
	var hairLength: String

	init(hairLength: String, name: String, height: String, weight: String) {
		self.hairLength = hairLength
		print(self.hairLength)
		super.init(name: name, height: height, weight: weight)
		print(self.name)
	}

	convenience init(name: String) {
		self.init(hairLength: "3cm", name: "Kristof Kocsis", height: "195cm", weight: "80kg")
	}
}
```

If you override all the designated initializers of a superclass, you will inherit all the convenience initializers associated with that superclass. By default, these inherited convenience initializers will only call the overriden designated initializer. You can also give your own definition of the convenience init in the subclass.

## Overriding initializers

In Swift, once you declare a designated initializer, you no longer have access to the superclass’s designated initializer to initialize the class. If you want to use the same initializer signature then you can override the original initializer. Override behaves a little different depending on if you are overriding a designated initializer or a convenience init and if you are overriding with a designated or a convenience init.

### Overriding a designated initializers

If you override the designated initializer of a superclass you still need to initialize the properties in the class and call super.init since you are only using the signature of the function and not the contents of it.

```
class Male: Person {
	let gender = "M"
	var hairLength: String

	init(hairLength: String, name: String, height: String, weight: String) {
		self.hairLength = hairLength
		print(self.hairLength)
		super.init(name: name, height: height, weight: weight)
		print(self.name)
	}

	convenience init(name: String) {
		self.init(hairLength: "3cm", name: "Kristof Kocsis", height: "195cm", weight: "80kg")
	}

	override init(name: String, height: String, weight: String) {
		self.hairLength = "0"
		super.init(name: name, height: height, weight: weight)
	}
}
```

### Overriding convenience initializers

Strictly speaking you cannot override a convenience init of a superclass. You can only override a designated init because you can call super.init and access a it. This is not the case with convenience initializers. You cannot access a superclass’s convenience initializer from a subclass.

So if you want to use the same init signature as a convenience init’s signature in a superclass you can just simply create the same initializer without the override keyword and the compiler won’t complain.

```
class SomeClass {
	var str: String

	init(str: String) {
		self.str = str
	}

	convenience init(strFromInt num: Int) {
		self.init(str: "\(num)")
	}
}

class AnotherClass: SomeClass {
	var text: String

	init(text: String, str: String) {
		self.text = text
		super.init(str: str)
	}

	override init(str: String) {
		self.text = str
		super.init(str: str)
	}

	convenience init(strFromInt num: Int) {
		self.init(str: "\(num)")
	}
}
```

## Overriding with a designated vs convenience initializers

You just learned about overriding convenience and designated initializers. Now let’s talk about overriding the init method with either a convenience or designated init.

All of our previous overrides were done using designated initializers. So this is when you can call super.init. However in this case, if have another designated init in your class and you have some logic in it, you cannot call it from the overridden designated init. This is because you cannot call a designated initializer from a designated initializer.

If you want to override a superclass’s initializer and you want to call the subclass’s designated init the you can override with a convenience init. You declare a convenience overriding init by using`convenience override init`. (You can also use `override convenience init`, this makes no difference. But this makes your code harder to read since people might think you are overriding a convenience init which you arent. You are overriding a designated init with a convenience init.)

```
class SomeClass {
	var str: String

	init(str: String) {
		self.str = str
	}

	convenience init(strFromInt num: Int) {
		self.init(str: "\(num)")
	}
}

class AnotherClass: SomeClass {
	var text: String

	init(text: String, str: String) {
		self.text = text
		super.init(str: str)
	}

	convenience override init(str: String) {
		self.init(text: "", str: str)
	}

	convenience init(strFromInt num: Int) {
		self.init(str: "\(num)")
	}
}
```

## Initialization funnel

You might have been wondering about the `self.init`and `super.init`calls and how they work. Well they are a product of a concept called the Initialization funnel. This initialization funnel makes sure that you are initializing all your classes and that you are correctly initializing all your classes ion a hierarchy.

In the initialization funnel a convenience init can only call one designated init in the same class or call another convenience init from the same class. Ultimately a convenience init must get to designated init. Designated initializers can only call one designated init from a superclass when if applicable.

![initialization funnel](https://res.cloudinary.com/kristofk-com/image/upload/v1565861981/kristofk-com/posts/2018-03-28-class-init%E2%80%93Swift-initializers-pt-2/initializerDelegation-min.png)

# Conclusion

Now you know all there is to know about class initialization. If you read part 1 then you know everything there is to know about initialization in Swift.

If you’d like to read more here are some useful resources:

[Apple Official Documentation](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Initialization.html)

[Ray Wenderlich Initializers pt.2](https://www.raywenderlich.com/121603/swift-tutorial-initialization-part-2)
