---
published: true
layout: post
title: Creating Native macOS Apps with Xamarin.Forms
author: mindofai
date: 2017-010-11 12:00
tags: [macOS, Cocoa App, Xamarin.Forms 3.0, Visual Studio, Mobile, iOS, Android, Xamarin, Xamarin. Forms]
---

<img src="{{site.baseurl}}/MAC-01.png"/>


Back in .NET Conf 2017 The Xamarin team already shared what’s going to be new with **Xamarin Forms 3.0** and it actually surprised me. I was expecting some performance improvements, bug fixing and a big upgrade on XAML. But, what they announced focuses on enabling the usage of Xamarin.Forms in more ways and on more platforms. I was really hoping for XAML improvements, maybe add some cascading styling like how CSS works. Maybe sometime in the future, we’ll get it. For now, I’ll just use the [**XAMLCss by warapa**](https://github.com/warappa/XamlCSS). Anyway if you want to watch all sessions from .NET Conf 2017, you can check it out on [**Channel9**](https://channel9.msdn.com/Events/dotnetConf/2017). Going back, I really didn’t expect these new features, but definitely, I love it and really excited to try it out!

That’s why right now, I’m going to show to you one of the exciting features added to the **Xamarin.Forms 3.0** that I think you’ll also love. I’m talking about Xamarin.Form’s **macOS** support.

# Reaching more platforms


One of the Xamarin team’s plan is to reach more platforms. That means UWP, iOS and Android are not only platform the Xamarin.Forms will be able to target from now on, they are also bringing **macOS, GTK#, Linux and WPF**!

<img src="{{site.baseurl}}/MAC-02.png" height="350"/>

You might think that it will be hard and will take a lot of time to integrate your Xamarin.Forms solution into the macOS project, but it’s not. Not at all. You’ll be able to create a native macOS application using your Xamarin.Forms solution using **Visual Studio for Mac** or **Xamarin Studio** in just **3 quick steps**!

## First step: Add a Cocoa App project

Right now, Xamarin.Forms template doesn’t have a **Cocoa App** initially. So, what you would do is to start Visual Studio for Mac or Xamarin Studio and open your existing Xamarin.Forms solution. Then, add a project into the solution by right-clicking the solution and selecting *Add > Add New Existing Project*. 

<img src="{{site.baseurl}}/MAC-03.png" height="300"/>

You can then select *Mac > App > Cocoa App* and name it whatever you want, but ideally, the name has a suffix of **.macOs**.

<img src="{{site.baseurl}}/MAC-04.png" height="500"/>

<img src="{{site.baseurl}}/MAC-05.png" height="500"/>

## Second Step: Add the Xamarin.Forms NuGet Package

You will have to add the Xamarin.Forms’ latest pre-release nuget package or specifically [**2.4.0.282**](https://www.nuget.org/packages/Xamarin.Forms/2.4.0.282). To do this, right click the Cocoa App project that you just created and select *Add > Add Nuget Packages*.

<img src="{{site.baseurl}}/MAC-06.png" height="300"/>

Then, search for 'Xamarin.Forms' and make sure that the *‘Show pre-release packages’* is ticked. Click 'Add' to add Xamarin.Forms nuget package.

<img src="{{site.baseurl}}/MAC-07.png" height="500"/>

You will also need to update the Xamarin.Forms on your shared project and the version should be the same with what the Cocoa app have.


## Third Step: Configure the Cocoa App Project

The first thing that you should do with your Cocoa app project is to add the shared project into your Cocoa app as a reference. 

<img src="{{site.baseurl}}/MAC-10.png" height="200"/>

<img src="{{site.baseurl}}/MAC-11.png" height="250"/>

Then, open the Info.plist and remove the *‘Main storyboard file base name’ entry (Opened with XCode)* 

<img src="{{site.baseurl}}/MAC-08.png" height="300"/>

Or just open the Info.plist inside Visual Studio or Xamarin Studio by clicking it and leave the *Main Interface* blank. 

<img src="{{site.baseurl}}/MAC-09.png" height="300"/>

The next one is to update your **Main.cs’ Main method** to initialize the **AppDelegate**:

```
static void Main(string[] args)
{
NSApplication.Init();
NSApplication.SharedApplication.Delegate = new AppDelegate();
NSApplication.Main(args);
}
```

Lastly, update the AppDelegate by changing the **NSApplicationDelegate** to **FormsApplicationDelegate**:

```
public class AppDelegate : FormsApplicationDelegate
```

Initialize the Cocoa app window within the constructor:

```
NSWindow _window;

public override NSWindow MainWindow
{
   get { return _window; }
}


public AppDelegate()
{
   var style = NSWindowStyle.Closable | NSWindowStyle.Resizable | NSWindowStyle.Titled;

   var rect = new CoreGraphics.CGRect(200, 200, 800, 600);
   _window = new NSWindow(rect, style, NSBackingStore.Buffered, false);
   _window.Title = "Mind of Ai";
}
```

Then inside the **DidFinishLaunching** method, initialize Xamarin.Forms and load the application:

```
public override void DidFinishLaunching(NSNotification notification)
{
   Forms.Init();
   LoadApplication(new App());
   base.DidFinishLaunching(notification);
}
```

You can now set your project as the startup project and run your macOS! 


<img src="{{site.baseurl}}/MAC-12.png" height="500"/>


<img src="{{site.baseurl}}/MAC-13.png" height="500"/>



Again, in just 3 quick steps, it’s done!

# Wrapping up

This is just a basic walkthrough since this is still on **preview**. Expect that there are still bugs and not ready for production. Not all nuget packages are compatible and surely, there are lots of UI features still not implemented, but this is a good start. For now, you can send your issues and problems that you encounter in this forum discussion: [https://forums.xamarin.com/discussion/93585/preview-xamarin-forms-for-macos/p1](https://forums.xamarin.com/discussion/93585/preview-xamarin-forms-for-macos/p1)
