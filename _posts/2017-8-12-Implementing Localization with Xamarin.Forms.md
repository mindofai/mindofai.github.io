---
published: false
layout: post
title: Implementing Localization with Xamarin.Forms
author: mindofai
date: 2017-06-04 12:00
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

Localization doesn’t only apply with text or labels. It can also be applied with images. As you can see right here, these are the stop signs around the globe. Most of them look alike, just the same label. But as you can see japan ruined everything. Not really, but still, it has a different shape. Another thing the problem with colors In western cultures, red means danger or error. While, in China, it means good news. So, there are alot of things to consider and I don’t wanna get started with gender!

If you want to try this out, I uploaded [this project to github](https://github.com/mindofai/BindablePropertyDemo). Hopefully, this can get you started with creating bindable properties. Happy coding!

Reference:
- [https://developer.xamarin.com/guides/xamarin-forms/xaml/bindable-properties/](https://developer.xamarin.com/guides/xamarin-forms/xaml/bindable-properties/)
