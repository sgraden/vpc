---

copyright:
  years: 2018
lastupdated: "2018-06-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# VPC Glossary

## Access Control List
An Access Control List (ACL) can manage (that is, it can allow or deny) ingress and egress traffic for a subnet. An ACL is stateless. Each ACL consists of rules, based upon a _source IP_, _source port_, _destination IP_, _destination port_, and _protocol_.

In IBM Cloud VPC, every subnet is created with a default ACL, which allows inbound and outbound traffic, but customers can create custom ACLs. Only one ACL is attached to a subnet at any time, but one ACL can be attached to multiple subnets.

## Floating IP addresses
Floating IP addresses are public IP addresses that are provided by the system. You cannot bring your own public IP. Floating IP addresses are reachable from the internet, and they can be associated to an instance (for example, a VSI, a load balancer, and a VPN gateway). You can reserve a Floating IP address from the pool of available Floating IP addresses provided by IBM, and you can associate or unassociate it to (or from) any instance in the same Virtual Private Cloud.

## Profile
A Profile is a popular combination of vCPU and RAM that can be instantiated quickly to start up a virtual server instance (VSI). Three families of profiles are supported: Balanced, Compute, and Memory.


## Public Gateway
A Public Gateway (PGW) enables a subnet (with all the VSIs attached to the subnet) to connect to the internet. Note that subnets are private by default; however, optionally, you can create a PGW and attach a subnet to the PGW. After a subnet is attached to the PGW, all the VSIs in that subnet can connect to the internet.

PGW uses many-to-1 NAT, which means that thousands of VSIs with private addresses will use 1 public IP address to talk to the public internet. PGW does not enable the internet to initiate a connection with those instances. Use the CRUDPGW API to attach and detach subnets to and from your PGW.

## Region
An IBM Cloud VPC spans multiple regions. Each region contains multiple Zones, which represent independent fault domains.

## Security Group
A security group acts as a virtual firewall that controls the traffic for one or more servers (VSIs). A security group is a collection of 5-tuple (source IP and port, destination IP and port, and protocol) rules that specify whether to allow traffic for an associated VSI. When a customer launches a VSI, he or she can associate one or more security groups with that VSI. Given the correct permissions, customers can modify security group rules.

## Subnet
A subnet is an IP address range, bound to a single Zone, which cannot span multiple Zones or Regions. A subnet can span the entirety of the Zone in the IBM Cloud VPC.

## Zone
An independent fault domain. A Zone is an abstraction designed to assist with improved fault tolerance and decreased latency. A Zone guarantees the following properties:
		
 * Each Zone is an independent fault domain and it is extremely unlikely for two Zones in a region to fail simultaneously
 * Traffic between Zones in a region will be < 2 ms latency
    
## External Links
For more general information, here are some external links you can follow:
 * [What is many-to-one NAT?](https://en.wikipedia.org/wiki/Network_address_translation)
