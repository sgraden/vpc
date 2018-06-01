---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# About VPC

A Virtual Private Cloud (VPC) is a virtual network that is tied to your customer account. It offers you a cost-effective entry point that provides you with cloud security, and the ability to scale dynamically with growth. It offers you fine-grained control over your virtual infrastructure and your network traffic segmentation.

IBM Cloud VPC is part of the next generation of the IBM One Cloud platform, which redefines the traditional industry standards for performance, service growth, flexibility, and deployment freedom.

Major Benefits:

 * Quick to get started using predefined configurations
 * Flexible geographic scope
 * Secure from the ground up
 * Easily scalable
 * Sharable VPC network and resources
 * Monitor your workloads for optimal performance and efficiency

IBM Cloud VPC offers an isolated, security-rich environment. It gives you the security of a private cloud, with the agility and ease of use of a public cloud. With IBM Cloud VPC, you can manage key network services and launch Virtual Servers as needed to support your mission-critical, cloud-based applications.

A Virtual Private Cloud is ideal for cloud-native workloads. For more detailed information about the key features that IBM Cloud VPC provides, please see our [workloads example document](vpc-cloud-native.html).

## How it works

The IBM Cloud VPC offering provides logical isolation from other networks in all regions. A Virtual Private Cloud is subdivided into subnets of various sizes, using a range of private IP addresses, depending on user need. Subnets are contained within a single Zone, so they cannot span Zones--but the entire IBM Cloud VPC can consist of resources in one or more Zones. By default, all resources (such as VSIs) within the same Virtual Private Cloud can communicate to each other, regardless of their subnet.

More details about [connectivity](vpc-connectivity.html) and [security](vpc-security.html) are available.

General information about how to use IBM Cloud VPC with subnets and regions is available [here](vpc-regions-and-subnets.html).

**Note: For the Beta release, there is only one Zone and one Region.**

### Terminology 
 
For general definitions of IBM Virtual Private Cloud terminology, see the [glossary](vpc-glossary.html).

## Overview steps for setting up your IBM Cloud VPC

Here's the general flow for how to get going:

1. Create a Virtual Private Cloud.
2. Create one or more subnets in the Virtual Private Cloud in one or more zones.
3. Create a public gateway (PGW) if you want public internet traffic.
4. Create network Access Control Lists (ACLs) to manage traffic to your subnets.
5. Create security groups to manage traffic to your virtual servers.
6. Reserve a Floating IP address, and associate it with a server.
7. Create resources (servers, volumes, and so forth) in one or more zones of a Virtual Private Cloud.
8. Deploy your service or applications across those servers

### Managing your IBM Cloud VPC

You can create, name, and resize your IBM Cloud VPC using the [IBM Console](console-tutorial.html), the [CLI](cli-network-reference.html), or the [REST API](apis.html) provided by IBM Cloud. 

You can delete a Virtual Private Cloud if there are no running instances in it.

**Note: For the Beta release, there is only one Zone and one Region.**

### Managing your subnets

A subnet is an IP address range (CIDR block). Subnets are bound to a single Zone and cannot span multiple Zones or Regions. However, a subnet can span the entirety of the Zone abstractions within their Virtual Private Cloud. Subnets in the same IBM Cloud VPC are connected to each other.

#### Zones 

A Zone is an abstraction designed to assist with improved fault tolerance and decreased latency. A Zone guarantees the following properties:

 * Each Zone is an independent fault domain and it is extremely unlikely for two Zones in a region to fail simultaneously
 * Traffic between Zones in a region will be < 2 ms latency
 
**Note: For the Beta release, there is only one Zone and one Region.**

#### Reserved IP Addresses

Certain IP addresses are reserved for use by IBM when operating the Virtual Private Cloud. Here are the reserved addresses: 

 * 10.0.0.0: Network address.
 * 10.0.0.1: Reserved by IBM for the VPC router.
 * 10.0.0.2: Reserved by IBM.
 * 10.0.0.3: Reserved by IBM for future use.
 * 10.0.0.255: Network broadcast address used by IBM. 
