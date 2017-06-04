---
published: false
layout: post
title: Creating a Custom Control with Bindable Properties
author: mindofai
date: 2017-06-04 12:00
tags: [Custom, Custom Control, BindableProperty, Bindable, XAML, Mobile App, UWP, iOS, Android, Xamarin, Xamarin. Forms]
---

Last week, I gave a talk for last month's MSDN Session wherein I talked about Xamarin Live Player. A lot of developers were amazed, especially those who are in need of iOS debugging. Atleast, they can now check their application out in an iOS device without a Mac. Right after my talk and all the questions about Xamarin Live Player, someone came up to me and asked me about how can they create a property for their custom control, because currently, they're struggling with how to do it. I really found it interesting and told them that I'll just create an article about it. So, yeah, that's the reason why this article exists now lol.

<img src="{{site.baseurl}}/MAS-14.png"/>

# My Custom Control

I already created a custom control called **MyCustomControl** that has a label and an image. I want to use this as a layout for each sport categories that will be shown on my home page. I'll admit, this isn't the best example to use for demoing BindableProperty, but this works :P 

## MyCustomControl.xaml

``` xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentView xmlns="http://xamarin.com/schemas/2014/forms" 
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="BindablePropertyDemo.Custom.MyCustomControl">
    <Grid x:Name="grid" 
          Padding="10,40,10,10"
          HeightRequest="160"
          VerticalOptions="Start">
        <Grid.RowDefinitions>
            <RowDefinition Height="100"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>
        <Image x:Name="image"
               Source="basketball.png"
               HeightRequest="100"/>
        
        <Label x:Name="title"
               Text="BASKETBALL"
               Grid.Row="1" 
               FontSize="20"
               VerticalOptions="Center"
               TextColor="White"
               HorizontalOptions="Center" 
               FontAttributes="Bold"/>
    </Grid>
</ContentView>
```

Anyway, that is what I currently have. I can only set the actual image's source and label's text. What I want to do is to create a property that will be exposed by the control. I wonder what do we need to use to do this??? Well, you guessed it, it's called **BindableProperty**.

# What is a Bindable Property?

Basicall, a bindable property is a special type of property, where the property's value is tracked by the Xamarin.Forms property system. You can read more about Bindable Property in [this article](https://developer.xamarin.com/guides/xamarin-forms/xaml/bindable-properties/).

# Adding Bindable Properties

There are several things that we need to set up and we'll be adding these for each setting this up for each properties that we want to add.

## Adding the exposed property

First, you need to create a regular property for your bindable property. We're gonna start with the label and we'll name it *TitleText*. This is the property that will be exposed by the control.

       ``` csharp
       public string TitleText { get; set; }
       ```
       
## Adding the BindableProperty field

The next step is to create the **BindableProperty**. What you need to do is to create a read-only **BindableProperty** field. Ideally, the name of this field is the same as the regular property that we created, we'll just add *Property* at the end of it.

       ``` csharp
       public static readonly BindableProperty TitleTextProperty;
       ```
       
But, ofcourse, we're not done with it. The next part is to set the the field with *BindableProperty.Create()* method. This *Create()* method takes numerous parameters wherein some of them can be *null*:

       ``` csharp
       public static readonly BindableProperty TitleTextProperty = BindableProperty.Create(
                                                         propertyName: "TitleText",
                                                         returnType: typeof(string),
                                                         declaringType: typeof(MyCustomControl),
                                                         defaultValue: "",
                                                         defaultBindingMode: BindingMode.TwoWay,
                                                         propertyChanged: TitleTextPropertyChanged);

       ```
 
 As you can see,there are several parameters being set. I'm going to break down each of the parameters that I've set:
 
**propertyName** - the name of our exposed property as a string.

**returnType** - the return type of our property.

**declaringType** - the type declaring this BindableProperty.

**defaultBindingMode** - the binding mode our property should have.

**propertyChanged** - the specified callback method to be fired after the property has changed. This will receive 3 parameters: *bindable* (the current control class), *oldValue* (the old value of the property), and *newValue* (the newest value of the property)

## Adding the callback method

   private static void TitleTextPropertyChanged(BindableObject bindable, object oldValue, object newValue)
        {
            var control = (MyCustomControl)bindable;
            control.title.Text = newValue.ToString();
        }

 
  <img src="{{site.baseurl}}/MAS-1.png"/>
 
Now, we can create our Azure Mobile App. To create a Mobile App, click New, then you can either search for ‘Mobile App’ or click Web + Mobile, then select Mobile App.

  <img src="{{site.baseurl}}/MAS-2.png"/>
  
Once Mobile App is selected, you can now fill out the required details. You will have to give a name, the subscription, the resource group, and an App Service plan (Standard would suffice). You can also enable the Application Insights to track things about your services such as diagnosis of issues and your users’ interaction with it. 
 

  <img src="{{site.baseurl}}/MAS-3.png"/>
  
After filling this out, you can now click Create. This will take a while to create, but after a period of time, you should see this.


  <img src="{{site.baseurl}}/MAS-4.png"/>

This means we’ve already created our Mobile App. Now, we can set up our Easy Tables!

