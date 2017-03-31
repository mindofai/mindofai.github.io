---
published: true
layout: post
title: Bot Framework and Xamarin.Forms Application Integration using DirectLineClientAPI
author: mindofai
date: 2017-03-31 12:00
tags: [Bot, BotFramework, .NET, REST, API, DirectLine, DirectLineClient, UWP, Xamarin, Xamarin. Forms]
---

Last month, I talked about how to integrate your chat bot, particularly your Microsoft bot framework, into your Xamarin.Forms application alongside with Philip Domingo, my friend and my colleague from Avanade. He created a simple chat bot with Azure Bot Service which is pretty cool and very easy. You can even make a bot without typing any code. How awesome is that?

<br>

After Philip's part, I created a Xamarin.Forms application with Prism MVVM Framework using [Prism's template pack](https://marketplace.visualstudio.com/items?itemName=BrianLagunas.PrismTemplatePack) made by Brian Lagunas which is really great btw. You can download the .vsix file and install it or you can just install it through Visual Studio's Extensions. Anyway, I first created the UI for the chatbox-like view using XAML:

<br>

 <img src="{{site.baseurl}}/Chatview.jpeg" style="width: 350px;"/>

<br>

The most important thing here is the service that calls the DirectLineClient API (specifically v1.1). But, first, what is this DirectLineClient API thingy? It's a REST API for sending and receiving message from a bot framework.

> The Direct Line API is a simple REST API for connecting directly to a single bot. This API is intended for developers writing their own client applications, web chat controls, mobile apps, or service-to-service applications that will talk to their bot.

<br>

First thing is you need to create a method for setup that you're gonna call every time your application starts. I used `System.Net.Http.HttpClient` for REST API calls.

<br> 
## Setup()

```csharp

   private string conversationId;
   private string token;
   private HttpClient _httpClient;

   public async Task<bool> Setup()
        {
            _httpClient = new HttpClient();
            _httpClient.BaseAddress = new Uri("https://directline.botframework.com/");
            _httpClient.DefaultRequestHeaders.Accept.Clear();
            _httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
            _httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", "<bot secret key>");
            var response = await _httpClient.PostAsync("/api/tokens/conversation", null);

            if (response.IsSuccessStatusCode)
            {
                var result = response.Content.ReadAsStringAsync();
                token = JsonConvert.DeserializeObject<string>(result.Result);
                return true;
            }
            return false;
        }
 ```

<br>

The `https://directline.botframework.com/` is not the URL of your bot's web application. This is a general URL, so you shouldn't change this. You can get your `bot secret key` by following [these steps](https://docs.botframework.com/en-us/support/embed-chat-control2/). All we're getting here is a token, but what we need is to create a conversation. That's the next thing we'll do.


# Creating a Conversation with Bot

Now that we're getting the token, you need to create a conversation with the bot and get the `ConversationID`. This conversation will contain all your messages to the bot and bot's replies. After getting the value of the token, add this block of code:

```csharp
_httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
                response = await _httpClient.PostAsync("/api/conversations", null);
                if (response.IsSuccessStatusCode)
                {
                    var conversationInfo = await response.Content.ReadAsStringAsync();
                    conversationId = JsonConvert.DeserializeObject<Conversation>(conversationInfo).ConversationId;
                    return true;
                }
```       
Once you run the application, you can now get the `ConversationID`, we can now communicate to our bot.

# Sending Messages to the Bot

In order for us to send a message, we first need to create another method.

## SendMessage()

```csharp
public async Task<BotMessage> SendMessage(string name, string message)
        {
            var messageToSend = new BotMessage() { From = name, Text = message };
            var contentPost = new StringContent(JsonConvert.SerializeObject(messageToSend), Encoding.UTF8, "application/json");
            var conversationUrl = "https://directline.botframework.com/api/conversations/" + conversationId + "/messages/";

            var response = await _httpClient.PostAsync(conversationUrl, contentPost);
        }
 ```
 
 As you can see right here, I'm serializing the BotMessage to JSON. The BotMessage has the name of who is it from (From) and the message (Text) The BotMessage also contains the `Id`, `Created` date, `ConversationID`, etc. I added the model below. Then, I posted the serialized BotMessage to `conversationURL` using `HttpClient.PostAsync()`. We've added the `ConversationId` to the link, meaning we're sending the message to the conversation. Alright, we can now send a message!
 
## BotMessage model
 
 ```csharp
public class BotMessage
    {
        public string Id { get; set; }
        public string ConversationId { get; set; }
        public DateTime Created { get; set; }
        public string From { get; set; }
        public string Text { get; set; }
        public string ChannelData { get; set; }
        public string[] Images { get; set; }
        public Attachment[] Attachments { get; set; }
        public string ETag { get; set; }
    }

    public class Attachment
    {
        public string Url { get; set; }
        public string ContentType { get; set; }
    }
```

# Receiving Messages from the Bot
 
 After sending our message, the Bot will immediately reply. Getting the reply is quite easy! The request URI is identical with the sending of messages, but instead of `POST`, you need to use `GET`. After sending message, add this code block.
 
 ```csharp
var messagesReceived = await _httpClient.GetAsync(conversationUrl);
var messagesReceivedData = await messagesReceived.Content.ReadAsStringAsync();
var messagesRoot = JsonConvert.DeserializeObject<BotMessageRoot>(messagesReceivedData);
var messages = messagesRoot.Messages;
return messages.Last();
 ```
The data doesn't only have the bot's reply to your message, but it has all the messages inside the conversation. So, I have to create a model which has a list of BotMessage called BotMessageRoot (added the model below). To get your bot's reply, you need to get the latest message, which is the last one.

```csharp
  public class BotMessageRoot
    {
        public List<BotMessage> Messages { get; set; }
    }
``` 

The last one that I want to share is that tokens do expire every 30 minutes, so you can only have a whole conversation with a bot for 30 minutes. What I suggest is you renew your token every time the user sends a message. You can renew it using these two lines. Add this right before the return keyword:

## Renew

```csharp
var renewUrl = "https://directline.botframework.com/api/tokens/" + conversationId + "/renew/";
 response = await _httpClient.GetAsync(renewUrl);
 ```

Now, you should have both Setup() and SendMessage() methods:

## Setup()

```csharp
 public async Task<bool> Setup()
        {
            _httpClient = new HttpClient();
            _httpClient.BaseAddress = new Uri("https://directline.botframework.com/");
            _httpClient.DefaultRequestHeaders.Accept.Clear();
            _httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
            _httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", "<bot secret key>");
            var response = await _httpClient.PostAsync("/api/tokens/conversation", null);

            if (response.IsSuccessStatusCode)
            {
                var result = response.Content.ReadAsStringAsync();

                token = JsonConvert.DeserializeObject<string>(result.Result);
                _httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
                response = await _httpClient.PostAsync("/api/conversations", null);
                if (response.IsSuccessStatusCode)
                {
                    var conversationInfo = await response.Content.ReadAsStringAsync();
                    conversationId = JsonConvert.DeserializeObject<Conversation>(conversationInfo).ConversationId;
                    return true;
                }
                return true;

            }
            return false;
        }
```

## SendMessage()
```csharp
 public async Task<BotMessage> SendMessage(string name, string message)
        {
            var messageToSend = new BotMessage() { From = name, Text = message };
            var contentPost = new StringContent(JsonConvert.SerializeObject(messageToSend), Encoding.UTF8, "application/json");
            var conversationUrl = "https://directline.botframework.com/api/conversations/" + conversationId + "/messages/";

            var response = await _httpClient.PostAsync(conversationUrl, contentPost);

            var messagesReceived = await _httpClient.GetAsync(conversationUrl);
            var messagesReceivedData = await messagesReceived.Content.ReadAsStringAsync();
            var messagesRoot = JsonConvert.DeserializeObject<BotMessageRoot>(messagesReceivedData);
            var messages = messagesRoot.Messages;

            var renewUrl = "https://directline.botframework.com/api/tokens/" + conversationId + "/renew/";
            response = await _httpClient.GetAsync(renewUrl);

            return messages.Last();
        }
```

Now, if you use this service, you can now communicate with the bot through Xamarin, UWP, Console apps, etc.! 

# Output

 <img src="{{site.baseurl}}/ChatbotXamarin.jpeg" style="width: 350px;"/>

Pretty cool, right? I also have this slide that I used with my talk last month where I discussed the DirectLineClient REST API:

# Slide
<iframe src="//www.slideshare.net/slideshow/embed_code/key/J9QITUWiwiQt3s" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/BryanAnthonyGarcia/directlineapi-xamarinforms-app-and-bot-framework-integration" title="DirectLineAPI - Xamarin.Forms App and Bot Framework Integration" target="_blank">


Hope this helps you develop your Xamarin Application integrated with Bot Framework! Good luck!

Resource:
- [https://docs.botframework.com/en-us/restapi/directline/](https://docs.botframework.com/en-us/restapi/directline/)
- [https://github.com/PrismLibrary/Prism](https://github.com/PrismLibrary/Prism)
