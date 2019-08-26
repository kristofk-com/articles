---
layout: article
title: Cryptocurrency Mining on an iPhone
tags: AppleStuff
---

In this post I’ll be discussing how can one mine cryptocurrency on an iPhone and I’ll be demonstrating it by mining some Electroneum. Spoiler alert, you won’t get rich by mining on phones.

Alright, so let’s start by talking a little about what a cryptocurrency is and what is Electroneum specifically? Wikipedia tells us that cryptocurrency is a digital asset designed to work as a medium of exchange that uses cryptography to secure its transactions, to control the creation of additional units, and to verify the transfer of assets.

So basically a cryptocurrency is money that is independent of any government and business, it is based on blockchain.

So what is Electroneum? Electroneum is a cryptocurrency developed in UK which means nothing, but what is more interesting is that it is easier to get into Electroneum than any other cryptocurrency. It has all the features that a popular cryptocurrency like Bitcoin would have and it is as easy as signing up on the Electroneum website.

Alright so in order to set up an iPhone as a mining device we will need an Electroneum account unless you want to mine for the developer. Although you won’t get or make anyone rich.

If you do decide to create an Electronium account then go to https://electroneum.com -> log in -> Create a new account and follow the steps and you’ll land in your wallet. From here you’ll need to remember one string, the one under the QR code that is your public wallet address. It is safe to share this with anyone as it can only be used to send you Electronium.

Alright so now let’s start setting up our iPhone. The app we are going to use to mine Electroneum is called MobileMiner. This app cannot be downloaded from the App Store so we’ll have to sideload it.

## Prerequisites

*   Developer Apple ID, this is free to create, the only downside is that you will need to reinstall any app after 7 days
*   Xcode downloaded, this can be done from the Mac App Store
*   iOS App signer, this can be downloaded from the web

### Downloading Xcode

I am going to make it very simple for you to download Xcode, just click on this [link](https://itunes.apple.com/us/app/xcode/id497799835?mt=12) and then download the app.

### Setting up a Developer Apple ID

A Developer Apple ID is nothing more than an Apple ID Signed into Xcode. In order to sign into Xcode with your Apple ID go to Xcode -> Preferences ( cmd + , ). Then on the Accounts tab clock on the ‘+’ and sign in to your Apple ID.

### Downloading iOS App signer

In order to download iOS App Signer go to [this link](https://dantheman827.github.io/ios-app-signer/) and click download.

## Setting up MobileMiner

This is the hardest part, so I’ll break this one up into multiple sections.

### Downloading the IPA file and the project

The project can be found on GitHub, which is a website for developers to share code and projects. Go to [this link](https://github.com/limneos/MobileMiner). Then download the ZIP file. After that download the IPA file by scrolling down on the page until you find “Compiled iOS App” or alternatively you can use [my link](http://www.mediafire.com/file/f6qzt8jv26wtqm6/MobileMiner.ipa) which links to the same page.![](https://res.cloudinary.com/kristofk-com/image/upload/v1566803400/kristofk-com/posts/2017-12-24-crypto-currency-mining-on-an-iphone/Screenshot-2017-12-24-12.10.05-min.png)

### Getting the provisioning profile

Ok so don’t worry about what a provisioning profile is. Just unpack the downloaded ZIP file by clicking on it and then in the folder, there is going to be a file that has a .xcodeproj extension. Open that file and Xcode should open. Now you need to clock on the project and under signing, you need to select your apple id and change the bundle identifier to “com.<your name>.MobileMiner. And select try again. Now the error should disappear and you can close Xcode.

### Signing the IPA file

Now open up the iOS App Signer. Fill in the form with the following info:

*   **Input file**: The IPA file you downloaded earlier
*   **Signing Certificate**: Your Apple ID
*   **Provisioning Profile**: The one that you have generated just now, the one that ends with “.MobileMiner”

The rest of the options don’t matter, all there is left to is press start, select a name and an output folder. I choose my download folder and for the name, I choose “MobileMiner1.ipa”.

![](https://res.cloudinary.com/kristofk-com/image/upload/v1566803400/kristofk-com/posts/2017-12-24-crypto-currency-mining-on-an-iphone/Screenshot-2017-12-24-12.57.39-min.png)

## ![](https://res.cloudinary.com/kristofk-com/image/upload/v1566803400/kristofk-com/posts/2017-12-24-crypto-currency-mining-on-an-iphone/Screenshot-2017-12-24-12.58.03-min.png)

## Installing MobilMiner on any iOS Device

Now plug your iPhone into your computer. Back in Xcode select Window -> Devices and Simulators and you’ll see your device. Select it and after pressing ‘+’ select the IPA file you have just created with the iOS App Signer tool. This will install it on your iDevice.

Now you’ll see the app on your iPhone but you won’t be able to open it. In order to do that you’ll need to go to Settings -> General -> Device Management and trust your developer account aka your email address.

## Start Mining!

Now within the app go to settings -> Edit Configurations -> Edit -> Add New and edit the following fields:

*   Configurations name: Whatever you want
*   Username/Address: Copy-Paste your Electroneum wallet address here

Don’t worry about the rest, now you can select done.

Now click on Active Configuration and select the one that you have just created.

Now click Start Mining! and you are off to the races.

* * *

That is all you need to do in order to start mining on your iPhone.
