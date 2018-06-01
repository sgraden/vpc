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

# Setting up security in your IBM Cloud VPC

![Security for Beta](/images/VPC-internal-beta.png)

Figure: A customer can subdivide a Virtual Private Cloud with subnets. 

* Traffic to and from a subnet can be controlled by Access Control Lists (ACLs)
* A Security Group (SG) can control the traffic at the VSI level
* Set up a public gateway for access to the internet

## Terminology

This [glossary](vpc-glossary) provides definitions and descriptions of ACLs and SGs, and the actions you can perform with them. The sectio nthat follows descibes

### Access Control List
An **Access Control List (ACL)** can manage (that is, it can allow or deny) ingress and egress traffic for a subnet. An ACL is stateless, which means that ingress and egress rules must be specified separately and explicitly. Each ACL consists of rules, based upon a *source IP*, *source port*, *destination IP*, *destination port*, and *protocol*. 

In IBM Cloud VPC, every subnet is created with a default ACL, which allows inbound and outbound traffic, but customers can create custom ACLs. Only one ACL is attached to a subnet at any time, but one ACL can be attached to multiple subnets. For more information about how to use ACLs during the Beta release, please see our [ACL guide](using-acls.html).

**Available User Actions**

  * List all Subnets and see ACL associations
  * List all ACLs
  * List all rules in certain ACLs (Ingress + egress categories)
  * CRUD (Create, Read, Update, Delete) the ACL
  * Charges up to 25 ingress and egress rules are free (All rules are free during Beta release.)

### Security Group
A **security group** acts as a virtual firewall that controls the traffic for one or more servers (VSIs). A security group is a collection of 5-tuple rules that specify whether to allow traffic for an associated VSI. 

When a customer launches a VSI, he or she can associate one or more security groups with that VSI. Given the correct permissions, customers can modify security group rules using the IBM Console, the CLI, or the API.

**Available User Actions**

  * List all security groups (SG)
  * List the server's SG associations
  * List all SG rules and associations on a specific SG
  * List all rules in certain SG (Ingress + egress categories)
  * CRUD (Create, Read, Update, Delete) the SG
  * Specify "allow" actions

For more information about how to create a VSI that uses security groups, and more about the limitations of security groups during the Beta release, please refer to [our security groups guide](security-groups.html).

### End-to-end encryption

Although IBM Cloud VPC does not provide end-to-end encryption, it allows for it. For example, if you have a secure endpoint on a virtual server (for example, an HTTPS server on Port 443), you can attach a floating IP to that server, and then your connection is end-to-end encrypted from the client to the server on Port 443.  Nothing in the path forces a decryption.

Note, however, that if you use an insecure protocol such as HTTP on Port 80, your data is in the clear from end to end.
