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

First, you should create an interface for the OpenAppService, then create a `Launch()` method that we'll call later:

## IOpenAppService Interface

```csharp
public interface IOpenAppService
{
    Task<bool> Launch(string stringUri);
}
```

The next step is to create platform-specific implementations for UWP, Android, and iOS. It will be a little bit tricky with iOS and I'll explain it later.

Let's work with UWP first:

## OpenAppService (UWP)

```csharp
[assembly: Xamarin.Forms.Dependency (typeof (OpenAppService))]
namespace OpenAppLaunch.UWP {

 public class OpenAppService : IOpenAppService
 {
    public async bool  Launch(string stringUri)
    {
        Uri uri = new Uri(stringUri);
        return await Windows.System.Launcher.LaunchUriAsync(uri);
    }
 }
}
```

Then for Android: 

## OpenAppService (Droid)

```csharp
[assembly: Xamarin.Forms.Dependency(typeof(OpenAppService))]
namespace OpenAppLaunch.Droid
{
    public class OpenAppService : Activity, IOpenAppService
    {
        public Task<bool> Launch(string stringUri)
        {
        try{
            Intent intent = Android.App.Application.Context.PackageManager.GetLaunchIntentForPackage(stringUri);

            
            if (intent != null)
            {
                intent.AddFlags(ActivityFlags.NewTask);
                Forms.Context.StartActivity(intent); 
            }
            else
            {
                intent = new Intent(Intent.ActionView);
                intent.AddFlags(ActivityFlags.NewTask);
                intent.SetData(Android.Net.Uri.Parse("market://details?id=" + stringUri)); // This launches the PlayStore and search for the app if it's not installed on your device
                Forms.Context.StartActivity(intent);
            }
                return Task.FromResult(true);
          }
            return Task.FromResult(false);
        }

```

As for iOS, this is where it gets tricky. Due to iOS 9's security, we will need to add the name of the app into the `info.plist`. This security requirement was added because some apps were using this functionality to determine what other apps you had installed except pre-installed apps.

## info.plist

```xml
<key>LSApplicationQueriesSchemes</key>
<array>
    <string>google</string>
    <string>facebook</string>
</array>
```

If the application name is not added to the `info.plist`, when you try to launch the application using `OpenAppService.Launch()`, it will still launch the application, but it will return `false`. For the iOS' OpenAppService:

## OpenAppService (iOS)

``` csharp
[assembly: Xamarin.Forms.Dependency(typeof(OpenAppService))]
namespace OpenAppLaunch.iOS
{
    public class OpenAppService : IOpenAppService
    {
      
        public Task<bool> Launch(string stringUri)
        {
            try
            {
                NSUrl request = new NSUrl(stringUrl);
                bool isOpened = UIApplication.SharedApplication.OpenUrl(stringUrl);

                if (isOpened == false)
                    UIApplication.SharedApplication.OpenUrl(new NSUrl(stringUrl));
                    
                return Task.FromResult(true);
            }
            catch (Exception ex)
            {
                Debug.WriteLine("Cannot open url: {0}, Error: {1}", request.AbsoluteString, ex.Message);
                var alertView = new UIAlertView("Error", ex.Message, null, "OK", null);

                alertView.Show();
                
                return Task.FromResult(false);
            }
        }
    }
```

You can use the `OpenAppService` service and call the `Launch(string stringUri)` method and pass the URI. How does that URI look like? The URI should be like this: 

``` csharp
"appname://dataYouWantToPass"
```

Now, pass it as a parameter using the `OpenAppService.Launch()`:

``` csharp
OpenAppService.Launch("skype://2812574");
```

Now, you can open external apps through URI with Xamarin.Forms with these platform-specific implementations and with the help of DependencyService! I hope this will help you with your development for the future!

Resources:
- [https://forums.xamarin.com/discussion/48089/how-to-open-other-apps-from-xamarin-forms](https://forums.xamarin.com/discussion/48089/how-to-open-other-apps-from-xamarin-forms)
