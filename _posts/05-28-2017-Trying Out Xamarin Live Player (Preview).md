---
published: false
layout: post
title: Trying Out Xamarin Live Player (Visual Studio 2017 Preview)
author: mindofai
date: 2017-05-28 12:00
tags: [Debugging, Xamarin Live Player, Live Player, Preview, Visual Studio, Mobile, iOS, Android, Xamarin, Xamarin. Forms]
---

So, I'm already kinda late with this. It's been almost 3 weeks since Build 2017 happened in Seattle and I just finished watching some of the highlights on [https://channel9.msdn.com/Events/Build/2017](Channel 9), especially all the things relevant to Xamarin and Mobile .NET. I've read that Xamarin had a bunch of sessions where they announce awesome stuff and I was really interested and excited about a couple of things, namely Xamarin Live Player, Visual Studio Mobile Center, .NET Standard and Fluent Design. I will write a different article about other the other three, but we'll start talking about Xamarin Live Player.

# Xamarin Live Player

Visual Studio 2017's brand-new Xamarin Live Player for Android and iOS allows you to write, execute, and debug your Xamarin application continuously on an actual iOS or Android device straight from the IDE. It has the traditional development cycle where you write-compile-run-debug, but it's so much faster. But, what I loved about it is that it has a live previewer mode where your code is automatically compiled and deployed per-view basis continuously into your actual device. It's pretty awesome, though, this is not new to me, since Gorilla Player almost identically does the same stuff, but I prefer Xamarin Live Player since the setup is much easier.

## Getting started

So, what I want to show to you is how you can actually use Xamarin Live Player. From installation to running a blank app into your device with Xamarin Live Player's live preview mode. Since we can only try out Xamarin Live Player using Visual Studio 2017 Preview (15.3), we'll need to start from the actual installation of Visual Studio 2017 Preview, but ideally, if 15.3 becomes generally available, you can skip the installation step and just make sure that your Visual Studio 2017 is updated.

## Visual Studio 2017 Preview Installation

First, you need to install the Visual Studio 2017 Preview ((https://www.visualstudio.com/en-us/news/releasenotes/vs2017-preview-relnotes)[For Windows]/(https://developer.xamarin.com/recipes/cross-platform/ide/change_updates_channel/#xamarinstudio)[For Mac]. Make sure that the Visual Studio 2017 version you're installing is 15.3. The only workload you need to install is ofcourse Cross-Platform Development. It wiss ask you for the installation nickname, you can just name it `153Preview` or whatever you like. The installation will take a while.

## Xamarin Live Player App Installation

While you're installing 
