---
published: true
layout: post
title: Trying Out Xamarin Live Player
author: mindofai
date: 2017-05-28 12:00
tags: [Debugging, Xamarin Live Player, Live Player, Preview, Visual Studio, Mobile, iOS, Android, Xamarin, Xamarin. Forms]
---

<img src="{{site.baseurl}}/XLP-1.png"/>

So, I'm already kinda late with this. It's been almost 3 weeks since Build 2017 happened in Seattle and I just finished watching some of the highlights on [Channel 9](https://channel9.msdn.com/Events/Build/2017), especially all the things relevant to Xamarin and Mobile .NET. I've read that Xamarin had a bunch of sessions where they announce awesome stuff and I was really interested and excited about a couple of things, namely Xamarin Live Player, Visual Studio Mobile Center, .NET Standard and Fluent Design. I will write a different article about other the other three, but we'll start talking about Xamarin Live Player.

# Xamarin Live Player

Visual Studio 2017's brand-new [Xamarin Live Player](https://www.xamarin.com/live?utm_medium=Blog&utm_source=Xamarin_blog_5_11_MI&utm_campaign=msbuild_2017) for Android and iOS allows you to write, execute, and debug your Xamarin application continuously on an actual iOS or Android device straight from the IDE. It has the traditional development cycle where you write-compile-run-debug, but it's so much faster. But, what I loved about it is that it has a live previewer mode where your code is automatically compiled and deployed per-view basis continuously into your actual device. It's pretty awesome, though, this is not new to me, since Gorilla Player almost identically does the same stuff, but I prefer Xamarin Live Player since the setup is much easier.


<img src="{{site.baseurl}}/XLP-2.png"/>

# Getting started

So, what I want to show to you is how you can actually use Xamarin Live Player. From installation to running a blank app into your device with Xamarin Live Player's live preview mode. Since we can only try out Xamarin Live Player using Visual Studio 2017 Preview (15.3), we'll need to start from the actual installation of Visual Studio 2017 Preview, but ideally, if 15.3 becomes generally available, you can skip the installation step and just make sure that your Visual Studio 2017 is updated.

# Visual Studio 2017 Preview Installation

First, you need to install the Visual Studio 2017 Preview ([For Windows](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-preview-relnotes)/[For Mac](https://developer.xamarin.com/recipes/cross-platform/ide/change_updates_channel/#xamarinstudio)). If you already have a Visual Studio 2017 installed, don't worry, this is a different one. You can actually run the currently-installed Visual Studio 2017 and this one side-by-side, meaning they're not the same application. Make sure that the Visual Studio 2017 version you're installing is 15.3. The only workload you need to install is ofcourse Cross-Platform Development. It wiss ask you for the installation nickname, you can just name it `153Preview` or whatever you like. The installation will take a while.

<img src="{{site.baseurl}}/XLP-3.png"/>

After the installation, this is what you will see on your Visual Studio Installer. There will be two different Visual Studio 2017 application as you can see below:

<img src="{{site.baseurl}}/XLP-4.png"/>

# Get Xamarin Live Player Up and Running

 we can now start setting up the Xamarin Live Player. This means that Xamarin Live Player isn't installed and ready to use right away. You will still have to do a couple of things to get it up and running.

## Install Xamarin Updater

First, we need to install Xamarin Updater which provides us out of band updates to Xamarin for Visual Studio 2017 or later. Open your Visual Studio 2017 Preview and select Tools > Extension and Updates. Select Online and search for "Xamarin Updater" and download Xamarin Updater. After downloading, you will have to close your Visual Studio to install the Xamarin Updater.

<img src="{{site.baseurl}}/XLP-5.png"/>

## Xamarin Preview Updates

Once installed, you can go back to Tools > Extension and Updates. Select Updates and then Xamarin Previe node. This gives you the list of stuff you can update for Xamarin. What yo need to update specifically is the Xamarin for Visual Studio. Click update and once done, you will have to close your Visual Studio again to install the updates. 

<img src="{{site.baseurl}}/XLP-6.png"/>

Then, we'll have to re-open Visual Studio again. Our Visual Studio is ready. Let's now set up our devices!

<img src="{{site.baseurl}}/XLP-7.png"/>

## Installing Xamarin Live Player Application

This one's pretty straightforward, you just need to install the Xamarin Live Player application into your device ([iOS](https://itunes.apple.com/us/app/xamarin-live-player/id1228841832?ls=1&mt=8)/[Android](https://play.google.com/store/apps/details?id=com.xamarin.live)). Also, we'll only try it out with Android, but it's pretty much the same with iOS. After the installation, we can now pair our device with Visual Studio 2017.

<img src="{{site.baseurl}}/XLP-8.jpg"/>

# Create/Open a Xamarin Project

Apparently, you can't pair your device with Visual Studio unless you have a Xamarin Project opened. So, let's open any or create a Xamarin Project. In my case, I've already created my own.

# Pair Device to Visual Studio
Once you have a Xamarin project opened in your Visual Studio, we can now pair our device with Visual Studio. To do this, select Tools > Xamarin Live Player > Manage Devices. This will open this popup:

<img src="{{site.baseurl}}/XLP-9.png"/>

There are two ways to pair, first is to type the code from your Xamarin Live Player app on your device or just scan the QR code being shown in the popup. This is like a handshake. Make sure you're on the same wifi network, too. This will add your device to the list of paired device. FYI I'm using [Vysor](https://www.vysor.io/) for the device mirroring.

<img src="https://media.giphy.com/media/9sMZsuUFlg90I/giphy.gif" Width="700px"/>

Now, it's all finally set up. We can now debug our application using Xamarin Live Player!

# Debug using Xamarin Live Player 

To do traditional development cycle debugging, we can select our paired device on the device list. To select the paired device, look for your device name and it has a concatenated "Player" text at the end. That means it's the live player then hit F5 to debug.

<img src="{{site.baseurl}}/XLP-10.png"/>

<img src="https://media.giphy.com/media/l0Iy3PnprUKYbCb1m/giphy.gif" Width="700px"/>

It will compile and will take seconds to deploy it to your device. I was actually amazed how smooth and fast it is! Now, you can debug without even waiting for the long compilation, builds, etc. which sometimes takes minutes. But wait, there's more!

# Live Run Feature

Now if you don't want to debug your application and just see the live preview on your device, you can use this Live Run feature. This allows you to write not only your UI, but also the business logic of your application. Again, this is really smooth and you can easily check your changes without running your application.

<img src="https://media.giphy.com/media/l0IyiH4cWGctrIv7y/giphy.gif" Width="700px"/>

# Settings and Logs

Inside your Xamarin Live Player Application on your device, you can actually set some settings like for example, changing the theme, allowing to show compile and runtime errors, etc. As for the logs, this is where you can see the compilation and runtime errors that you configure on your settings, but you can only see high-level logs.

<img src="{{site.baseurl}}/XLP-11.png" Width="400px"/>

# Limitations

There are still some stuff that are not supported for iOS and Android. Again, this is still on preview, but expect to have a lot of updates. Here's the list of the [limitations for both Android and iOS](https://developer.xamarin.com/guides/cross-platform/live/limitations/).

I'm really amazed with this one, though I didn't expect it. I just thought that XAML Previewer was enough. But, when I tried this out, I'm convinced that I'll be using this from now on. This is just one of the things from this year's Build Conference that made my jaw drop. I will be talking about other Xamarin-related stuff on my next article.

Reference/s:
-[Xamarin Live Player](https://developer.xamarin.com/guides/cross-platform/live/)
-[Visual Studio 2017 Preview 15.3](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-preview-relnotes)
-[Previewing the Xamarin Live Players for Visual Studio](https://blog.xamarin.com/live-player/)
