---

copyright:
  years: 2018
lastupdated: "2018-07-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Overview steps for setting up your IBM Cloud VPC

Here's the general flow for how to get going:

1. Create a Virtual Private Cloud.
2. Create one or more subnets in the Virtual Private Cloud in one or more zones.
3. Create a public gateway (PGW) if you want public internet traffic.
4. Create network Access Control Lists (ACLs) to manage traffic to your subnets.
5. Create security groups to manage traffic to your virtual servers.
6. Reserve a Floating IP address, and associate it with a server.
7. Create servers in one or more zones of a Virtual Private Cloud.
8. Deploy your service or applications across those servers

## Overview of managing your IBM Cloud VPC

You can create, name, and resize your {{site.data.keyword.cloud}} VPC using the [IBM Console](console-tutorial.html), the [CLI](cli-network-reference.html), or the [REST API](apis.html) provided by IBM Cloud. 

You can delete a Virtual Private Cloud if there are no running instances in it.

## Overview of managing your subnets

A subnet is an IP address range (CIDR block). Subnets are bound to a single Zone and cannot span multiple Zones or Regions. However, a subnet can span the entirety of the Zone abstractions within their Virtual Private Cloud. Subnets in the same IBM Cloud VPC are connected to each other.

**Note: For the Beta release, there is only one Zone and one Region.**

### Zones

A Zone is an abstraction designed to assist with improved fault tolerance and decreased latency. A Zone guarantees the following properties:

 * Each Zone is an independent fault domain and it is extremely unlikely for two Zones in a region to fail simultaneously
 * Traffic between Zones in a region will be < 2 ms latency

**Note: For the Beta release, there is only one Zone and one Region.**

### Reserved IP Addresses

Certain IP addresses are reserved for use by IBM when operating the Virtual Private Cloud. Here are the reserved addresses:

 * 10.0.0.0: Network address.
 * 10.0.0.1: Reserved by IBM for the VPC router.
 * 10.0.0.2: Reserved by IBM.
 * 10.0.0.3: Reserved by IBM for future use.
 * 10.0.0.255: Network broadcast address used by IBM.
