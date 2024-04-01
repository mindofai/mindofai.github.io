---
published: true
layout: post
title: Azure Messaging Services Quickstart - Storage Queues
author: mindofai
date: 2023-08-23 12:00
tags: [Azure, Messaging, Storage Queue, Integration, Events, Service Bus]
---

<img src="{{site.baseurl}}/SQ.png"/>


Welcome to my blog post on Azure Messaging Services! In these articles, I'll delve into the intricacies of various messaging solutions offered by Azure, exploring why and when you should use them, and how to make the most out of each service.

Today, we'll specifically talk about **Azure Storage Queue**.

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

## Azure Storage Queue

<img src="{{site.baseurl}}/MS-2.png"/>

### Why Use It?

- Basic messaging solution in Azure.
- Integrates seamlessly with Azure Storage concepts.
- Suitable for scenarios where reliability and scalability are essential.

### When Not to Use It?

- Large message sizes (>64 KB).
- Long retention requirements.
- Multiple consumers for the same message.

### How to Use It?

- Supported by various SDKs.
- Accessible via standard HTTP with SAS Token/Shared Key.

## Creating a Storage Queue in Azure

Creating a Storage Queue in Azure is a straightforward process. Follow these steps to set up your Storage Queue using the Azure portal:

**Step 1: Sign in to the Azure Portal**
Navigate to the [Azure Portal](https://portal.azure.com/) and sign in with your Azure account credentials.

**Step 2: Create a Storage Account**
If you haven't already created a Storage Account, follow these steps:

- Click on the "Create a resource" button (+) in the Azure portal.
- Search for "Storage account" and select it from the results.
- Click on the "Create" button.
- Fill in the required details for your Storage Account, such as subscription, resource group, storage account name, location, and performance.
- Click on the "Review + create" button and then "Create" to provision the Storage Account.

**Step 3: Navigate to Storage Account**
Once your Storage Account is created, navigate to it by selecting it from the list of resources in the Azure portal.

**Step 4: Create a Queue**
Within your Storage Account, locate the "Queues" option in the left-hand menu under the "Data storage" section.

- Click on "Queues" to view existing queues or create a new one.
- Click on the "+ Queue" button to create a new queue.
- Enter a unique name for your queue.
- Optionally, configure additional settings such as metadata and access policies.
- Click on the "Create" button to create the queue.

**Step 5: Access and Manage Your Queue**
Once your queue is created, you can start using it to send and receive messages. You can manage your queue settings, monitor queue metrics, and configure access policies as needed.

To get the connection string for your Storage Queue, follow these steps:

- Navigate to your Storage Account in the Azure portal.
- Under "Settings," select "Access keys."
- Copy the connection string from either of the two key options provided.

Congratulations! You have successfully created a Storage Queue in Azure.

## Sample code

Here's the link to the sample .NET code for Storage Queues. You can paste the copied connection string on the connectionString field: [https://github.com/mindofai/StorageQueueDemo](https://github.com/mindofai/StorageQueueDemo/)

You should be able to test sending messages using storage queues. I sugges you add breakpoints, so you'll see the message lifecycle on a Storage Queue.

## Further Exploration

References:

- **Storage Queue**: [Get started with Azure Storage Queue using .NET](https://bit.ly/3pU7R4q)

If you have any questions or wish to explore specific topics further, feel free to reach out to me:

- Bryan Anthony Garcia
- @mindofai
- bryananthonygarcia@live.com

Thank you for reading!
