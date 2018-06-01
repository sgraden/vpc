---

copyright:
  years: 2018
lastupdated: "2018-06-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Setting up connectivity in your IBM Cloud VPC

![Internal Beta](/images/VPC-internal-beta.png)

Figure: All subnets within the IBM Cloud VPC are connected to each other by a private link. 

* Subnets can connect to the public internet through an optional Public Gateway (PGW). 
* You can assign a Floating IP address (FIP) to a VSI to reach it from the internet, or vice versa. 
* At General Availablity, you'll use VPN and Direct Link to obtain access to the internet and to your on-premise data centers, securely. VPN will be available later in the Beta timeframe, Direct Link will be available after GA.

## Private connectivity within your IBM Cloud VPC
Subnets in the IBM Cloud VPC can talk to each other over a private link. Customers do not need to set up any routes.

## Terminology

This [glossary](vpc-glossary.html) contains definitions and information about commonly-used terms for IBM Cloud VPC.

### Use a Public Gateway For External Connectivity of a Subnet
A **Public Gateway (PGW)** enables a subnet (with all the VSIs attached to the subnet) to connect to the internet. Note that subnets are private by default; however, optionally, you can create a PGW and attach a subnet to the PGW. After a subnet is attached to the PGW, all the VSIs in that subnet can connect to the internet. 

PGW uses Many-to-1 NAT, which means that thousands of VSIs with private addresses will use 1 public IP address to talk to the public internet. PGW does not enable the internet to initiate a connection with those instances. Use the CRUDPGW API to attach and detach subnets to and from your PGW.

For more general information, here are some external links you can follow:

 * [What is a public gateway?](https://en.wikipedia.org/wiki/Default_gateway)
 * [What is a subnet?](https://en.wikipedia.org/wiki/Subnetwork)
 * [What is a Floating IP address?](https://wiki.lunanode.com/index.php/Floating_IP_addresses)
 * [What is MANY-TO-ONE NAT?](https://en.wikipedia.org/wiki/Network_address_translation)
 * [What is VPN?](https://en.wikipedia.org/wiki/Virtual_private_network)

### Use Floating IP For External Connectivity of a VSI 
**Floating IP addresses** are public IP addresses that are provided by the system. You cannot bring your own public IP. Floating IP addresses are reachable from  the internet, and they can be associated to an instance (for example, a VSI, a loadbalancer, and a VPN gateway). You can reserve a Floating IP address from the pool of available Floating IP addresses provided by IBM, and you can associate or unassociate it to (or from) any instance in the same Virtual Private Cloud. 

Your Floating IP cannot be associated with multiple interfaces. You must specify the interface of VSI that will be associated with the Floating IP. That interface will also have private IP address. The backend system will perform 1-TO-1 NAT operations between the Floating IP and the Private IP of that interface. A Floating IP is released only when you specifically request the release action. 

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
