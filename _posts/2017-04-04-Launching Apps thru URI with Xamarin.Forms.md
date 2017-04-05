---
published: true
layout: post
title: Launching Apps thru URI with Xamarin.Forms
author: mindofai
date: 2017-04-04 12:00
tags: [URI, Launch, UWP, iOS, Android Xamarin, Xamarin. Forms]
---

As a developer who has always been working with Microsoft Technologies, specifically, Windows (Phone and Desktop) 8, 8.1, and UWP apps, launching other apps from an app that I'm developing is really quick and easy. With just two lines of code, you can execute external apps which is installed to your device or machine. All you have to do is to create a `myapp://app` Uri and launch it using `Launcher.LaunchUriAsync();` method:

```csharp
 Uri uri = new Uri("myapp://app");
   await Windows.System.Launcher.LaunchUriAsync(uri);
```

Two lines of code. As easy as that.

But, now that I migrated to Xamarin.Forms development, obviously, this won't work for other platforms. So, I looked for ways to do this and I found [this forum thread](https://forums.xamarin.com/discussion/48089/how-to-open-other-apps-from-xamarin-forms).

I saw Jordan Hewitt's reply to the thread and he shared how you can do it with both Android and iOS and it's quite easy. There will be different implementations for each platforms, meaning we'll have to use [Dependency Injection](https://developer.xamarin.com/guides/xamarin-forms/application-fundamentals/dependency-service/)  to create an implementation. 

First, you should create an interface for the OpenApp, then create a `Launch()` method that we'll call later:

```
public interface IOpenApp
{
    Task<bool> Launch(string Uri);
}
