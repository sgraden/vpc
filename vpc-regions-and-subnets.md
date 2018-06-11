---

copyright:
  years: 2018
lastupdated: "2018-06-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Using an IBM Cloud VPC with regions and subnets

This document describes how regions and subnets will be incorporated into your IBM Cloud VPC in the upcoming GA release, when multiple zones and regions are available. **Note: For the Beta release, there is only one Zone and one Region.**

Also, this document lists the available or restricted IP address ranges and available user actions, which DO apply in this Beta release. **Note: For the Beta release, you have to create your VPC before you create your subnet(s) within that VPC.**

For step-by-step instructions on setting up your subnets in IBM Cloud VPC Beta release, please refer to our [Example Code tutorial](example-code.html). 


## IBM Cloud VPC and Regions

An IBM Cloud VPC spans multiple regions. Each region contains multiple Zones, which represent independent fault domains. 

![vpc-example-graphic](images/perfect-vpc-image.png)


## IBM Cloud VPC and Subnets

Customers can divide an IBM Cloud VPC into subnets. (A subnet is an IP address range, bound to a single Zone, which cannot span multiple Zones or Regions.) A subnet can span the entirety of the Zone in the IBM Cloud VPC. 

All the subnets in an IBM Cloud VPC can reach one another though private L3 routing by an implicit router. The customer does not need to set up any routers or routes.

CIDRs are allocated to each Zone. Customers can pick a range of IP addresses from the existing CIDRs for the new subnet. If the Zone CIDR is not suitable, one of the existing CIDRs can be edited or a new CIDR can be added to Zone. These are available IP addresses, as defined in **RFC 1918**.

 * 10.0.0.0 – 10.255.255.255
 * 172.16.0.0 – 172.31.255.255
 * 192.168.0.0 – 192.168.255.255

**Note: IPv6 support will come later, it is not available in the Beta release.**

### The following addresses are reserved addresses in a subnet:

  * Network address (first address in the CIDR range)
  * Default gateway address (second address in the CIDR range)
  * Name server (Third address in the CIDR range)
  * Reserved address (4th addresss in the CIDR range)
  * Broadcast address (last address in the CIDR range)
  
### Available User Actions
  * CRUD (Create, Read, Update, Delete) a Virtual Private Cloud.
  * Provide a unique name to a Virtual Private Cloud.
  * CRUD a subnet.

### Creating a Subnet:
  * a) You can create a subnet by providing the size of subnet you need, such as the number of addresses supported (for example, 1024)
  * b) You can create a subnet by providing a CIDR range (such as 10.0.0.1/29)
  
### Deleting a Subnet:
  * You cannot delete a subnet if resources (such as a Virtual Server Instance (VSI)) are in use in that subnet, the resources must be deleted first.
  * You can associate or unassociate a VSI with a subnet (it requires vNIC addition and bandwidth selection)
  * You can NOT resize the existing subnet. For example, 10.10.10.0/24 cannot be resized to 10.5.1.3/20
