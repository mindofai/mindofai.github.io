---
published: false
layout: post
title: Trying Out Xamarin Live Player
author: mindofai
date: 2017-05-28 12:00
tags: [Debugging, Xamarin Live Player, Live Player, Preview, Visual Studio, Mobile, iOS, Android, Xamarin, Xamarin. Forms]
---

So, I'm already kinda late with this. It's been almost 3 weeks since Build 2017 happened in Seattle and I just finished watching some of the highlights on [Channel 9](https://channel9.msdn.com/Events/Build/2017), especially all the things relevant to Xamarin and Mobile .NET. I've read that Xamarin had a bunch of sessions where they announce awesome stuff and I was really interested and excited about a couple of things, namely Xamarin Live Player, Visual Studio Mobile Center, .NET Standard and Fluent Design. I will write a different article about other the other three, but we'll start talking about Xamarin Live Player.

# Xamarin Live Player

Visual Studio 2017's brand-new [Xamarin Live Player](https://www.xamarin.com/live?utm_medium=Blog&utm_source=Xamarin_blog_5_11_MI&utm_campaign=msbuild_2017) for Android and iOS allows you to write, execute, and debug your Xamarin application continuously on an actual iOS or Android device straight from the IDE. It has the traditional development cycle where you write-compile-run-debug, but it's so much faster. But, what I loved about it is that it has a live previewer mode where your code is automatically compiled and deployed per-view basis continuously into your actual device. It's pretty awesome, though, this is not new to me, since Gorilla Player almost identically does the same stuff, but I prefer Xamarin Live Player since the setup is much easier.

# Getting started

So, what I want to show to you is how you can actually use Xamarin Live Player. From installation to running a blank app into your device with Xamarin Live Player's live preview mode. Since we can only try out Xamarin Live Player using Visual Studio 2017 Preview (15.3), we'll need to start from the actual installation of Visual Studio 2017 Preview, but ideally, if 15.3 becomes generally available, you can skip the installation step and just make sure that your Visual Studio 2017 is updated.

# Visual Studio 2017 Preview Installation

First, you need to install the Visual Studio 2017 Preview ([For Windows](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-preview-relnotes)/[For Mac](https://developer.xamarin.com/recipes/cross-platform/ide/change_updates_channel/#xamarinstudio)). If you already have a Visual Studio 2017 installed, don't worry, this is a different one. You can actually run the currently-installed Visual Studio 2017 and this one side-by-side, meaning they're not the same application. Make sure that the Visual Studio 2017 version you're installing is 15.3. The only workload you need to install is ofcourse Cross-Platform Development. It wiss ask you for the installation nickname, you can just name it `153Preview` or whatever you like. The installation will take a while.

After the installation, this is what you will see on your Visual Studio Installer. There will be two different Visual Studio 2017 application as you can see below:

# Get Xamarin Live Player Up and Running

 we can now start setting up the Xamarin Live Player. This means that Xamarin Live Player isn't installed and ready to use right away. You will still have to do a couple of things to get it up and running.

## Install Xamarin Updater

First, we need to install Xamarin Updater which provides us out of band updates to Xamarin for Visual Studio 2017 or later. Open your Visual Studio 2017 Preview and select Tools > Extension and Updates. Select Online and search for "Xamarin Updater" and download Xamarin Updater. After downloading, you will have to close your Visual Studio to install the Xamarin Updater.

## Xamarin Preview Updates

Once installed, you can go back to Tools > Extension and Updates. Select Updates and then Xamarin Previe node. This gives you the list of stuff you can update for Xamarin. What yo need to update specifically is the Xamarin for Visual Studio. Click update and once done, you will have to close your Visual Studio again to install the updates. Then, we'll have to re-open Visual Studio again. Our Visual Studio is ready. Let's now set up our devices!

# Installing Xamarin Live Player Applicatrion

