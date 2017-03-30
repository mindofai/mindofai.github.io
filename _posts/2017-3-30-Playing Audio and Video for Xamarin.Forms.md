---
published: true
layout: post
title: Playing Audio and Video for Xamarin.Forms
author: mindofai
date: 2017-03-30 12:00
tags: [UWP, Android, iOS, Media, Video, Audio MediaElement, Xamarin. Forms, InTheHand.Forms]
---

My experience working with video and audio streaming in Xamarin.Forms. We had this project where we used Xamarin.Forms for developing a cross-platform chatbot (Bot Framework + LUIS.ai) application (btw, this was my first Xamarin.Forms project). We needed to play a video and I thought it will be really easy, because in UWP development, you can just use MediaElement. I'VE NEVER BEEN SO WRONG IN MY LIFE. It's so painful, especially with UWP. 
<br>
<br>

We searched for other workarounds and stuff that we can use for playing videos, but we couldn't find anything. Yeah, I know only a few uses UWP apps, but still, Xamarin.Forms should've atleast created a control for it.

<br>
<br>

I've had that problem months ago, but it looks like I'm going to encounter it again. So, I searched for workarounds, thinking that there might be a NuGet package out there that I can use. Luckily, I found one! We can now play videos/audios with Xamarin.Forms using [**InTheHand.Forms**](https://github.com/inthehand/InTheHand.Forms) which can be used for Android, iOs, and ofcourse UWP. If you have used the UWP's MediaElement , this will be easy for you. Follow these steps:

<br>
<br>

1. To use this, first, you need to install [***this NuGet package***](https://www.nuget.org/packages/inthehand.forms) to the PCL and to all three platform-specific projects (Android, iOS, and UWP) or whichever you have. It will not show any error if you only added the package in PCL and run it, so it'll hard for you to debug this if you forgot to install it to your platform-specific projects.


<br>
<br>
2. After the installation of package, the next thing you'll do is to open the XAML page where you want to play a video and add this namespace to your XAML:


```
xmlns:inthehand="clr-namespace:InTheHand.Forms;assembly=InTheHand.Forms"
```

<br>
<br>

3. Now, you can use the InTheHand.Forms' MediaElement:

```
 <inthehand:MediaElement HorizontalOptions="Fill" VerticalOptions="Fill" AreTransportControlsEnabled="true" AutoPlay="True" 
                           Source="https://sec.ch9.ms/ch9/b4ca/4e3d3cb1-4345-467b-9dc7-9fdcc9f6b4ca/VS2017_high.mp4"/>
  ```

<br>
<br>

As you can see, it's almost the same as how the UWP's MediaElement looks like. You just need to set the source and you're done. I've added a link for the source which is about [Intro to Xamarin and VS2017](https://channel9.msdn.com/events/Xamarin/Recent-Webinars/Introduction-to-Xamarin-for-Visual-Studio-2017). There are other controls that you might want to set such as `AreTransportControlsEnabled` to show/hide the controls and `AutoPlay` to auto play the video/audio.

<br>
<br>

4. Once done, you can now run your application to iOS, Android, and Windows.

 <img src="{{site.baseurl}}/MediaElementUWP.png" style="width: 500px;"/>


<br>
<br>
This is so useful for me since I was really frustrated with my previous project which needed to play videos/audios. Now, you can just install this package, add the namespace, place the MediaElement control, and done! Pretty cool, right? Hopefully, this can also help you with your current or future projects.


<br>
<br>

Resources:

- [https://inthehand.github.io/html/T_InTheHand_Forms_CheckSwitch.htm#](https://inthehand.github.io/html/T_InTheHand_Forms_CheckSwitch.htm#)
- [https://github.com/inthehand/InTheHand.Forms](https://github.com/inthehand/InTheHand.Forms)
- [https://www.nuget.org/packages/inthehand.forms](https://github.com/inthehand/InTheHand.Forms)

