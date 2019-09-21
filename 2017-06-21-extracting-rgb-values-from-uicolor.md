---
layout: article
title: Extracting RGB values from UIColor
tags: SwiftDevelopment
---

This code snippet is an extension to the UIColor class for extractiog the RGB color values since accessing theme with the built in methods is messy.

**This is the code, you can insert it into any of the project files:**

```
extension UIColor {

    public func rgb() -> (red:Int, green:Int, blue:Int, alpha:Int)? {
        var fRed : CGFloat = 0
        var fGreen : CGFloat = 0
        var fBlue : CGFloat = 0
        var fAlpha: CGFloat = 0
        if self.getRed(&fRed, green: &fGreen, blue: &fBlue, alpha: &fAlpha) {
            let iRed = Int(fRed)
            let iGreen = Int(fGreen)
            let iBlue = Int(fBlue)
            let iAlpha = Int(fAlpha)

            return (red:iRed, green:iGreen, blue:iBlue, alpha:iAlpha)
        } else {
            // Could not extract RGBA components:
            return nil
        }
    }
}
```

## Now how to use this extension

1.  You need to import UIKit…. duh…

	```
	import UIKit
	```

2.  Create an instance of the UIColor class

	```
  let color: UIColor = UIColor(red: 234, green: 54, blue: 1, alpha: 1)
	```

3.  Call the rgb() method

	```
  let rgb = color.rgb()
	```

4.  Now you can access each color, they are returned in _Int?_

	```
  let red = color.rgb()?.red
  let green = color.rgb()?.green
  let blue = color.rgb()?.blue
  let alpha = color.rgb()?.alpha
	```

5.  If you want to print theme than you can wrap theme up in a neat String

	```
  let rgbColors = "R:\(red!) G:\(green!) B:\(blue!) A:\(alpha!)"
  print(rgbColors)
	```

Full playground file:

```
import UIKit

extension UIColor {

    public func rgb() -> (red:Int, green:Int, blue:Int, alpha:Int)? {
        var fRed : CGFloat = 0
        var fGreen : CGFloat = 0
        var fBlue : CGFloat = 0
        var fAlpha: CGFloat = 0
        if self.getRed(&fRed, green: &fGreen, blue: &fBlue, alpha: &fAlpha) {
            let iRed = Int(fRed)
            let iGreen = Int(fGreen)
            let iBlue = Int(fBlue)
            let iAlpha = Int(fAlpha)

            return (red:iRed, green:iGreen, blue:iBlue, alpha:iAlpha)
        } else {
            // Could not extract RGBA components:
            return nil
        }
    }
}

let color: UIColor = UIColor(red: 234, green: 54, blue: 1, alpha: 1)

let rgb = color.rgb()

let red = color.rgb()?.red //
let green = color.rgb()?.green
let blue = color.rgb()?.blue
let alph = color.rgb()?.alpha

let rgbColors = "R:\(red!) G:\(green!) B:\(blue!) A:\(alpha!)"
print(rgbColors)
```

If you have any questions or taughts leave theme down below in the comment section.
