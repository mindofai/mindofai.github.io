---
publish: true
layout: post
title: Debugging .NET Native in Visual Studio
author: tom
tags: [UWP, Surface, Debugging, Xamarin, Xamarin.Forms]
---

As I've mentioned before, for your Xamarin.Forms app on UWP, a lot happens when you flip the switch from Debug build to Release build.  The Xamarin forums and StackOverflow have lots of questions related to issues stemming from this.  The big difference is that in Release mode, Visual Studio compiles your app using the .NET Native tool chain.  This can sometimes cause late-in-the-dev-cycle runtime issues that pop up when a release build is performed.  As most know, the further along a bug gets in the development cycle, the more expensive it is [CITIATION NEEDED], so I'd encourage you to regularly test a Release build on UWP, or better yet, have your CI Process produce a Release build for you to test before the app can be moved to Production environments. 

From MSDN:
> If you run into an issue when testing the Release configuration that you need to debug it is important to note that the Release configuration is by default fully optimized code (e.g. code inlining will be applied in many places). These optimizations will have a significant impact on the debugging experience including unpredictable stepping and breakpoint behavior (due to code inlining) and the inability to inspect most variables due to memory optimizations. This means you will want to debug a non-optimized .NET Native build. 

The easiest way to do this is to create a new build configuration with code optimization disabled, that way you can simply switch to this new configuration when you need to debug a .NET Native build.

- In the Solution Configurations dropdown, select Configuration Manager.
 - Under **Active solution configuration** dropdown, select the **<New...>** option
  - Name this new configuration "Debug .NET Native" or something like that.
   - Copy settings from Release, click OK
 - You'll now see your new configuration in the config manager screen, but before you close this, make sure to check the Build and Deploy checkboxes for the UWP head project.  They're unchecked by default (I don't understand why)

Then go to the Project Properties of your .UWP head project.  You'll need to toggle 2 boxes here:
1. Uncheck **Optimize code**
2. Check the **Compile with .NET Native tool chain**



# Resources
- [https://blogs.msdn.microsoft.com/visualstudioalm/2015/07/29/debugging-net-native-windows-universal-apps/](https://blogs.msdn.microsoft.com/visualstudioalm/2015/07/29/debugging-net-native-windows-universal-apps/)

