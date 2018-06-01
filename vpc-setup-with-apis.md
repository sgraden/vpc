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

# How to set up IBM Cloud VPC programmatically

For Beta testing, the Regional Infrastructure API Service (RIAS) APIs are available for setting up a Virtual Private Cloud programmatically. Follow the general steps below to accomplish a setup!

Our [API Reference](apis.html) provides a comprehensive description of the APIs available for the Beta release.

## Before you begin: 

Know your zone (for example _US-South_)

## Here are the overall steps for setting up a VPC using RIAS APIs:

1. Create a Virtual Private Cloud = give it a name

2. Create a zone = create a subnet and put it in a zone

3. Create a server (VSI) = put it on a subnet

### After you've done those 3 steps, here are some options:

 * You can attach a floating IP
 * You can use Public Gateway
 * You can get a key
 * [You can use security groups](security-groups.html)
 * [You can use network ACLs](using-acls.html)
  
 **Note:** ALL IBM Cloud REST APIs are part of IBM Cloud VPC Regional Infrastructure API Service (RIAS).
