---
layout: article
title: Current location of iOS device in Swift
tags: Development/Practice
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1566632614/kristofk-com/posts/2018-01-21-location-swift/thumbnail-location-in-swift-min.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1566632614/kristofk-com/posts/2018-01-21-location-swift/thumbnail-location-in-swift-min.png
---

This blog post is a quick guide to the most basic method of getting the current location of any iOS device. There are plenty of tutorials out there on how to build turn by turn navigation and how to acquire location from the background. I couldn’t, however, find a blog post or a video that discusses the simplest and most primitive way to get the location of the device.

This method is good in cases like a weather app or maybe if you want to give fun facts to the user about their location when they launch the app or press a button.

<div>{%- include extensions/youtube.html id='RjVrSfQNkbM' -%}</div>

# Technologies

So I’m going to be using Apple’s built-in technologies: CoreLocation, CLLocationManager and CLGeocoder.

# Setting up the project

So the first step is to create a project. Now in this project, we won’t be displaying any data on the user’s screen but we are going to print to the console in Xcode. So we need to create a new Single View project the language of which is going to be Swift.

![Creating new project 1](https://res.cloudinary.com/kristofk-com/image/upload/v1566632632/kristofk-com/posts/2018-01-21-location-swift/1-new-proj-1-min-300x216.png)![Creating new project 2](https://res.cloudinary.com/kristofk-com/image/upload/v1566632610/kristofk-com/posts/2018-01-21-location-swift/1-new-proj-2-min-1024x739.png)

## Edit Info.plist

In the Info.plist file we need to add a new line. The title of the line is going to be

```
Privacy - Location When In Use Usage Description</pre>
```

the type is `String` and the value can be anything you want it to be, for me it is `This app is all about determining your location.`

![Adding row to info plist file](https://res.cloudinary.com/kristofk-com/image/upload/v1566632610/kristofk-com/posts/2018-01-21-location-swift/2-info-plist-1-min-221x300.png)![info plist file](https://res.cloudinary.com/kristofk-com/image/upload/v1566632610/kristofk-com/posts/2018-01-21-location-swift/2-info-plist-2-min-300x142.png)

## Set up Main.storyboard

This step is going to be very easy! Just drag a button in the middle of the screen and click **Resolve Auto Layout Issues -> Add Missing Constraints**. After this connect the button’s Touch Up Inside action to the ViewController.

![Setting up main storyboard](https://res.cloudinary.com/kristofk-com/image/upload/v1566632610/kristofk-com/posts/2018-01-21-location-swift/3-main-story-min-300x205.png)

## Write the code for determining the location in ViewController.swift

The code we need to write is very short! I am going to go in the order that the documentation recommends.

1.  Import the CoreLocation framework  
    Insert the following code to the very beginning of the file.

```
import CoreLocation
```

2.  Create an instance of `CLLoactionManager`  
    Instert the following code to the very beginning of the ViewController class.

```
let locationManager = CLLocationManager()
```

3.  Set up the [delegate](https://old.kristofk.com//delegation-swift/) and request access to location  
    Insert the following code into the `viewDidLoad()` function – this is going to show an error but you can disregard it for now.

```
locationManager.delegate = self
locationManager.requestWhenInUseAuthorization()
```

4.  Set up the [delegate](https://old.kristofk.com//delegation-swift/) functions that are going to be called when we request the location  
    The 2 functions that are going to be called when we request the location are `locationManager(_:didUpdateLocations:)` and `locationManager(_:didFailWithError:)`. The 1st one is called if the location can be determined successful otherwise the didFailWithError is going to be called. I like to set up functions like these separately in extensions so let’s do that. Insert the following code in an extension under the ViewController class.

		```
    extension ViewController: CLLocationManagerDelegate {
    	func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
    		if let lat = locations.last?.coordinate.latitude, let long = locations.last?.coordinate.longitude {
    			print("\(lat),\(long)")
    		} else {
    			print("No coordinates")
    		}
    	}
    	func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
    		print(error)
    	}
    }
		```

    This code will print out your coordinates if they are successfully acquired. If the coordinates are not available then “No coordinates” string will be printed out. And if the location cannot be determined then simply the error is going to be printed.

5.  Now for the last step of determining your location, we need to call the requestLocation() function. I’ll call it in the IBAction function that we created for the button previously but you could also call it in `viewDidLoad` or even better `viewDidAppear`.

		```
    @IBAction func button(_ sender: Any) {
    		locationManager.requestLocation()
    }
		```

## Giving the location a meaningful name

Your users won’t understand coordinates for locations but rather a more meaningful name like a landmark, street or city. So now let’s convert the coordinates into more meaningful names. For this, I’m going to be using `GLGeocoder` class. I have copied the following code from Apple’s website and I have pasted it into the extension of the delegate functions.

```
func lookUpCurrentLocation(completionHandler: @escaping (CLPlacemark?) -> Void ) {
		// Use the last reported location.
		if let lastLocation = self.locationManager.location {
			let geocoder = CLGeocoder()

			// Look up the location and pass it to the completion handler
			geocoder.reverseGeocodeLocation(lastLocation, completionHandler: { (placemarks, error) in
				if error == nil {
					let firstLocation = placemarks?[0]
					completionHandler(firstLocation)
				}
				else {
					// An error occurred during geocoding.
					completionHandler(nil)
				}
			})
		}
		else {
			// No location was available.
			completionHandler(nil)
		}
	}
```

This function takes no arguments since it accesses the locationManager directly. This function accepts a closure with 1 parameter that is the Geolocation of the coordinates. In this closure, we can specify what we want to do with the result.

Let’s call this function if and when our coordinates are printed right after the print statement. This allows us to make sure that we have a location. The code is the following:

```
lookUpCurrentLocation { geoLoc in
				print(geoLoc?.locality ?? "unknown Geo location")
			}
```

# Conclusion

Now if you run your this app on a physical iPhone or iOS device then you should get the coordinates and the name of the city back. In case something went wrong then you’ll get some kind of an error message based on where the error occurred.

* * *

If you would like to read up on this topic then I recommend you start with the [Official Apple Documentation](https://developer.apple.com/documentation/corelocation).

I hope that this post helped some of you to get started in CoreLocation. If you want to get similar information on iOS development, make sure to check back to kristofk.com weekly.
