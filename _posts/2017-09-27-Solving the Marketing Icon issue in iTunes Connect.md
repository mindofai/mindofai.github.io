---
published: false
layout: post
title: Launching Apps thru URI with Xamarin.Forms
author: mindofai
date: 2017-09-27 12:00
tags: [iTunes, iTunes Connect, App Submission, Apple, Icon, Marketing Icon, Issue, iOS, Xamarin Studio, Xamarin. Forms]
---

We've encountered an issue with our iOS app submission and I had to work until 2 in the morning to fix it. This is something you might also encounter when you upload your build to iTunes Connect. According to new guidelines for the XCode 9: 


The solution is pretty quick and easy if you're using XCode (as long as you have XCode 9):

But for Xamarin Studio, this Marketing Icon isn’t available in the App Assets yet. I tried looking for a solution. It took me hours looking for a helpful fix, but I couldn't find any. So, we came up with a solution. What we did is updated the **Contents.json** under the AppIcons.appassets and we added the settings for the Marketing Icon:
