---
published: true
layout: post
title: Azure Messaging Services Quickstart - Event Grid
author: mindofai
date: 2023-09-02 12:00
tags: [Azure, Messaging, Event Grid, Topic, Integration, Events, Service Bus]
---

<img src="{{site.baseurl}}/EG.png"/>


Welcome to my blog post on Azure Messaging Services! In these articles, I'll delve into the intricacies of various messaging solutions offered by Azure, exploring why and when you should use them, and how to make the most out of each service.

Today, we'll specifically talk about **Azure Event Grid**.

## Why Messaging?

Firstly, it's essential to address why we need these messaging services. At a basic level, you might not actually need them. If you're building a small application with a single client, API, and database, messaging might not be necessary. However, messaging becomes invaluable when you have distributed applications, such as microservices or serverless applications, that need to communicate seamlessly. While REST APIs are excellent for retrieving data and sending requests, messaging is the solution for non-blocking, loosely-coupled communication between applications or services.

## Understanding Messaging Terminology

Before we delve into specific services, let's familiarize ourselves with some key messaging terms:

- **Message**: Essentially an instruction or command sent from one system to another.
- **Event**: Similar to a message but more about broadcasting that something happened, rather than expecting an action.
- **Producer**: The sender of messages or events.
- **Consumer**: The receiver of messages or events.
- **Broker**: The intermediary service responsible for handling and routing messages or events.
- **Event-driven Architecture**: A design approach focused on building distributed applications that communicate via events or messages.

## Azure Event Grid

<img src="{{site.baseurl}}/MS-5.png"/>

### Why Use It?

- Seamless integration with Azure services.
- Fully managed, serverless infrastructure.
- Highly scalable event broker supporting multiple sources and subscriptions.

### When Not to Use It?

- Unsuitable for stream/batch processing (use Event Hub instead).
- Challenges in hybrid or multi-cloud environments.
- Testing and debugging can be tricky.

### How to Use It?

- Utilize SDKs such as .NET, Java, Python, etc.
- Leverage Azure Functions Trigger for event-driven scenarios.

## Creating an Event Grid & Event Grid Topic in Azure

Azure Event Grid is a fully-managed event routing service that allows you to react to events from various sources. Follow these steps to create an Event Grid topic and obtain the endpoint and key:

**Step 1: Sign in to the Azure Portal**
Navigate to the [Azure Portal](https://portal.azure.com/) and sign in with your Azure account credentials.

**Step 2: Create an Event Grid Topic**
- Click on the "Create a resource" button (+) in the Azure portal.
- Search for "Event Grid Topic" and select it from the results.
- Click on the "Create" button to create a new Event Grid topic.
- Fill in the required details for your topic, such as subscription, resource group, topic name, location, and pricing tier.
- Click on the "Review + create" button and then "Create" to provision the Event Grid topic.

**Step 3: Obtain Endpoint and Key**
- Once your topic is created, navigate to it from the Azure portal.
- In the topic menu, select "Access keys" under the "Settings" section.
- Here, you will find the endpoint URL and the access key for your Event Grid topic.
- Copy the "Endpoint" URL and save it for later use.
- Click on the "Copy" button next to the "Key 1" or "Key 2" to copy the access key.

Congratulations! You have successfully created an Event Grid topic and obtained the endpoint and key.

## Sample code

Here's the link to the sample .NET code for Event Grid. You can paste the copied the endpoint and key on their respective field: (https://github.com/mindofai/EventGridDemo)[https://github.com/mindofai/EventGridDemo]

You should be able to test sending events using event grid topic. I suggest you add breakpoints, so you'll see the events lifecycle on an Event Grid.

## Further Exploration

References:

- [Azure Event Grid Documentation](https://docs.microsoft.com/en-us/azure/event-grid/)
- [Azure Event Grid Pricing](https://azure.microsoft.com/en-us/pricing/details/event-grid/)

If you have any questions or wish to explore specific topics further, feel free to reach out to me:

- Bryan Anthony Garcia
- @mindofai
- bryananthonygarcia@live.com

Thank you for reading!
