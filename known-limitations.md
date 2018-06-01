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

# Known Limitations of the Beta release

Known limitations may be changing during the Beta release, as we add capabilities, so feel free to check back with this document from time to time. You'll find an overview at the beginning of this document and a more detailed list near the end of the document.

## Overview (TL;DR)

Here's an overview of what's not supported for the Beta release as of the date of this document.

### Features not supported during Beta

* Access to existing IBM Cloud Infrastructure Classic resources such as bare metal or Direct Link (that is, there's no peering)
* IBM Cloud VPC Private Services Endpoints (phasing in during Beta)

### APIs not supported during Beta

Only a subset of Network and Compute APIs are supported during the Beta release. For a summary of what's supported, see the [API overview](api-summary.html), and for more details see the [API Spec](apis.html).

The following APIs are not supported in this release.

| Component | Functions | Comments |
|------|------|--------|
| **Network:**  |   |   |
| Network_ACLs | Partly supported | [Here's the Doc](using-acls.html) |
| Security Groups | Partly supported |  [Here's the Doc](security-groups.html) |
| **Compute:** |   |   |
| Images | Create/Delete not supported | Only Ubuntu 16.04, CentOS 7.X |
| Network_Interfaces | Get (no create, delete, update) | Only one interface supported |
| Volume_Interfaces | Not supported |   |
| **Storage:** |   |   |
| Volumes | Not supported |   |
| Snapshots | Not supported |  |
| **Geo:** |   |   |
| Regions | Get | Only one region |
| Zones | Get | Only one zone |
| **Elastic Load Balancer** |   |  Coming later in Beta |
| **VPN** |   |  Coming later in Beta |

### Subnet range constraint in IBM Console UI for Beta

Our current IBM Console UI enforces that customers must pick a subnet prefix from the fixed range. This requirement applies only until address prefixes are available in the release, then customer will have the flexibility to add new address prefix pools.

## Here are the Details

This section gives a detailed list of unsupported features and use cases for this Beta release. You might find this list useful in case of troubleshooting or some specific questions that might arise.

### Features Not Supported for Beta

1. A Virtual Private Cloud cannot be peered with other Virtual Private Clouds.

2. A Virtual Private Cloud can be peered only with the IBM Cloud Classic environment. IBM Cloud VPC peering with Classic can be established only during Virtual Private Cloud creation, and only for existing IBM Cloud Infrastructure (Softlayer) customers who have Virtual Router Function (VRF) accounts. If the customer's account is non-VRF, an error is displayed, asking the customer to convert ther account if Classic peering is desired. (Most accounts already have VRF. If you don't know, you can open a support ticket.)

3. A customer can peer only one Virtual Private Cloud with Classic, not multiple Virtual Private Clouds.

4. A customer who enables peering between IBM Cloud VPC and IBM Cloud Classic, must make sure there is no address conflict. IBM won't do any sanity check for the customers, for now.

5. (Supported later in Beta release timeframe) After IBM Cloud VPC Classic peering is established, existing virtual machines or bare metal servers on Classic won't be shown as part of the Virtual Private Cloud. Those resources won't be attached to any subnets in the Virtual Private Cloud. However, newly provisioned servers will be attached to subnets in the Virtual Private Cloud and they can communicate (ping, send data) to other resources in the IBM Cloud Classic infrastructure (SoftLayer).

6. Customers cannot migrate their existing IBM Cloud VSI or bare-metal servers into their IBM Cloud VPC.

7. For a customer to use other IBM Cloud services (such as Direct Link) or ping their existing IBM Cloud servers from their Virtual Private Cloud, peering must be enabled during the IBM Cloud VPC creation. Each customer can have only 1 VPC with peering enabled. In total, each customer can have 5 VPCs.

8. Customers won't be able to set up custom routes in the IBM Cloud VPC. All the subnets in Virtual Private Cloud can communicate with each other by default.

9. IBM Cloud VPC won't support multicast or broadcast domains.

10. IBM Cloud VPC has nothing to do with the fast provisioning of the VSIs. It's targeted by a different work stream.

11. IBM Cloud VPC does not provide end-to-end encryption, but it supports it.

12. Here's the list of core IBM Cloud services that an IBM Cloud VPC customer can use: NTP, Logging, DNS resolvers. Other services are not accessable.

13. A subnet cannot be on multiple Zones.

14. A customer cannot attach or detach a subnet to or from an availability Zone.

15. A customer cannot resize a subnet.

16. A customer cannot provision a bare metal server in IBM Cloud VPC.

17. IBM Cloud Classic resources cannot be in the same subnet in the IBM Cloud VPC. 

18. There's no support for IPv6, neither as bring your own private IP in VPC, nor as Floating Public IP.

19. The customer may not use his or her own public IP as a Floating IP. The floating IP pool is provided by IBM.

20. A Floating IP is bound to a Zone. For example, a Floating IP reserved from a pool in Zone 1 won't be assigned to a VSI in Zone 2 in the same VPC.

21. A customer cannot move private IP addresses between VSIs.

22. A customer cannot move a network interface between VSIs.

23. A customer cannot designate the specific IP address of the VSI, only specify the IP range for the subnet. Once the customer attaches a VSI to a subnet, the system assigns a private IP from that subnet.

24. IBM Cloud VPC comes with its own Network as a Service tools such as LBaaS, ACLs, and security groups. A customer cannot use their network appliances (for example, a Vyatta Gateway or other load balancer) to control any resource in the IBM Cloud VPC. A customer cannot use their loadbalancer or security groups services in IBM Cloud Classic (SoftLayer) to control their resources in the IBM Cloud VPC.

25. The public gateway does not allow the traffic to be intiated from the Internet to a VSI in the IBM Cloud VPC. For that purpose, a floating IP must be used.

26. ACL is stateless, so return traffic must be allowed explicity in ACL rules.
