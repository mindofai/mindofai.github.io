---
published: true
layout: post
title: Azure Messaging Services Quickstart - Event Hubs
author: mindofai
date: 2023-08-27 12:00
tags: [Azure, Messaging, Event Hub, Storage Account, Blob, Integration, Events, Service Bus]
---

<img src="{{site.baseurl}}/EH.png"/>


Welcome to my blog post on Azure Messaging Services! In these articles, I'll delve into the intricacies of various messaging solutions offered by Azure, exploring why and when you should use them, and how to make the most out of each service.

Today, we'll specifically talk about **Azure Event Hub**.

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
## Azure Event Hub

<img src="{{site.baseurl}}/MS-4.png"/>

### Why Use It?

- Ideal for stream and batch processing.
- Enables real-time data analytics.
- Managed Kafka with minimal overhead.

### When Not to Use It?

- Not required for batch/stream processing.
- Testing and debugging locally might be cumbersome.
- Consider cost implications.

### How to Use It?

- Supported by various SDKs and Azure Functions Trigger.
- Integrates seamlessly with Azure native services like Event Grid and Stream Analytics.

## Creating an Event Hub & Blob Storage in Azure
Follow these steps to create an Event Hub and connect it to Blob Storage in Azure:

**Step 1: Sign in to the Azure Portal**
Navigate to the [Azure Portal](https://portal.azure.com/) and sign in with your Azure account credentials.

**Step 2: Create an Event Hub Namespace**
- Click on the "Create a resource" button (+) in the Azure portal.
- Search for "Event Hubs" and select it from the results.
- Click on the "Create" button to create a new Event Hubs namespace.
- Fill in the required details for your namespace, such as subscription, resource group, namespace name, location, and pricing tier.
- Click on the "Review + create" button and then "Create" to provision the Event Hubs namespace.

**Step 3: Create an Event Hub**
- Once your namespace is created, navigate to it from the Azure portal.
- In the namespace menu, select "Event Hubs" under the "Entities" section.
- Click on the "Add" button to create a new Event Hub.
- Enter a unique name for your Event Hub and configure other settings as needed.
- Click on the "Create" button to create the Event Hub.

**Step 4: Configure Blob Storage**
- Navigate to the Blob Storage account you want to connect to the Event Hub.
- In the Blob Storage account menu, select "Events" under the "Blob service" section.
- Click on the "Add Event Subscription" button to create a new event subscription.
- Enter a name for your subscription and select the Event Hub namespace you created earlier.
- Choose the event types you want to subscribe to, such as "BlobCreated" or "BlobDeleted."
- Specify the endpoint where you want Event Hubs to send events. This could be a webhook URL or the endpoint of another Azure service.
- Click on the "Create" button to create the subscription.


Congratulations! You have successfully created an Event Hub and connected it to Blob Storage in Azure.

## Sample code

Here's the link to the sample .NET code for Storage Queues. You can paste the copied connection string on the connectionString field: (https://github.com/mindofai/EventHubDemo)[https://github.com/mindofai/EventHubDemo]

You should be able to test sending events using event hub and blob storage. I sugges you add breakpoints, so you'll see the events lifecycle on an Event Hub.

## Further Exploration

References:

- [Azure Event Hubs Documentation](https://docs.microsoft.com/en-us/azure/event-hubs/)
- [Azure Blob Storage Documentation](https://docs.microsoft.com/en-us/azure/storage/blobs/)
- [Azure Event Hubs Pricing](https://azure.microsoft.com/en-us/pricing/details/event-hubs/)
- 
If you have any questions or wish to explore specific topics further, feel free to reach out to me:

- Bryan Anthony Garcia
- @mindofai
- bryananthonygarcia@live.com

Thank you for reading!
