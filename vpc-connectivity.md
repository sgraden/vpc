---

copyright:
  years: 2018
lastupdated: "2018-08-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Setting up connectivity in your IBM Cloud VPC

![Beta](/images/vpc-beta.png)

**Figure: A customer can subdivide a Virtual Private Cloud with subnets, and each subnet can reach the public internet, if desired.** 

* Subnets can connect to the public internet through an optional Public Gateway (PGW). 
* You can assign a Floating IP address (FIP) to a VSI to reach it from the internet, or vice versa. 
* At General Availablity, you'll use VPN and Direct Link to obtain access to the internet and to your on-premise data centers, securely. VPN will be available later in the Beta timeframe, Direct Link will be available after GA. For more information, see our [Planned Experience document](about.html#planned-ibm-virtual-private-cloud-experience).

## Private connectivity within your IBM Cloud VPC
Subnets in the IBM Cloud VPC can talk to each other over a private link. Customers do not need to set up any routes.

## Terminology

This [glossary](vpc-glossary.html) contains definitions and information about termsused in this document for IBM Cloud VPC.

### Use a Public Gateway For External Connectivity of a Subnet
A **Public Gateway (PGW)** enables a subnet (with all the VSIs attached to the subnet) to connect to the internet. Note that subnets are private by default; however, optionally, you can create a PGW and attach a subnet to the PGW. After a subnet is attached to the PGW, all the VSIs in that subnet can connect to the internet. 

PGW uses _Many-to-1 NAT_, which means that thousands of VSIs with private addresses will use 1 public IP address to talk to the public internet. PGW does not enable the internet to initiate a connection with those instances. Use the API to attach and detach subnets to and from your PGW.


### Use a Floating IP address for external connectivity of a VSI 
**Floating IP addresses** are IP addresses that are provided by the system and are reachable from the public internet. You can reserve a Floating IP address from the pool of available Floating IP addresses provided by IBM, and you can associate or unassociate it to (or from) any instance in the same Virtual Private Cloud, by means of the vNIC for that instance. You cannot bring your own public IP. Any Floating IP address can be associated to various types of virtual server instances (VSIs), for example, a load balancer or a VPN gateway. 

Your Floating IP address cannot be associated with multiple interfaces. You must specify the interface on the VSI that will be associated with that individual Floating IP. That interface also will have a private IP address. The backend system performs _1-to-1 NAT_ operations between the Floating IP and the Private IP of that interface. A Floating IP is released only when you specifically request the release action. 

**Note: Associating a Floating IP address with a VSI removes the VSI from the PGW's Many-to-1 NAT mentioned previously.**

For more information about NAT operations, please refer to [the related Internet RFC document](http://www.faqs.org/rfcs/rfc1631.html).

**Note: Currently, Floating IP supports only IPv4 addresses.**

### Use VPN for Secure External Connectivity
Virtual Private Network (VPN) service is available for users to connect to their IBM Cloud VPC from the internet, securely.

**Available User Action**
  * Ability to CRUD (Create, Read, Update and Delete) VPN service (site-to-site IPSEC VPN) for handling data transfer
  * Ability to associate VPN service to a customer's IBM Cloud VPC or virtual network
  * Ability to identify customer's on-site subnets either by static definition or by dynamic routing
  * Support for secure ciphers such as SHA256, AES, 3DES, IKEv2
  * Built-in service reliability to achieve high SLA
  * Continuous monitoring of VPN connection health
  * Support for both initiator and responder modes; that is, traffic may be initiated from either side of the tunnel
