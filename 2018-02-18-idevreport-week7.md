---
layout: article
title: China to be the leader in A.I. – iTunes connect will be offline • iDevReport • Week 7, 2018
tags: iDevReport
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1566482256/kristofk-com/posts/2018-02-18-idevreport-week7/iDevReport7-18-thumbnail-min.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1566482256/kristofk-com/posts/2018-02-18-idevreport-week7/iDevReport7-18-thumbnail-min.png
---

This is iDevReport where I summarize the major news and events, I collect the best blog posts and award the best resources for Apple Developers. Today is Feb. 17\. and this was week 7 of 2018.

**Topics**:  
Swift  
App Store  
Security  
Become a better developer

**News highlight**:  
China is looking to be the leader in AI  
Medicin-like morality to Computer Science  
iTunes Connect will be down  
New big updates to Swift 4.1 released

This week nothing happened in terms of Apple news especially developer news. Apple seems to be too busy with moving to the new office.

<div>{%- include extensions/youtube.html id='D35fKuZ9oAg' -%}</div>

# China is looking to be the leader in AI

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566482256/kristofk-com/posts/2018-02-18-idevreport-week7/china-ai-leader-min-1024x576.png)

[The New York Times reported](https://www.nytimes.com/2018/02/12/technology/china-trump-artificial-intelligence.html?emc=edit_mbe_20180213&nl=morning-briefing-europe&nlid=78972471&te=1) that China released a manifesto and a plan to become the biggest leader in AI. This comes at a time when the US is starting to lose ground in the technological development. The Obama administration also had plans to develop the development of AI but that has since passed. The Chinese government and the city of Beijing are planning on investing large sums into the development of AI. They also have plans to teach the topic in schools and to bring in talent from outside the country.

The US seems to be doing the exact opposite. It is feared that the US government will not allow as many workers from outside the country as before and that the budget for R&D will be reduced by 15%. Meanwhile companies like Google, Facebook and Amazon are pouring money into Canada and the EU.

In Canada, Toronto has become a hotspot for AI development and companies are flocking to get their hand on talent. In the EU Amazon is investing in Germany and Facebook has spent €10 million in its Paris operations. This might just be the next big rush for the stars.

# Medicin-like morality to CS

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566482256/kristofk-com/posts/2018-02-18-idevreport-week7/medicine-vs-apps-min-1024x576.png)

The medical profession has an ethic:

> First, do no harm

Silicon Valley has an ethos:

> Build first and ask for forgiveness later

