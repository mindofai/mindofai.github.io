---
published: true
layout: post
title: Why is CloudEvents with .NET and Azure Event Grid a great Event-Driven solution?
author: mindofai
date: 2023-10-11 12:00
tags: [Azure, CloudEvents, Event Grid, Events, Messaging, .NET, Event-driven]
---

<img src="{{site.baseurl}}/CE-1.png"/>

Today, we'll explore how you can leverage CloudEvents, Azure services, and the .NET framework to architect robust and scalable event-driven applications. But before we dive into the technical details, let's first understand the concept of events and why CloudEvents play a crucial role in modern event-driven architectures.

## What are Events?

Before we talk about CloudEvents, let me give you a bit of a refresher of what event-driven architecture is, by starting off with events. 

So events are a notification that something happened. A change of state. As an example in real world. Maybe, a light was turned on. From a state of a turned off light, to a turned on light, a football match has just finished, or a baby was born. These are all events.

Now, in the tech world, you might hear of things like:

- A button was pressed
- A file was uploaded
- The data has been updated

All these are events. It says that something happened. A change of state.

So, that means that an Event-Driven Architecture is…

## Event-Driven Architecture

Event-driven architecture is a design approach centered around event data. It enables distributed applications to react to these events in real-time, facilitating seamless communication and coordination between various components. This architecture is commonly employed in modern applications built with microservices, enabling agility and scalability.

Anyway, there are three key players of an event-driven system. One of them is the event producer.

### Event Producers

<img src="{{site.baseurl}}/CE-2.png"/>

So, what it does is it produces the event data. As for our first example, let’s say we have an Arduino IoT that’s used to monitor the weather. It produces the coordinates, time, and the weather details, etc. And the other is when users use an application, when a user navigates from one page to another, we’ll see patterns from the event data sent on every navigation. These event producers don’t expect anything, though. They will send the data, but that’s just what they do. To send, they don’t care if anyone receives it or not. That’s it’s only job.

### Event Consumers

<img src="{{site.baseurl}}/CE-3.png"/>

On the other end is the consumer. What the event consumer does is it handles the event data sent by a event producer. It can act on whatever the event data wants it to do, or just create a report from it. Maybe something that visualizes all the event data sent or whatever. The thing with event consumers and producers is that they’re not partners. There can be multiple producers and there can also be multiple consumers.

So, okay we have this on both ends, so what’s in the middle? Who does all the facilitating?

### Event Brokers

<img src="{{site.baseurl}}/CE-4.png"/>

It’s the event broker. It is the module that decouples both producer and consumer. It is responsible for receiving, validating, retaining, and routing the events sent by the producer to the appropriate consumer.

There are lots of event brokers out there and they have different capabilities, but we’re reppin Microsoft and they got exactly what we need here and it’s called Azure Event Grid.


## Azure Event Grid: A Fully-Managed Event Routing Service

<img src="{{site.baseurl}}/CE-5.png"/>

Azure Event Grid is a fully-managed event routing service that supports both Azure and non-Azure services. It operates on a pub-sub model, allowing seamless event consumption across environments. Azure Event Grid provides built-in event connectors for Azure services and supports custom event models, offering flexibility and scalability.

## Challenges in Event-Driven Systems

While event-driven architectures offer numerous benefits, managing event data across hybrid, edge, and multi-cloud environments poses significant challenges. Events often traverse multiple stages and use different protocols, requiring complex handling and integration.

<img src="{{site.baseurl}}/CE-6.png"/>

For this example, we got data coming from an IoT and that sends out data to an IoT gateway, then to the broker, functions, and then finally a datalake and stream analytics that eventually creates a visualization report.

So, you can see that the event data goes thru a lot. It goes thru a lot of componentry and middleware, and it may be transported thru different protocols. The pain here is that on each of these blue boxes, we have to cater these protocols and event data. It has to understand the syntax of the data coming across.

And it’s not easy to handle, coz there are multiple producers maybe coming from multiple cloud providers producing multiple events with multiple formats, and there’s little to no commonality.

<img src="{{site.baseurl}}/CE-7.png"/>

For me, that’s a problem that needs some fixing. So yeah, in conclusion, you have to work on new handlers for each event format and having to deal with new handler for each event formats and newly introduced ones? Not good.

## Introducing CloudEvents

<img src="{{site.baseurl}}/CE-8.png"/>

CloudEvents is a standardized format designed to address the challenges of event data interoperability. Developed by the Cloud Native Computing Foundation (CNCF), CloudEvents provides a common schema for describing event data, ensuring consistency, accessibility, and portability across diverse environments.

So, why cloud events? It’s because events are everywhere. The best thing they could’ve done is to make it easier for us to deal with events. Here are 3 main reasons why:

- **Consistency** - The lack of a common way of describing events means developers have to write new event handling logic for each event source.
- **Accessibility** - No common event format means no common libraries, tooling, and infrastructure for delivering event data across environments.
- **Portability** - The portability and productivity we can achieve from event data is hindered overall.

As I’ve mentioned, CloudEvents is just mainly specifications. That’s mainly it. It standardizes the event format by providing a core specification and the good thing about it is it supports all these protocols. 

<img src="{{site.baseurl}}/CE-9.png"/>

CloudEvents have bindings to support JSON, HTTP, AMQP, Kafka, Websockets and more to maximize cross-platform interopability.

### CloudEvents Core Spec sample

<img src="{{site.baseurl}}/CE-10.png"/>

So this is the core specifications of a CloudEvent schema. Nothing special here, right? Just a normal schema, and that’s by design. Mainly because they wanted it to have flexible event semantics. You can easily adjust. So it was purposely made to be dumb, but in reality, this is bare minimum that works for most if not all event formats out there. So there are two parts here. 

First is the context metadata, it’s in the name, it provides context to the event data. The specversion, the event type, the source, the subject, time, etc. and even the content type which can by xml, json, or whatever.

And ofcourse we have the actual data that needs to be sent and processed by the target handler.

### CloudEvents HTTP Binding Spec sample

<img src="{{site.baseurl}}/CE-11.png"/>

If we are to use the http protocol, let’s say we’re sending an event and we want it to abide with the CloudEvent specs. We need to put the context metadata into request headers with the prefix **ce-**. Then we put the data into the body.

## Implementing CloudEvents

<img src="{{site.baseurl}}/CE-12.png"/>

Here's a simple implementation by David Barkol to help you get started with Cloudevents: https://madeofstrings.com/2018/05/06/publish-and-consume-events-with-cloudevents-and-azure-event-grid/

Additionally, if you want to handle legacy producers, this is what it would most likely look like:

<img src="{{site.baseurl}}/CE-13.png"/>

## Conclusion

<img src="{{site.baseurl}}/CE-14.png"/>

By adopting CloudEvents and leveraging Azure Event Grid, organizations can build highly interoperable and scalable event-driven systems. Standardizing event formats with CloudEvents promotes consistency, accessibility, and portability, enabling seamless communication and integration across diverse environments. With the power of CloudEvents, .NET, and Azure, you can architect event-driven solutions that drive innovation and business agility.

## Additional Resources

- [Azure Event Grid Overview]([https://cosmos.azure.com/capacitycalculator/](https://learn.microsoft.com/en-us/azure/event-grid/overview))
- [Cloud Event Specifications](https://github.com/cloudevents/spec)
- [Azure Event Grid CloudEvents Demo](https://github.com/justinyoo/azure-event-grid-cloudevents-sample)

If you have any questions or wish to explore specific topics further, feel free to reach out to me:

- Bryan Anthony Garcia
- @mindofai
- bryananthonygarcia@live.com

Thank you for reading!
