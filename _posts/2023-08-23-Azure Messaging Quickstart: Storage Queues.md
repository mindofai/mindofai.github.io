---
published: true
layout: post
title: Azure Messaging Services Quickstart - Storage Queues
author: mindofai
date: 2023-08-23 12:00
tags: [Azure, Messaging, Storage Queue, Integration, Events, Service Bus]
---

## Introduction

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

## Sample code

Here's the link to the sample .NET code for Storage Queues: [https://github.com/mindofai/StorageQueueDemo](https://github.com/mindofai/StorageQueueDemo/)


## Further Exploration

References:

- **Storage Queue**: [Get started with Azure Storage Queue using .NET](https://bit.ly/3pU7R4q)


If you have any questions or wish to explore specific topics further, feel free to reach out to me:

- Bryan Anthony Garcia
- @mindofai
- bryananthonygarcia@live.com

Thank you for reading!
