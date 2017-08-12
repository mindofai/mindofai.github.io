---
published: false
layout: post
title: Implementing Localization with Xamarin.Forms using Resx files
author: mindofai
date: 2017-08-12 12:00
tags: [Localization, Internationalization, i18n, l10n, Globalization, Languages XAML, Mobile App, UWP, iOS, Android, Xamarin, Xamarin. Forms]
---

<img src="{{site.baseurl}}/BP-1.png"/>


Last, Mobile .NET Developers - Philippines in partnership with DevCon PH and Seer Technologies had a whole day hands-on training session called Xamarin Code Camp for Professionals. In the first half of the event, the crew and I talked about Visual Studio 2017, fundamentals of Xamarin, Microsoft Cognitive Services, MVVM, Localization and Accessibility. Then, right after lunch, we had live coding and mini hackaton about the things we discussed in the in the first half. All in all, it was a great event, everyone looked happy and I really think they learned a lot of things about Xamarin. 

I was supposed to talk only about Localization, but we needed to atleast give them knowledge about MVVM, because they’ll be using the design pattern in the live coding. So, yeah, we didn’t have a choice so I gave a brief introduction to MVVM and I just followed the given slides lol. Anyway, I really want to talk about Localization, because I feel like it’s really important to implement it to all applications in the App Store or Play Store, since it’s going to be available globally. Only a few application have been internationalized, but I’m pretty sure that these apps are much easier to use for a lot of people globally and ofcourse, they cater a bigger market.

## Internationalization

So, let’s talk about Internationalization. Basically, it is when your app supports more than one language. Just like Pitbull, your app becomes mr. worldwide.

Enough with the jokes. In all seriousness, Internationalization is the process of making your code capable of displaying different languages and adapting its display for different locales. This is also called globalization. So, some of you might be wondering what is i18n? If you look at it, between the i and n, there are 18 letters. These are called numeronyms. That’s pretty much it.

## B-b-but, why???

You might ask, why is this important? This is the list of the top countries who download apps on Playstore. The first country on the list is India, US is close second and Brazil is third. Then fourth and fifth are South Korea and Japan. 4 of the top countries don’t have english as their main language so it’s really a great idea to support their very own. So, in order for your app to cater these top countries, support these countries’ languages.

## How exactly are you gonna support these languages? 

How are you gonna implement this on your app? That’s what localization is. You can implement it by creating resources (such as strings and images) for each language and bundling them with the internationalize app. All you have to do is to create a resource file for each languages. These resources have a list of key value pair of words, phrases, or sentences. For example, you have a resource file for english, and you have key of ThankYouText with a value of “Thank You”. And you also have a resource file for Filipino which also has a ThankYouText key but with a value of “Salamat”. After creating these resources, you can now use it on your app. The app will select its corresponding resource depending on the phones language. If there is no corresponding resource, it will use the default, which is english.

## It's not only about the language

Localization doesn’t only apply with text or labels. It can also be applied with images. As you can see right here, these are the stop signs around the globe. Most of them look alike, just the same label. But as you can see japan ruined everything. Not really, but still, it has a different shape. Another thing the problem with colors In western cultures, red means danger or error. While, in China, it means good news. So, there are alot of things to consider, so let's start because I don’t even wanna get started with gender.

## Creating Resx files

In order for us to create a language resource for each language that we want to support, we'll have to create a **Resources** folder first (just to organize our resx files) inside the **Portable** project. Next is to actually create the resource file. You can do this by right-clicking the Resource folder, **Add > New File > Misc.** and select Resource file. Name the resource file **AppResource.resx** and this will be our default language resource which is english. Once created, you can now add a Name or the key for this translatable string(It must be a valid C# property name - so no spaces or special characters are allowed) and of course the value which is the string that we want to display in our application. It should look like this:


Once done with our default resource file, we can now create resource files for other languages that we want to support. For each language you're going to support, you will need to add an aditional resource file with the name: *"Resource.{culture name}.resx"*. You can find a list of culture names [here](https://msdn.microsoft.com/en-us/library/cc233982.aspx). In my case, I'll support the Spanish language, so I'll name it **Resource.es.resx**. We'll need to add the same keys that we added in our default resource to make sure our app will have translations for each text. This is how mine looks like:

You can create more if you want, but I'll only add Spanish.

## Using Resx files through C#

We can now use our resource files by just calling the AppResource class. As an example, I created a **Label** control with the text of **AppResource.WelcomeText**.


Now, when I run the app, this is how it looks like when my phone's language settings is English.

But, when I use Spanish as my phone language, this is how it looks like:

Using resource files through C# isn't as hard as you think it is. We can also use XAML for this, but we'll have to add a glue in order for our app to inject our values into our controls. We'll have to use the **IMarkupExtension** interface. We'll do it by creating a C# class named **TranslateExtension.cs** and we'll implement it by adding this:

```csharp
using System;
using System.Globalization;
using Xamarin.Forms;
using Xamarin.Forms.Xaml;

namespace Glider_Log.Resources
{
    [ContentProperty("Text")]
    public class TranslateExtension : IMarkupExtension
    {
        public string Text { get; set; }

        public object ProvideValue(IServiceProvider serviceProvider)
        {
            if (Text == null)
                return null;

            return Resource.ResourceManager.GetString(Text, CultureInfo.CurrentCulture);
        }
    }
}
```

If you want to try this out, I uploaded [this project to github](https://github.com/mindofai/BindablePropertyDemo). Hopefully, this can get you started with creating bindable properties. Happy coding!

Reference:
- [https://developer.xamarin.com/guides/xamarin-forms/xaml/bindable-properties/](https://developer.xamarin.com/guides/xamarin-forms/xaml/bindable-properties/)
