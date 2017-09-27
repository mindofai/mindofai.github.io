---
published: false
layout: post
title: Launching Apps thru URI with Xamarin.Forms
author: mindofai
date: 2017-09-27 12:00
tags: [iTunes, iTunes Connect, App Submission, Apple, Icon, Marketing Icon, Issue, iOS, Xamarin Studio, Xamarin. Forms]
---

We've encountered an issue with our iOS app submission and I had to work until 2 in the morning to fix it. This is something you might also encounter when you upload your build to iTunes Connect. According to new guidelines for the **XCode 9**: 


The solution is pretty quick and easy if you're using XCode (as long as you have XCode 9):

But for Xamarin Studio, this Marketing Icon isn’t available in the App Assets yet (Welp, until now! Read 'til the end). I tried looking for a solution. It took me hours looking for a helpful fix, but I couldn't find any. So, we came up with a solution. What we did is updated the *Contents.json* under the *Assets.xcassets* and we added the settings for the Marketing Icon:

    ```{
          "size" : "1024x1024",
          "idiom" : "ios-marketing",
          "filename" : "logo.png",
          "scale" : "1x"
        }
        ```
 
I’ve also added the **logo.png** image which should be **1024x1024** inside *AppIcons.xcassets*. You need to make sure that the logo.png was added inside the iOS project:

```
       <ImageAsset Include="Resources\Images.xcassets\AppIcons.appiconset\logo.png"/>
```

After doing this, the warning will be gone. You should be able to successfully submit the binary to Apple for review and you won’t receive the warning message anymore. 

The funny thing here is that Visual Studio for Mac already have an update where they added the Marketing Icon into their AppIcon assets. So, you can just update your Visual Studio for Mac to **7.1.5** and make sure you already have **XCode 9**. After updating, you can check the AppIcon assets and you'll find the Marketing Icon:


You can just set the Marketing Icon image and you're good to go. This made me slightly crazy because right after applying our fix, we saw this. But hey, this is what I expect from Microsoft! Quick fix!

So, yeah, hope this helps!

