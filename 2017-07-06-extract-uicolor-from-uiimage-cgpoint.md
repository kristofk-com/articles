---
layout: article
title: Extract UIColor from UIImage @ CGPoint
tags: SwiftDevelopment
---

This code snippett will allow you to extract the UIColor of a pixel in a UIImage at a given CGPoint. This is useful for apps that deal with pictures or colors.

First of all the code:

```
extension UIImage {    
    public func getPixelColor(pos: CGPoint) -> UIColor {

        let pixelData = self.cgImage!.dataProvider!.data
        let data: UnsafePointer<UInt8> = CFDataGetBytePtr(pixelData)

        let pixelInfo: Int = ((Int(self.size.width) * Int(pos.y)) + Int(pos.x)) * 4

        let r = CGFloat(data[pixelInfo]) / CGFloat(255.0)
        let g = CGFloat(data[pixelInfo+1]) / CGFloat(255.0)
        let b = CGFloat(data[pixelInfo+2]) / CGFloat(255.0)
        let a = CGFloat(data[pixelInfo+3]) / CGFloat(255.0)

        return UIColor(red: r, green: g, blue: b, alpha: a)
    }
}
```

As you can see this is an extension, which means that you can use the function at any instance of UIImage.

## How to use the code snippet in a Playground

1.  You need to import UIKit

		```
    import UIKit
		```

2.  Add an image to the Resourches folder  

    I have an image inside the Resources folder called app-icon.png

3.  Create an instance of the UIImage class

		```
    let image = UIImage(named: "app-icon.png")
		```

4.  Create a point with the CGPoint class

		```
    let point = CGPoint(x: 768, y: 384)
		```

5.  Call the function on the instance

		```
    let color = image?.getPixelColor(pos: point)
		```

    This will return the R, G, B, and A values of the UIImage.

Full playground file:

```
import UIKit

extension UIImage {
    public func getPixelColor(pos: CGPoint) -> UIColor {

        let pixelData = self.cgImage!.dataProvider!.data
        let data: UnsafePointer<UInt8> = CFDataGetBytePtr(pixelData)

        let pixelInfo: Int = ((Int(self.size.width) * Int(pos.y)) + Int(pos.x)) * 4

        let r = CGFloat(data[pixelInfo]) / CGFloat(255.0)
        let g = CGFloat(data[pixelInfo+1]) / CGFloat(255.0)
        let b = CGFloat(data[pixelInfo+2]) / CGFloat(255.0)
        let a = CGFloat(data[pixelInfo+3]) / CGFloat(255.0)

        return UIColor(red: r, green: g, blue: b, alpha: a)
    }
}

let image = UIImage(named: "app-icon.png")

let point = CGPoint(x: 768, y: 384)

let color = image?.getPixelColor(pos: point)
```

If you have any questions or taughts leave theme down below in the comment section.
