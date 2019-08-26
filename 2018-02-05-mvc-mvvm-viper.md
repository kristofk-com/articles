---
layout: article
title: Architectural patterns, MVC, MVVM… What is the hype all about?
tags: SwiftDevelopment
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1566583873/kristofk-com/posts/2018-02-05-mvc-mvvm-viper/thumbnail-for-mvvm-min.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1566583873/kristofk-com/posts/2018-02-05-mvc-mvvm-viper/thumbnail-for-mvvm-min.png
---

For about a solid year now more and more blog posts and discussions are arising about architectural patterns within iOS Development. Developers are using a variety of these patterns and they are writing about them, why it is better and how it could improve the app development process.

Currently, Apple advises us, developers to use the MVC pattern in our Apps while most of these devs I talked about earlier are endorsing a pattern called MVVM and sometimes Viper. So what is all the craze about?

<div>{%- include extensions/youtube.html id='KRN76e44NAc' -%}</div>

# What is an Architectural Pattern?

An architectural pattern within the code base of an app is the separation of objects and files, it is the structure of the app’s code. There are virtually endless possibilities but there are a few that the dev community agreed upon. So what are the **qualities of a good patter**?

*   Balanced **distribution** of responsibilities among entities with strict roles.
*   **Testability** usually comes from the first feature (and don’t worry: it is easy with appropriate architecture).
*   **Ease of use** and a low maintenance cost.

Most patterns are included in the MV(X) family meaning that an app has a Model a View and something else.

# So what is wrong with MVC?

At this point, you might be asking this question? I mean, Apple recommends it, developers have been using it for some time now so why is there any talk about a change.

## Little MVC history