# Initializing Easy Tables
Initializing the Easy Tables is, ofcourse, really easy and also fast. To do this step, go to the Mobile Section of our Mobile App and select Easy Tables. 
 
 
  <img src="{{site.baseurl}}/MAS-5.png"/>
 
Once Easy Tables is clicked, this blade will appear. Click the ‘Need to configure Easy Tables…’ notification which is being shown at the top. It will navigate you to another blade wherein you set your Easy Tables’ data connection and initialize the Mobile App’s Easy Tables.
 
  <img src="{{site.baseurl}}/MAS-6.png"/>
 
## Adding Data Connection for your Easy Tables
The first step in initializing your Easy Tables is to add a data connection. As of now, you can only add Azure SQL Databases. Click the button below the ‘Connect a Database’ and you can now create a connection to an existing database or you can create one. We’ll just create an empty Azure Database.

  <img src="{{site.baseurl}}/MAS-7.png"/>
  
After clicking the button, you can just click Add, select SQL Database, and create a new one.
   
  <img src="{{site.baseurl}}/MAS-8.png"/>
  
 
You will have to configure the details for the Database name and the server it’s going to be in. After that, click Select. 
This will also automatically create a connection string for you. Ideally, you will have to type in your server’s username and password, but with Easy Tables, it will be already set up for you. You can now just click OK to finish things up.

  <img src="{{site.baseurl}}/MAS-9.png"/>
  
It will just take a while, because this will create not only the database (and even the server if you created a new one), but also the data connection for your Easy Tables. 

Finally, you will be navigated back to the Initialization of Easy Tables. The next step is just the acknowledgement of the creation of Easy Tables. All you have to do is to click the checkbox, then click `Initialize App` and you’re all done.


  <img src="{{site.baseurl}}/MAS-10.png"/>

We can now add tables for our Easy Tables.

# Adding Tables
After a few moments, we’re now ready to create our first table for our Database. You can call it anything you want, but I already have an existing DataModel named Debt. The beauty of Easy Tables is that it automatically updates your columns in the tables dynamically based on the data we pass in. You can also set the permission for each method. You can select from three access permissions: Anonymous, Authenticated users (wherein only authenticated users can access your tables), or even disable any access. We’ll select anonymous for now then click OK.
 
  <img src="{{site.baseurl}}/MAS-11.png"/>
 
Now, our backend is fully set up. You can actually try to retrieve the table data like a REST API with the endpoint `http://<urlofazureapp>/api/tables/<nameoftable>?ZUMO-API-VERSION=2.0.0`.

# Trying out your backend
To integrate our mobile app into our Xamarin application, we need to firstly add the Azure Mobile App SDK Nuget Packages. The Microsoft.Azure.Mobile.Client lets you connect to your Azure Mobile backend and the SQLiteStore enables you to add full online/offline synchronization. Both of this should be added in all projects (PCL/Shared and all platforms):
 
 
  <img src="{{site.baseurl}}/MAS-12.png"/>
 
Next step is to add this line of code on your platform projects. For iOS, add this to the FinishedLaunching method of AppDelegate class. For Android, add this to the OnCreated method of MainActivity class:

```csharp
Microsoft.WindowsAzure.MobileServices.CurrentPlatform.Init();
SQLitePCL.CurrentPlatform.Init();
```

This is to initialize the Azure Mobile Client SDK on your platform projects.
Now, we can finally create a Data Model that we’ll use locally to map the data from our backend. First, it should have the same name as the created table and a string of Id property should be added. This ensures the Mobile App SDK to identify that the data model can be mapped from the backend. This is how my Debt class looks like:

```csharp
  public class Debt
    {
        [Newtonsoft.Json.JsonProperty("Id")]
        public string Id { get; set; }
        
        public string Name { get; set; }

        public double Amount { get; set; }

        public bool IsPaid { get; set; }
    }
```

## Creating the Service 
Finally, we can now create our service that will use the Mobile App SDK to integrate with our Mobile App backend. This will enable our app to read, insert, delete, and modify data locally and synchronize it to our backend. We will put all of this in a single class.

## AzureMobileService class
First, create a class named AzureMobileService. Then, create a method named `Initialize()` and two properties: `MobileServiceClient` and `IMobileServiceSyncTable`. 

```csharp
public class AzureMobileService
    {
        public MobileServiceClient Client { get; private set; }
        private IMobileServiceSyncTable<Debt> debtTable;

        private async Task Initialize()
        {
        }
    }
```
    
## Initialize()
In our `Initialize()` method, we will initialize our `MobileServiceClient` and `SyncTable`. This needs to be called only once. We need to pass in the base url of our Mobile App and specify the path of our local database:

```csharp
private async Task Initialize()
        {
            Client = new MobileServiceClient("https://<mobileappname>.azurewebsites.net");

            var path = Path.Combine(MobileServiceClient.DefaultDatabasePath, "debtsync.db");

            var store = new MobileServiceSQLiteStore(path);

            store.DefineTable<Debt>();

            await Client.SyncContext.InitializeAsync(store);

            debtTable = Client.GetSyncTable<Debt>();
        }
```


