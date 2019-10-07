---
layout: article
title: "[Outdated] Using frameworks in Playgrounds (Xcode 9)"
tags: SwiftDevelopment
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1567151811/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/thumbnail_playground-framework.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1567151811/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/thumbnail_playground-framework.png
---

In this post, I’m going to show off how to use 3rd party libraries and frameworks imported with CocoaPods in Xcode 9 playgrounds. This takes only a few minutes to set up.

Why would you use a framework in a playground? Glad you ask, you use Playground to prototype and test features quickly as it runs instantly… surprise, surprise. The framework part comes in handy when the sad feature is dependent on an external framework. The inspiration comes from trying to set up JTAppleCalendar in my project and I needed to constantly run the project to see the changes every time. Playground is a big time saver.

I am going to use the [JTAppleCalendar](https://github.com/patchthecode/JTAppleCalendar) framework/library for this project.  
You could also use the Facebook SDK of which I wrote a [blog post](https://old.kristofk.com//facebook-swift-sdk-updated-to-swift-4/).

## Setting up the Xcode project

If you already have a project with working libraries or frameworks I’d recommend you skip this step and use the Workspace of the project.

### Creating an Xcode Project

Otherwise, go ahead and create a new Project, I’m going to create a Single View app, but it shouldn’t matter which template you use. I’ll name my **playDemo**.

![Creating Xcode project](https://res.cloudinary.com/kristofk-com/image/upload/v1567151810/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/projectSetUp.jpg)

### Importing Framework

I’m going to be using [CocoaPods](https://cocoapods.org) but it shouldn’t matter what tool you use if any. If you have never used CocoaPods before than here is the [installation guide](https://guides.cocoapods.org/using/getting-started.html).

1.  Open terminal and run the following commands
    *   `$ cd <projectDirectory>`
    *   `$ pod init`
    *   `$ open Podfile`

![Terminal window screenshot](https://res.cloudinary.com/kristofk-com/image/upload/v1567151811/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/terminal1.jpg)

1.  Now you should have the Podfile open in Text Edit and this is where you can add your pods, I’ll ad JTAppleCalendar like so:

![Text edit Podfile screenshot](https://res.cloudinary.com/kristofk-com/image/upload/v1567151810/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/Podfile.jpg)

1.  Now save and close the Podfile and back in terminal run the following command
    *   `$ pod install`
    *   `$ open <projectName>.xcworkspace` <span style="font-size: 1em">alternatively, you can open the workspace file in the project’s directory</span>

![Terminal window screenshot](https://res.cloudinary.com/kristofk-com/image/upload/v1567151811/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/terminal2.jpg)

That <span style="font-size: 1em">is it for the setup, now you have a fully functioning project with a framework.</span>

## Set up Playground file

1.  Let’s start with creating the playground file, there are multiple ways to do this:
    *   From the Xcode Home screen
    *   ⌘ + ⌥ + ⇧ + N

1.  Name it anything and save it anywhere. I’ll leave the default name and I’ll save it next to the project directory.

![Creating playground](https://res.cloudinary.com/kristofk-com/image/upload/v1567151810/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/playgroundSetUp.jpg)

### Copy the Playground into the workspace

1.  You should already have the workspace open but if you don’t just open it from the project’s library

1.  File → Add Files to “<projectName>”

![Options selection](https://res.cloudinary.com/kristofk-com/image/upload/v1567151810/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/addFile.jpg)

1.  Select the playground file

![Selecting playground file](https://res.cloudinary.com/kristofk-com/image/upload/v1567151811/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/selectFile.jpg)

## Finally, run the project

When running the project, make sure that you select a simulated device.![Selecting run device](https://res.cloudinary.com/kristofk-com/image/upload/v1567151810/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/deviceSelect.jpg)

So now you can import the framework into the playground and you can start prototyping.  
![Playground file contents](https://res.cloudinary.com/kristofk-com/image/upload/v1567151810/kristofk-com/posts/2017-11-20-xcode-9-playground-frameworks/final.jpg)

* * *

Hope, you enjoyed this tutorial, leave questions, recommendation and comments below and check back in a week for the latest post.
