---
layout: article
title: Facebook Swift SDK updated to Swift 4
tags: SwiftDevelopment
---

For a while now Facebook’s Swift SDK hasn’t been updated and some deprecated code was left inside. Then Swift 4 came along and it made things even worse. I believe it is time for a guide on how to set up the SDK in Xcode 9 / Swift 4\. Alternatively, you could use the iOS SDK but I’ll leave it up to you.

Multiple issues have been created regarding this. ([issue1](https://github.com/facebook/facebook-sdk-swift/issues/162) [issue2](https://github.com/facebook/facebook-sdk-swift/issues/182))

For starters according to the official Facebook documentation you set up the SDK with CocoaPods by using the following pods:

```
pod 'FacebookCore'
pod 'FacebookLogin'
pod 'FacebookShare'
```

This is all fine and well but if you try to compile your project now it won’t work. In the next three steps I’ll show you the errors and the fixes.

* * *

## 1) Get-only properties

_[Source: Brigadier @ StackOverflow](https://stackoverflow.com/a/44534962/6879072)_

This error normally would show up only when you fix the 2nd and 3rd error but you need to fix this before theme, not to mention it is convenient this way.  
I don’t know how this happened and why was this left in the SDK, regardless here is the fix.

_Go inside the Podfile_

**Replace this:**

```
pod 'FacebookShare'
```

**With this:**

```
pod 'FacebookShare', :git => 'https://github.com/1amageek/facebook-sdk-swift'
```

* * *

## 2) ‘toUIntMax()’ obsoleted

_[Source: zach-fuller @ GitHub](https://github.com/facebook/facebook-sdk-swift/issues/162)_

This error is a result of updating to Swift 4, but it is very easy to fix.

There are two instances of this error, in both cases:

**Replace this:**

```
$0.toUIntMax() as UInt64
```

**With this:**

```
UInt64($0)
```

* * *

## 3) Cannot subscript a value…

_[Source: carlhung @ Github](https://github.com/facebook/facebook-sdk-swift/issues/162)_

The full error message:

```
Cannot subscript a value of type 'String.UnicodeScalarView' with an index of type 'CountableRange' (aka 'CountableRange')
```

This fix yet again is replacing the code.

**Replace this:**

```
let range = 0 ..< min(10, cleaned.count)
let characters = cleaned[range].map(Character.init)
return String(characters)
```

**With this:**

```
let substr = String(cleaned)
if substr.characters.count > 10 {
  let endIndex = substr.index(substr.startIndex, offsetBy: 9)
  return String(substr[substr.startIndex...endIndex])
} else {
  return substr
}
```

* * *

**Conclusion**  
Let’s hope that Facebook will get back to this SDK and update it. It would be nice if everything would be updated to Swift even the Facebook app. Until then we will have to live with this SDK and the iOS SDK.
