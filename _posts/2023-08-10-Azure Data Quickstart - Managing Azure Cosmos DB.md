---
published: true
layout: post
title: Azure Data Quickstart - Managing Azure Cosmos DB
author: mindofai
date: 2023-08-10 12:00
tags: [Azure, Database, Document, Cosmos, DB, NoSql]
---

<img src="{{site.baseurl}}/DB-1.png"/>

## What is Azure Cosmos DB?

<img src="{{site.baseurl}}/DB-2.png"/>

Azure Cosmos DB is a massively scalable NoSQL database provided as a fully managed Platform as a Service (PaaS) by Azure. It boasts a 99.999% SLA, ensuring high availability, and offers single-digit millisecond read and write latencies. Key features include automatic horizontal partitioning, elastic scaling for both storage and throughput, global distribution, and support for multiple models and APIs.

# Relational vs. Document

<img src="{{site.baseurl}}/DB-3.png"/>

Relational databases store data in rows, whereas document databases store data in documents. While relational databases have columns like "FirstName" and "LastName," document databases have properties. Relational databases are strongly typed, meaning they require consistent column values, whereas document databases allow for flexible data storage without predefined schemas.

## Measuring Performance

<img src="{{site.baseurl}}/DB-11.png"/>

### Latency

Latency refers to the overall wait time for a request to be completed, impacting user perception of performance. It is influenced by factors such as distance and network conditions.

### Throughput

<img src="{{site.baseurl}}/DB-4.png"/>

Throughput measures the database's capacity to process concurrent requests within a specific period. Request Units (RUs) serve as the currency for managing throughput, with different types of requests consuming varying amounts of RUs.

## Throughput Offerings

Azure Cosmos DB offers three throughput offerings:

1. **Provisioned throughput (manual):** Allows for the reservation of a specific number of RUs per second, guaranteeing availability but requiring manual adjustment.

<img src="{{site.baseurl}}/DB-5.png"/>

2. **Provisioned throughput (autoscale):** Automatically adjusts provisioned throughput based on workload demand, offering cost-effective scalability.
   
<img src="{{site.baseurl}}/DB-6.png"/>


3. **Serverless:** Consumption-based model where users pay only for the RUs consumed, ideal for unpredictable workloads.

<img src="{{site.baseurl}}/DB-7.png"/>

Now if you want to know how much you’ll spend for an Azure cosmos db in a monthly basis, you can check out the capacity calculator, you can input configuration parameters, your expected requests per second, and you’ll get the total cost per month with its computation.

<img src="{{site.baseurl}}/DB-8.png"/>

## Global Distribution

<img src="{{site.baseurl}}/DB-9.png"/>

Enabling global distribution in Azure Cosmos DB allows for the replication of data across multiple regions, ensuring high availability and low-latency access for users worldwide. This can be achieved with a few clicks, and multi-master configurations enable writes across all regions for enhanced resilience.

<img src="{{site.baseurl}}/DB-10.png"/>

By effectively managing Azure Cosmos DB's performance, throughput, and global distribution, organizations can leverage its capabilities to build highly scalable and responsive applications tailored to their specific requirements.

## Additional Resources

- [Azure Cosmos DB Capacity Calculator](https://cosmos.azure.com/capacitycalculator/)
- [Microsoft Docs: Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/)
- [Microsoft Learn: Azure Cosmos DB](https://learn.microsoft.com/en-us/azure/cosmos-db/)


If you have any questions or wish to explore specific topics further, feel free to reach out to me:

- Bryan Anthony Garcia
- @mindofai
- bryananthonygarcia@live.com

Thank you for reading!
