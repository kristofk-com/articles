---
layout: article
title: iDev Report 6/18
tags: iDevReport
article_header:
  type: cover
  image:
    src: https://res.cloudinary.com/kristofk-com/image/upload/v1566482710/kristofk-com/posts/2018-02-12-idevreport-week6/iDevReport6-18-thumbnail-min.png
cover: https://res.cloudinary.com/kristofk-com/image/upload/v1566482710/kristofk-com/posts/2018-02-12-idevreport-week6/iDevReport6-18-thumbnail-min.png
---

Welcome to the first iDev Report of the week. This post will summarise everything that happened with Apple mainly focusing on topics that affect Apple developers. This is the summary of week 6 of 2018.

<div>{%- include extensions/youtube.html id='whIDMi7tjZA' -%}</div>

# Main news stories

## Apple rejecting apps that have emojis in the UI

![Where not to place emojis](https://res.cloudinary.com/kristofk-com/image/upload/v1566482709/kristofk-com/posts/2018-02-12-idevreport-week6/iDevReport6-18_4C_1-1024x600.jpg)

Some developers have come forward that their apps and updates are being rejected by Apple because they have used emojis in the UI and/or the marketing material shows this. If the emoji appears somewhere where the user can type it then it is fine. However, Apple doesn’t seem to be consistent with this rule. Some apps are accepted while others are rejected and some apps are accepted after the 1st try. This will need to be addressed by Apple.

[https://9to5mac.com/2018/02/02/apple-rejecting-apps-with-emoji/](https://9to5mac.com/2018/02/02/apple-rejecting-apps-with-emoji/)  
[https://blog.emojipedia.org/apples-emoji-crackdown/](https://blog.emojipedia.org/apples-emoji-crackdown/)

## iPhone X users are unable to receive calls

![iPhone X calling issue](https://res.cloudinary.com/kristofk-com/image/upload/v1566482709/kristofk-com/posts/2018-02-12-idevreport-week6/iDevReport6-18_5c_1.jpg)

Users of the new iPhone X are reporting a software bug that is causing the display to not wake up when they are receiving a call causing theme to not be able to pick up the phone. This also happens when they take the phone away from their face the screen doesn’t wake up. Apple is investigating the situation but stable software update to fix the issue is yet to come.

[Growing number of iPhone X users unable to accept calls, Apple investigating](https://9to5mac.com/2018/02/04/iphone-x-cant-answer-calls-issue/)

## Developers wrongfully getting emails about ad statistics of other apps

This year a considerable amount of developers have stated that they received emails about app ad statistics in the App Store. The catch is that these apps were not theirs. Apple has since sent out emails to the affected developers as to what happened and that it was an internal server error and that this won’t happen in the future. The information that Apple sent out can be sensitive especially for competition.

> [Did anyone else get an Apple Search Ads summary for a random app made by someone else?](https://www.reddit.com/r/iOSProgramming/comments/7vmkzm/did_anyone_else_get_an_apple_search_ads_summary/?ref_source=embed&ref=share) from [iOSProgramming](https://www.reddit.com/r/iOSProgramming/)

> [Apple says a processing error led it to send developers wrong app install and ad spend details](https://techcrunch.com/2018/02/07/apple-says-a-processing-error-led-it-to-send-developers-wrong-app-install-and-ad-spend-details/)

<iframe class="wp-embedded-content" sandbox="allow-scripts" security="restricted" style="position: absolute; clip: rect(1px, 1px, 1px, 1px);" src="https://techcrunch.com/2018/02/07/apple-says-a-processing-error-led-it-to-send-developers-wrong-app-install-and-ad-spend-details/embed/#?secret=RWiMdlnpNq" data-secret="RWiMdlnpNq" title="“Apple says a processing error led it to send developers wrong app install and ad spend details” — TechCrunch" marginwidth="0" marginheight="0" scrolling="no" width="750" height="422" frameborder="0"></iframe>

## HomePod released

This week Apple released the HomePod and the review floodgates were opened. The consensus seems to be that they could be louder but the sound quality is great. If you have been thinking of implementing Siri into your Apps then there has never been a better time. As of right now, SiriKit isn’t supported by the HomePod, but it is coming later on.

[https://developer.apple.com/sirikit/](https://developer.apple.com/sirikit/)

[https://www.apple.com/homepod/](https://www.apple.com/homepod/)

## Apple released new beta software across the board

All of the Apple operating systems have received a new beta version, that includes macOS, tvOS, whatchOS and iOS. The new big thing in iOS is the battery testing tool. It is a bit simple but it does the job. Also, the code in the iOS software hints to ClassKit which isn’t mentioned anywhere on Apple’s developer website so it is probably not ready for prime time. Here are the roundups of all the new features: [iOS](https://www.youtube.com/watch?v=oLoOJ_a9sIE), [tvOS](https://9to5mac.com/2018/02/06/tvos-11-3-beta-2/), [macOS](https://9to5mac.com/2018/02/06/macos-10-13-4-beta-2/).

# Articles

## White paper on iCloud

A newly published academic paper shows how iCloude has been designed and built to accommodate nearly a billion users. This paper is very technical so if you aren’t educated on the web and networks don’t even bother. But if you enjoy learning about web infrastructure then have a go at it.

[http://www.vldb.org/pvldb/vol11/p540-shraer.pdf?utm_campaign=iOS%2BDev%2BWeekly&utm_medium=email&utm_source=iOS_Dev_Weekly_Issue_338](http://www.vldb.org/pvldb/vol11/p540-shraer.pdf?utm_campaign=iOS%2BDev%2BWeekly&utm_medium=email&utm_source=iOS_Dev_Weekly_Issue_338)

## All possible App revenues

Tamoco has released a blog post on their website detailing all the possible ways an app can make money. It is a really interesting read if you are in the app market. If you have been thinking on how to make money of off your app or if you want to boost your revenues then I’d recommend you read it.

[https://www.tamoco.com/blog/ultimate-app-monetization-guide?utm_campaign=iOS%2BDev%2BWeekly&utm_medium=email&utm_source=iOS_Dev_Weekly_Issue_338](https://www.tamoco.com/blog/ultimate-app-monetization-guide?utm_campaign=iOS%2BDev%2BWeekly&utm_medium=email&utm_source=iOS_Dev_Weekly_Issue_338)

# Finally

## nocode

If you want to participate in the development of one of the largest apps you should go to this GitHub repo. There is a lively bunch of coders helping out I wouldn’t want to miss out if I were you.
