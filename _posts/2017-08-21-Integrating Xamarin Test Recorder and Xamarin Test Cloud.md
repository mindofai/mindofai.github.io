---
published: false
layout: post
title: Integrating Xamarin Test Recorder and Xamarin Test Cloud
author: mindofai
date: 2017-08-21 12:00
tags: [Xamarin Test Recorder, Xamarin Test Cloud, Xamarin UI.Test, iOS, Android, Automated Testing, Microsoft, UWP, Xamarin, Xamarin. Forms]
---


Back in 2009, there’s this Apple slogan that says, ’There’s an app for that’ and boom, 1, 2, 3 apps popped out in the marketplaces. And now, 7-8 years later, it happened more and more. Thousands of apps are out there. There’s almost an app for everything, may it be snack size or enterprise applications. Any functionality that you can imagine (well, not really, but you get the point). 

As developers, we have to move quickly. The competitions out there and they’re ready to replace us in the app store. We can’t afford to break anything and to do that, writing code is no longer enough. We have to test them before we release them in the public. We have to make sure that all important flow is working. The app is not crashing and it looks just like how we want it on all devices and OS versions, because users have crazy expectations. 

Yes, it’s easy to say that what we need to constantly test our application, but it consumes so much of our time doing these repetitive testing just to get the bare minimum viable quality. And it’s not just because of repetitiveness, but the complexity is extraordinary. I’m talking about the amount of devices that you need to satisfy. For iOS, there are numerous, iPhone 5, 5s, 6, 6s, 7, and even the iOS version. But, if we talk about android devices. There are thousands out there. Different make, size, version, etc. It’s practically impossible to cover all of them.

Some of Xamarin developers out there might have implemented an automated testing using Xamarin.UITest, if you’re one of them, that’s really awesome! But, as developers, we want to focus on the app development instead of creating codes for tests. Microsoft have something to offer that will make your mobile app testing so much easier and so much better. I’m talking about Xamarin Test Recorder. It’s a tool where you can simply interact with your app as you normally would with taps, swipes, and gestures, and it records each step. The output is the Xamarin.UITest code test script without writing a single line of code. All you need is Xamarin Test Recorder, an Android/iOS emulator, and your application’s .apk/.ipa file.
