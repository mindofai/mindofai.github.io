---
published: true
layout: post
title: Workaround for Xamarin.Forms' DisplayAlert Bug (Alert Being Shown Twice)
author: mindofai
date: 2017-04-05 12:00
tags: [Bug, DisplayAlert, Alert, Popup, Display, Twice, UWP, iOS, Android Xamarin, Xamarin. Forms]
---

While I was answering questions in StackOverflow, I encountered a [question](http://stackoverflow.com/questions/43106567/xamarin-form-display-alert-pop-up-appear-2-times/43106944#43106944) about Xamarin.Forms' DisplayALert. My first answer was so wrong and it's not solving any problem. I was trying to correct something which is already correct. I'll be honest, I haven't actually tried out his code. So, I tried the code myself. I thought it was only a bug within his app, but apparently, it's been a bug for a very long time. 

I'm taking about this code block:

```csharp
var resp = await DisplayAlert("","Are you sure want to Logout?","Yes", "No");
if (resp)
{ 
//Do something
}
```

## Bug
This results into two popups, which is obviously not expected. This is [an actual bug](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/127) and is reported to Bugzilla already back in December and I guess it's still not fixed.

## Solution

So, instead, I looked for other workarounds, because I know that I'll encounter this problem in the future, too. And also, I want to help the guy from StackOverflow. What I've found is that you need to need to invoke the Display Alert in the main UI thread using [Xamarin.Forms.Device.BeginInvokeOnMainThread](https://developer.xamarin.com/api/member/Xamarin.Forms.Device.BeginInvokeOnMainThread/p/System.Action/). We need to pass in an `Action` that will execute the `DisplayAlert` to the main UI thread:

```csharp
  Device.BeginInvokeOnMainThread(new Action(async () =>
  {
       if(await DisplayAlert("", "Are you sure want to Logout?", "Yes", "No"))
       {

       }
  }));
 ```
 
This is used in order to do something on the UI thread. So it's normally called from a background thread, in order to manipulate the UI, which can only be done on the UI thread. The body of the lambda expression is the code which you want to execute in the UI thread. This is the same with how Silverlight/WPF/WP8.1, iOS, and Android access the GUI thread:
 
## Silverlight/WPF/etc.

```csharp
Deployment.Current.Dispatcher.BeginInvoke( ()=> {
 if(await DisplayAlert("", "Are you sure want to Logout?", "Yes", "No"))
       {

       }
});
```

And for Android: `AndroidRunOnUiThread(() => delta)`

Same thing for iOS: `InvokeOnMainThread`
 
This fixes the issue, because we're now invoking it on the Main UI thread. Our DisplayAlert will now be executed once. So, yeah, for now, we can use this workaround. But, hopefully, they fix the bug, so we can just execute it without the BeginInvokeOnMainThread method. I hope this can help you with your development, especially those guys who's encountering this right now.
