---

copyright:
  years: 2018
lastupdated: "2018-08-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Setting up connectivity in your IBM Cloud VPC

In this document, you'll find concepts that describe use cases and capabilities within {{site.data.keyword.cloud}} VPC for subnets, Floating IP addresses, and VPN connections.

**Figure: A customer can subdivide a Virtual Private Cloud with subnets, and each subnet can reach the public internet, if desired.**

![Beta](/images/vpc-connectivity.png)

As shown in the figure:

* Subnets can connect to the public internet through an optional Public Gateway (PGW).
* You can assign a Floating IP address (FIP) to any VSI to reach it from the internet, or vice versa.
* Subnets in the IBM Cloud VPC offer private connectivity; they can talk to each other over a private link. Customers do not need to set up any routes.
* For more information, see our [Planned Experience document](about.html#ibm-virtual-private-cloud-experience).

## Terminology

This [glossary](vpc-glossary.html) contains definitions and information about terms used in this document for IBM Cloud VPC.

## Characteristics of subnets in VPC

A subnet consists of a specified IP address range (CIDR block). Subnets are bound to a single Zone, and they cannot span multiple Zones or Regions. However, a subnet can span the entirety of the Zone abstractions within their Virtual Private Cloud. Subnets in the same IBM Cloud VPC are connected to each other.

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

### Use a Public Gateway for external connectivity of a subnet

A **Public Gateway (PGW)** enables a subnet (with all the VSIs attached to the subnet) to connect to the internet. Note that subnets are private by default; however, optionally, you can create a PGW and attach a subnet to the PGW. After a subnet is attached to the PGW, all the VSIs in that subnet can connect to the internet.

PGW uses _Many-to-1 NAT_, which means that thousands of VSIs with private addresses will use 1 public IP address to talk to the public internet. PGW does not enable the internet to initiate a connection with those instances. Use the API to attach and detach subnets to and from your PGW.

### Use a Floating IP address for external connectivity of a VSI 
**Floating IP addresses** are IP addresses that are provided by the system and are reachable from the public internet.

You can reserve a Floating IP address from the pool of available Floating IP addresses provided by IBM, and you can associate or unassociated it to (or from) any instance in the same Virtual Private Cloud, by means of the vNIC for that instance. You cannot bring your own public IP. Any Floating IP address can be associated to various types of virtual server instances (VSIs), for example, a load balancer or a VPN gateway.

Your Floating IP address cannot be associated with multiple interfaces. You must specify the interface on the VSI that will be associated with that individual Floating IP. That interface also will have a private IP address. The backend system performs _1-to-1 NAT_ operations between the Floating IP and the Private IP of that interface. A Floating IP is released only when you specifically request the release action. 

**Note: Associating a Floating IP address with a VSI removes the VSI from the PGW's Many-to-1 NAT mentioned previously.**

For more information about NAT operations, please refer to [the related Internet RFC document ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.faqs.org/rfcs/rfc1631.html){: new_window}.

**Notes:**
* **Associating a Floating IP address with a VSI removes the VSI from the PGW's Many-to-1 NAT mentioned previously.**
* **Currently, Floating IP supports only IPv4 addresses.**

### Use VPN for secure external connectivity
Virtual Private Network (VPN) service is available for users to connect to their IBM Cloud VPC from the internet, securely. For step-by-step instructions, please see our [IBM Console UI guide](console-tutorial.html).

**VPN Capabilities**
  * Ability to CRUD (Create, Read, Update and Delete) VPN service (site-to-site IPSEC VPN) for handling data transfer
  * Ability to associate VPN service to a customer's IBM Cloud VPC or virtual network
  * Ability to identify customer's on-site subnets either by static definition or by dynamic routing
  * Support for secure ciphers such as SHA256, AES, 3DES, IKEv2
  * Built-in service reliability
  * Continuous monitoring of VPN connection health
  * Support for both initiator and responder modes; that is, traffic may be initiated from either side of the tunnel
