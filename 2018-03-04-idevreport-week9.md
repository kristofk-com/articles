---
layout: article
title: Releases from Apple & Google • iDevReport • Week 9, 2018
tags: iDevReport
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1566386721/kristofk-com/posts/2018-03-04-idevreport-week9/idevreport9-18-thumbnail-min.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1566386721/kristofk-com/posts/2018-03-04-idevreport-week9/idevreport9-18-thumbnail-min.png
---

This week some releases happened, some leaks surfaced and the EU is about to update their regulations regarding the handling of users’ data.

This week’s sections:

*   News
*   Blog posts & Articles
*   Releases
*   Casual Apple news

<div>{%- include extensions/youtube.html id='QND411ZKSEM' -%}</div>

# News

## [Updates to GDPR aka General Data Protection Regulation](https://www.smashingmagazine.com/2018/02/gdpr-for-web-developers/?utm_campaign=iOS%2BDev%2BWeekly&utm_medium=email&utm_source=iOS%2BDev%2BWeekly%2BIssue%2B341)

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566379130/kristofk-com/posts/2018-03-04-idevreport-week9/Screenshot-2018-03-04-11.23.png)

Heather Burn wrote about [this](https://www.smashingmagazine.com/2018/02/gdpr-for-web-developers/?utm_campaign=iOS%2BDev%2BWeekly&utm_medium=email&utm_source=iOS%2BDev%2BWeekly%2BIssue%2B341), that new updates are coming to GDPR and she sums it up nicely. This update has the potential to affect every developer regardless of location. Noncompliance may have very bad consequences. The rules aren’t all that bad rather they are sensible. As a developer the most relevant item in it is that documentation is the key, you need to document everything. As a team lead or a manager you will need to know what to document in addition.

# [New screenshots about ClassKit](https://9to5mac.com/2018/03/01/preferences-for-apple-upcoming-classkit-framework/)

New screenshots have surfaced that show the settings tab of ClassKit, both for students and teachers. The origin of the images is unknown and originally [9to5mac reported](https://9to5mac.com/2018/03/01/preferences-for-apple-upcoming-classkit-framework/) on this and then every other news site copied. There is no weight to this report it is just interesting and I thought I’d share it.

## [Concept art for the Universal apps on macOS](https://9to5mac.com/2018/03/01/macos-11-concept-gallery/)

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566379118/kristofk-com/posts/2018-03-04-idevreport-week9/screen-shot-2018-03-01-at-1-51-40-pm-1024x576.jpg)

Álvaro Pabesio released a series of images that depict how the cross-platform apps on macOS could look like. He went a bit too far and redesigned macOS itself in some places. Non the less this is a great resource to take inspiration from. Just like the previous story, this has no weight to it, it is more entertainment.

# Releases

## [SwiftNIO – Network driven application from Apple](https://github.com/apple/swift-nio)

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566379118/kristofk-com/posts/2018-03-04-idevreport-week9/Screenshot-2018-03-04-11.24.png)

According to Apple:

> SwiftNIO is a cross-platform asynchronous event-driven network application framework for rapid development of maintainable high performance protocol servers & clients.

For an iOS Developer, this doesn’t mean much but rather for low-level back-end web developers. An interesting thing about the announcement of the framework is that it wasn’t done at an Apple event. It was introduced in TOKYO try! Swift.

## [Flutter – UI designing tool from Google](https://medium.com/flutter-io/announcing-flutter-beta-1-build-beautiful-native-apps-dc142aea74c0)

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566379120/kristofk-com/posts/2018-03-04-idevreport-week9/header-illustration.png)

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566379110/kristofk-com/posts/2018-03-04-idevreport-week9/flutter-mark-square-100.png) Flutter is a utility that you can use to design the UI of cross-platform apps. This utility generates native UI elements and compiles down to native code yet it is simple to use and has powerful features. I’ll have to see what it can do in real life but the demos look great.

# Blog posts & Articles

## [WatchKit produces baby apps](https://marco.org/2018/02/26/watchkit-baby-apps)

Marco Arment wrote a blog post that that details his deja vu feeling towards WatchKit. He compares it to the 2007 iPhone launch. He goes on to talk about why he thinks WatchKit is inadequate and offers solutions as well. This is an interesting short read.

## [Introductory prices on the App Store](https://medium.com/revenuecat-blog/ios-introductory-prices-f1efb4f1a6a2)

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566379115/kristofk-com/posts/2018-03-04-idevreport-week9/1VjtXn7UbNiHHGAsqhGBudg.png)

Apple has introduced a new subscription type to complement the already existing one. Meet introductory prices. Introductory prices allow your users to not pay the full price of a subscription but have a demo rather. There are multiple styles you can implement with different advantages so I recommend you check it out.

## [Spotlight support on iOS](https://hackernoon.com/how-to-add-spotlight-support-to-your-ios-app-4a89054aff89)

The spotlight is one of my favourite tools on the Mac. While the iOS version of spotlight search is not as useful but it is just as powerful especially if you implement it within your app. Implementing Spotlight search into your app is a great way to keep your app relevant. If you want to learn more about how to do this, then make sure to read up on the blog post.

## Libraries

## [Repeat – Modern alternative to NSTimer in Swift](https://github.com/malcommac/Repeat)

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566379119/kristofk-com/posts/2018-03-04-idevreport-week9/Screenshot-2018-03-04-11.26.png)

> Repeat is small lightweight alternative to `NSTimer` with a modern Swift Syntax, no strong references, multiple observers reusable instances. Repeat is based upon GCD – Grand Central Dispatch.

This library is super easy to use, the code is very short and elegant. This might just replace NSTimer altogether.

The author of the Repo on GitHub also released a [post on Medium](https://medium.com/@danielemargutti/the-secret-world-of-nstimer-708f508c9eb) about the library and getting started with it.