The MVC pattern comes from a [paper](http://folk.uio.no/trygver/2007/MVC_Originals.pdf) published in 1979 about an architecture for apps with UI in the centre of it. This original architecture wasn’t exactly polished. It violated some of the principles we know in iOS Development today like the decoupling of objects and single responsibility. So battle these shortcomings Apple made some changes to the pattern and created the MVC pattern we know today, they write about it in the [Official Apple Documentation](https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html).

## Shortcomings of MVC

You might have heard of this, there is another meaning of MVC other than Model View Controller and that is Massive View Controller. This is the main issue with MVC. I bet that you have run into this problem before, that the ViewController class in your app is the biggest, it is the delegate and data source for everything, it includes the business logic too and it is very tightly coupled with the View itself. This is bad because a large number of objects makes the code unmaintainable and the close relation to the View and UI objects makes this class very hard to test.

I mean if you read the Official Apple Documentation then you’ll see that the way Apple designed MVC is good, it looks like this:![Apple's MVC in theory](https://res.cloudinary.com/kristofk-com/image/upload/v1566583872/kristofk-com/posts/2018-02-05-mvc-mvvm-viper/apple-mvc-min-300x124.png)

However, instead of that, we got a pattern that more closely represents this:![Apple's MVC in reality](https://res.cloudinary.com/kristofk-com/image/upload/v1566583872/kristofk-com/posts/2018-02-05-mvc-mvvm-viper/apple-mvc-reality-min-300x97.png)

So for the reasons above some developers are coming up with alternate solutions. They are looking for architecture patterns that we can use in place of the MVC pattern. And it looks like they found a few solutions.

# MV(X) patterns

These are the Architecture patterns that include a Model, View and something else. These patterns resemble the MVC pattern closely. The most popular ones are **MVP** and **MVVM**.

So let’s look at the generals, the things that these patterns share and have in common:

*   **Model:** responsible for the domain data or a data access layer which manipulates the data. Objects and business logic can come here.
*   **View:** responsible for the presentation layer (GUI), for iOS environment think of everything starting with the ‘UI’ prefix.
*   **Controller, Presenter, ViewModel:** the glue or the mediator between the Model and the View, in general, responsible for altering the Model by reacting to the user’s actions performed on the View and updating the View with changes from the Model.

## **MVP**

![Passive View variant of MVP](https://res.cloudinary.com/kristofk-com/image/upload/v1566583872/kristofk-com/posts/2018-02-05-mvc-mvvm-viper/Passive-View-variant-of-MVP-min-300x92.png)

Passive View variant of MVP

![Supervising Presenter variant of the MVP](https://res.cloudinary.com/kristofk-com/image/upload/v1566583872/kristofk-com/posts/2018-02-05-mvc-mvvm-viper/Supervising-Presenter-variant-of-the-MVP-min-300x115.png)

Supervising Presenter variant of the MVP

In this pattern, we have a presenter as the median between the Model and the View. This pattern introduces the idea that the View and the ViewController together make up the View part of the pattern and this way the presenter doesn’t have to include any layout code and so the life cycle of the Presenter is completely separate that of the View. The presenter is independent of UIViewController meaning that there is no inheritance. The presenter, however, is responsible for updating the view. There is a good code example for this and all the other patterns for that matter on [this blog post](https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52). So let’s summarise how good MVP is an architecture pattern:

*   **Distribution:** We have a very dumb view, meaning that the code is mostly divided between the Model and the presenter.
*   **Testability** is superb, because of the single responsibility and well-separated classes automated testing and unit testing is easier to write.
*   **Ease of use:** Despite the fact that there is more code to write, this pattern is actually easier to work with.

It is true that it isn’t worth using this type of pattern for very small apps because of the amount of code you have to write over what you would normally write in an app with the MVC pattern.

## MVVM

![MVVM diagram](https://res.cloudinary.com/kristofk-com/image/upload/v1566583872/kristofk-com/posts/2018-02-05-mvc-mvvm-viper/mvvm-diagram-min-300x91.png)

This is the latest and the greatest of the bunch. This pattern like the previous one treats the ViewController class and the Views together as the View itself. So what is the ViewModel then, well it is the UIKit independent representation of the View. This pattern is compatible with already established MVC pattern following apps. This means that you can simply move most of your code out of the ViewController class into the ViewModel and the Model parts of the app. This is the patter I’d recommend you use instead of MVC and for both smaller and great apps regarding the size of the code base.

## Viper

![Viper diagram](https://res.cloudinary.com/kristofk-com/image/upload/v1566583873/kristofk-com/posts/2018-02-05-mvc-mvvm-viper/viper-diagram-min-300x133.png)

This Architectural patter is the most complex out of all the ones out there. This pattern divides the code base into more than 3 parts, meaning that you need to constantly look out where you put your code. Viper is mostly used in great projects with lots of users and an immense amount of code. Viper is an advanced pattern that I don’t recommend for beginners. With Viper, you are forced to write way more code than with any of the other patterns making the maintenance hard and costly. This pattern should not be used in small projects unless there is a clear benefit to it maybe in the future.

## Conclusion

So I have read in one of the blog posts during the preparation for this one that MVC should be used as a guideline. It has great principles, values and ideas that we can definitely incorporate into our apps but that is it. It shouldn’t be used as the Architecture of our apps. I agree with this statement.

However, I also read that MVVM isn’t enough either. That we should break up the ModelView into smaller parts. That blog post didn’t talk about Viper, however. We must remember that while MVVM has a lot to offer if we abuse it and force viper onto a pattern like MVVM we make an even worse monster than if we did nothing.

When committing to a project decide the architecture and stick with it. If you have a small team or if you are the team and the app isn’t so big then don’t overcomplicate things with viper. Just use MVVM and forget about it. We, developers, tend to overthink and overcomplicate somethings sometimes, so lets not so that here. I even dare to say that it is not the pattern that matters but rather that we choose one and consistently stick with it.

* * *

Sources highlight:

*   [Break down of the original MVC paper](https://badootech.badoo.com/do-mvc-like-its-1979-da62304f6568)
*   [iOS Architectural Patterns](https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52)
*   [Apple Official Documentation – MVC](https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html)
