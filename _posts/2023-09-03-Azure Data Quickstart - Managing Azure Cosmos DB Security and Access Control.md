---
published: true
layout: post
title: Azure Cosmos DB Quickstart - Managing Azure Cosmos DB Security, Access Control, Backup, and Restore
author: mindofai
date: 2023-09-05 12:00
tags: [Azure, CosmosDB, Data, Access Control, Security, Network, Encryption, Backup, Restore]
---

This is the last part of the Azure Cosmos DB Quickstart and we'll talk about Security, Access Control, Backup, and Restore. Ensuring the confidentiality, integrity, and availability of your data is the top priority. We explore network-level security measures, authentication mechanisms, and authorization policies to safeguard your Azure Cosmos DB instance from unauthorized access and malicious activities.

### Network-level Security

Azure Cosmos DB offers network-level security features to control access to your database account.

#### IP Firewall
By configuring an IP firewall, you can restrict access to your Azure Cosmos DB account to specific IP addresses or ranges. This ensures that only authorized clients with approved IP addresses can connect to your database account. The account is accessed via its public IP address.

#### Virtual Network through Service Endpoint
Alternatively, you can use a virtual network (VNet) with a service endpoint to secure network access. This approach allows you to connect to your Azure Cosmos DB account only from approved virtual networks. The account is still accessed via its public IP address, but access is restricted to clients hosted within the approved VNets.

#### Virtual Network through Private Endpoint
For enhanced security, you can utilize private endpoints within a virtual network. With this setup, access to the Azure Cosmos DB account is restricted to traffic originating from approved virtual networks. Furthermore, the account is accessed only via private IP addresses that are local to the VNet, adding an extra layer of network-level security.

### Authentication and Authorization

Azure Cosmos DB supports various authentication and authorization mechanisms to control access to your data.

#### Primary/Secondary Keys
The primary and secondary keys provide a shared secret for authentication and authorization. These keys can be used for both management and data operations on the database account. They come in both read-write and read-only variants, offering flexibility in access control.

#### Resource Token Authentication
Resource tokens provide a granular control mechanism for access to specific resources within your Azure Cosmos DB account. Unlike primary/secondary keys, resource tokens allow for fine-grained access control at the container, partition, document, stored procedure, trigger, and UDF levels. This enables you to create users at the database level and assign permissions at the user level. Resource tokens are generated from desired permissions, providing a secure method for managing access to your data.

#### Azure Active Directory Integration
Integration with Azure Active Directory (Azure AD) allows you to authenticate requests using Azure AD identities. With Azure AD integration, you can enforce role-based access control (RBAC) and assign fine-grained permissions to users based on their roles. This eliminates the need for master keys or resource tokens and provides a more secure authentication mechanism using Azure AD identities.

## Encryption

Azure Cosmos DB supports server-side and client-side encryption to protect your data.

### Server-side Encryption

#### Built-in Server-side Encryption
Azure Cosmos DB provides built-in server-side encryption using Microsoft-managed keys. This encryption ensures that data is always encrypted at rest and in transit, providing enhanced security for your database. Encryption cannot be disabled, and data is automatically encrypted on the server side, eliminating the need for manual encryption processes.

#### Customer-managed Keys
In addition to built-in encryption, Azure Cosmos DB also supports customer-managed keys for server-side encryption. This allows you to use your own encryption keys for an extra layer of security. However, managing and rotating these keys is your responsibility, and losing the keys can result in data loss or unauthorized access. Customer-managed keys are recommended only if mandated by specific vertical or industry requirements.

### Client-side Encryption

Azure Cosmos DB also supports client-side encryption for additional security measures.

#### Data Encryption
With client-side encryption, data is encrypted on the client side before being stored in Azure Cosmos DB. This ensures that data remains encrypted throughout its lifecycle, providing an extra layer of protection against unauthorized access. Client-side encryption can be applied to specific properties only, allowing you to encrypt sensitive data while leaving other properties unencrypted. Encryption can be randomized or deterministic, depending on your security requirements.

## Backup & Restore

Azure Cosmos DB offers backup and restore capabilities to protect your data against accidental deletion, corruption, or loss.

### Backup Options

#### Periodic Backup
Azure Cosmos DB provides automatic and free periodic backups, taken at regular intervals. You can configure retention settings ranging from 8 hours to 30 days, with the option to retain up to 720 copies of backups (additional charges may apply for more than 2 copies). However, restoring from backups requires contacting support.

#### Continuous Backup
For more comprehensive backup solutions, Azure Cosmos DB offers continuous backup as an additional service (additional charges apply). Continuous backup allows for point-in-time restores within the last 30 days, providing greater flexibility in data recovery. This feature is available for SQL API and MongoDB API only and allows for self-service restore via the Azure portal.
