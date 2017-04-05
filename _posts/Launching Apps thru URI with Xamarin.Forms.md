---
published: true
layout: post
title: Launching Apps thru URI with Xamarin.Forms
author: mindofai
date: 2017-03-30 12:00
tags: [URI, Launch, UWP, iOS, Android Xamarin, Xamarin. Forms]
---

As a developer who has always been working with Microsoft Technologies, specifically, Windows (Phone and Desktop) 8, 8.1, and UWP apps, launching other apps from an app that I'm developing is really quick and easy. All you have to do is to create a `myapp://app` Uri and launch it using `Launcher.LaunchUriAsync();` method:
```
 Uri uri = new Uri("myapp://test");
   await Windows.System.Launcher.LaunchUriAsync(uri);

But, now that I migrated to Xamarin.Forms development, obviously, this won't work for other platforms
