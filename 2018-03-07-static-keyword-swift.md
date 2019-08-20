---
layout: article
title: An exhaustive guide to Static keyword AKA Type methods in Swift
tags: Development/Practice
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1566304410/kristofk-com/posts/2018-03-07-static-keyword-swift/static-type-swift-thumbnail-min.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1566304410/kristofk-com/posts/2018-03-07-static-keyword-swift/static-type-swift-thumbnail-min.png
---

This post is about the **static** keyword. When and how can you use it along with a specific use case? Quick note, in some cases the static keyword can be replaced by the class keyword and although Apple describes it under Type Methods, you can use the static keyword on much more than just methods.

<div>{%- include extensions/youtube.html id='n2p5Jy71l94' -%}</div>

# Theory

## Class

### Methods

In Swift, we differentiate between instance- and type methods. **Instance methods** are what you are most probably familiar with. Instance methods are what you call on the instance of a class:

    class SomeClass {
    	func instanceFunc() { print("instance func called") }
    }

    let instance = SomeClass()
    instance.instanceFunc()

On the other hand, we have **Type methods**. Type methods are called directly on the type instead of the instance. In order to specify a method as a type method, we have to use the `static`keyword.

```
class SomeClass {
	func instanceFunc() { print("instance func called") }
	static func typeMethod () { print("type method called") }
}

let instance = SomeClass()
instance.instanceFunc()

SomeClass.typeMethod()
```

A quick note that due to some Obj-C shenanigans within classes you can use the `class`keyword instead of the `static`keyword. However, it is recommended that in Swift you use the `static`keyword consistently.
{:.warning}


### Properties

Unlike the name would suggest the `static`keyword can be used on more than just methods. You can specify type properties as well which can be either mutable (`var`) and immutable (`let`).

```
class SomeClass {
	func instanceFunc() { print("instance func called") }
	static func typeMethod () { print("type method called") }

	let instanceProperty = "instance prop"
	var instancePropertyMutable = "instance prop mut"

	static let typePropImmut = "type prop imm"
	static var typePropMut = 1
}

let instance = SomeClass()
instance.instanceFunc()
instance.instanceProperty
instance.instancePropertyMutable

SomeClass.typeMethod()
SomeClass.typePropImmut
SomeClass.typePropMut
```

The mutable Type properties (`static var`) can be manipulated.

```
SomeClass.typePropMut // 1
SomeClass.typePropMut += 1
SomeClass.typePropMut // 2
```

Within a class or a type, the `static`stuff can call each other without the `self`keyword.

```
class SomeClass {
	func instanceFunc() { print("instance func called") }
	static func typeMethod () { print("type method called") }

	let instanceProperty = "instance prop"
	var instancePropertyMutable = "instance prop mut"

	static let typePropImmut = "type prop imm"
	static var typePropMut = 1

	static func addOne() { typePropMut += 1 }
}

SomeClass.typePropMut // 1
SomeClass.typePropMut += 1
SomeClass.typePropMut // 2

SomeClass.addOne()
SomeClass.typePropMut // 3
```

## Struct

**Structs** behave much the same way that classes do.

```
struct SomeStruct {
	static func someFunc() { }
	static let someProp: String = ""
}

SomeStruct.someFunc()
SomeStruct.someProp
```

## Protocol

You can also specify `static`stuff in **protocols** but you cannot call them on the protocol types, not even if you have provided a default implementation in an extension.

```
protocol SomeProtocol {
	static func someFunc ()
}

SomeProtocol.someFunc() // ERROR

extension SomeProtocol {
	static func someFunc() { print ("protocol") }
}

SomeProtocol.someFunc() // ERROR
```

# In practice

Now let’s look at a specific example. In the Official Apple Documentation, Apple uses a Level tracker minigame as an example so I’m going to stick to it.

The idea of the Level tracker is that you have a game and there are multiple users on a single device. A player can select a level to play on from the already unlocked levels. Anyone can unlock a level and it will sync across to everyone. At first, only level 1 is unlocked.

Here is the first half of the code:

```
struct LevelTracker {
    static var highestUnlockedLevel = 1
    var currentLevel = 1

    static func unlock(_ level: Int) {
        if level > highestUnlockedLevel { highestUnlockedLevel = level }
    }

    static func isUnlocked(_ level: Int) -> Bool {
        return level <= highestUnlockedLevel
    }

    @discardableResult
    mutating func advance(to level: Int) -> Bool {
        if LevelTracker.isUnlocked(level) {
            currentLevel = level
            return true
        } else {
            return false
        }
    }
}
```

The above struct works in the following manner.  
The `highestUnlockedLevel`type property is storing the highest level that was unlocked by any player.  
`unlock`type method unlocks a specified level.  
`isUnlocked`type method checks if a level is already unlocked or not, this is for convenience.  
`currentLevel`instance property keeps track of which level is an individual player on.  
`advance`method advances the player to the next level if it is unlocked.  
`@discardableResult`tag is used in order to silence those pesky warnings about not using the returned value.

The `LevelTracker`class is used in conjunction with the new class called`Player`.

```
class Player {
    var tracker = LevelTracker()
    let playerName: String
    func complete(level: Int) {
        LevelTracker.unlock(level + 1)
        tracker.advance(to: level + 1)
    }
    init(name: String) {
        playerName = name
    }
}
```

The `Player`class creates an instance of`LevelTracker`, gives a name to the player and the only thing it can do is to advance to the next level which is done by first unlocking the next level and then advancing to it.

The above mechanism could be used like so for example:

```
let player1 = Player(name: "Player1")
player1.complete(level: 1)
player1.complete(level: 2)
player1.complete(level: 4)
print("Highest unlocked level is now \(LevelTracker.highestUnlockedLevel)")

let player2 = Player(name: "Player2")
player2.tracker.advance(to: 5)
```

Here you can see that player1 advances up to level 5\. Then I check what is the highest level globally and I advance player2 to that level.

* * *

I hope you have found this post useful. The main source for the post comes from [Apple’s Official Documentation](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Methods.html).

Make sure to check back regularly and to subscribe to my [YouTube channel](https://www.youtube.com/channel/UC60VWleORVQ5rBEt85oqErQ?view_as=subscriber) since I post content at least weekly.

Feedback is always appreciated.