[_Source: NYTimes_](https://www.nytimes.com/2018/02/12/business/computer-science-ethics-courses.html?emc=edit_mbe_20180213&nl=morning-briefing-europe&nlid=78972471&te=1)

With the rise of machine learning and AI but no government to control it, this task is left to the creators, the next generation of Software engineers. Also with the rise of fake news on Facebook and inappropriate videos on YouTube we have to teach students the ethics and responsibilities of the new technologies. Harvard, MIT and Stanford amongst others are making courses that discuss ethics in CS. However, this is not enough!

> The set of institutions that are generationg the next generation of leaders in the technology sector have all got to get on thes train.  
> _/ – Jeremy Weistein /_

# iTunes Connect will be down

Just a quick heads up from Apple, the iTunes connect service will be down on Feb. 28\. at 6 AM Pacific Time for up to 2 hours.

# Updates in Swift

Swift has seen some new features this week. First of all, you can now compile your code so that Xcode optimises for code size rather than performance. The performance degradation is minor unless you have some kind of special use case so you might as well try it out. You can read up on this feature in a [blog post on swift.org](https://swift.org/blog/osize/?utm_source=Swift_Developments&utm_medium=email&utm_campaign=Swift_Developments_Issue_124).

The other news regarding Swift is that some developers are trying to bring Swift to windows. They have some tests that are successful so far but they are asking for more help. If you are interested you can get more information in this [blog post](https://forums.swift.org/t/state-of-windows/9778).

# Optimize the App Store

iA writer or at least a developer of iA Writer discusses some weird anomalies that he spotted in the App Store analytics. If you send traffic to the App Store, to your app, your sales will probably rise but Apple will punish you in terms of rankings. If you would like to learn more about this you can read up on [iA writer’s website](https://ia.net/writer/blog/what-happens-to-the-traffic-you-send-to-the-app-store/?utm_campaign=iOS%2BDev%2BWeekly&utm_medium=email&utm_source=iOS%2BDev%2BWeekly%2BIssue%2B339). Also, this blog post offers a solution, leave the App Store and take back control but before you do that you might want to see what Apple does with its cross-platform App Store idea, that might fix a lot of problems.

There is another [blog post from another developer](https://blog.appfigures.com/ios-11-app-store-increase-downloads/?utm_source=Swift_Developments&utm_medium=email&utm_campaign=Swift_Developments_Issue_124) that discusses the new features of the App Store and what Apple’s plans are. The blog post gives ideas on each item about how you can utilize it for yourself.

# Security for developers and consumers

[https://9to5mac.com/2018/02/13/skype-bug-grants-system-access-microsoft-too-lazy-to-fix/](https://9to5mac.com/2018/02/13/skype-bug-grants-system-access-microsoft-too-lazy-to-fix/)  
A major bug has been found in Microsoft’s Skype app for macOS. As it turns out it uses some magic to access the kernel of your machine and execute some Microsoft code there as it wouldn’t be able to do so otherwise. The problem with this approach, however, is that this leaves you mac vulnerable. Microsoft stated that it would require a whole app rewrite to fix to issue so instead of patching it they will build a better Skype app in the future.

Also, a security analytic has done some research into how a developer can be attacked and malicious code can be inserted into their app’s codebase. This might sound outlandish but this has happened multiple times before. This way all the users of your app are vulnerable. Such an attacker can gain the same access to a users phone as your app does. If you are concerned about your app’s users I recommend you read [this blog post](https://krausefx.com/blog/trusting-sdks).

# Become a better developer

You can run full apps in Xcode Playground. In a [blog post, Jussi Suojanen](http://swiftyjimmy.com/run-application-swift-playground/) discusses how he managed to run his entire swift projects on a playground. It is a little finicky to set up, you basically make your project into a Framework and then add podfiles to it and connect that to a playground. Meanwhile, my Xcode is struggling to execute functions in playgrounds.

An [open source web app](https://andresinaka.github.io/Transformer/) can help you create NSAttributed strings. The utility is basically a UI based text editor where you can type in your desired text ant the app will spit out the code for NSAttributedString in Swift of Obj-C.

In case you couldn’t attend the dotSwift conference in 2018 hosted by dotConferences, don’t be disappointed. You can still watch the videos of the talks on [their website](https://www.dotconferences.com/conference/dotswift-2018?utm_campaign=iOS%2BDev%2BWeekly&utm_medium=email&utm_source=iOS%2BDev%2BWeekly%2BIssue%2B339).

The tech lead for Google’s YouTube app on iOS, [Patrick Shyu has a YouTube channel](https://www.youtube.com/channel/UC4xKdmAXFh4ACyhpiQ_3qBw/). This itself isn’t big news but he gives very valuable insights to the development industry. He has only 3 videos so far but people are flocking to his channel. He already has over 1K subscribers so it is worth keeping an eye out.

Do you know how to get noticed as a developer and how to get an edge on interviews? [This post](https://medium.freecodecamp.org/developers-why-potential-clients-employees-ignore-you-1982d3d1186d) discusses exactly that and it boils down to these things:

*   A focused mind so you don’t become the jack of all trades and master of none.
*   Personal website… go figure
*   Tangible projects, not just the tutorial ones
*   Certificates, however, these do not prove your proficiency necessarily
*   GitHub profile, don’t use a cloud platform or some other website, use GitHub, it is the industry standard
*   Stack Overflow seems to be a legend that devs might get hired based on the questions they can answer
*   Technical posts are a great way to show you that you know what you are doing
*   A good CV for which you can use services like cvmkr.com or visualcv.com or even photoshop

# Casual Apple news

For the non-developer Apple community, this week was mostly boring.

For one the HomePod is leaving white circular marks on wooden surfaces and Apple responded that you shouldn’t use it on wood. [_Source_](https://9to5mac.com/2018/02/14/homepod-wood-crop-circles/)

There is an update on Apple’s new campus. The employees are walking into glass panes. They tried to remedy the problem by putting post-it notes on windows and doors, but those had to be taken down because they detracted from the building’s visuals. I guess Jony Ive wasn’t a fan. [_Source_](https://9to5mac.com/2018/02/16/apple-employees-walking-into-apple-park-glass/)

Apple is continuously pushing AR. Their latest move is that they created a dedicated page on the Apple website. The webpage is basically a sales page of the AR platform on iOS devices. [_Source_](https://www.apple.com/ios/augmented-reality/)
