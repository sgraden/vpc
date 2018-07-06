---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-06"

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

A Virtual Private Cloud is ideal for cloud-native workloads. For a detailed list of the key features that IBM Cloud VPC can provide for your workloads, skip to [this section](about.html#use-ibm-cloud-vpc-for-cloud-native-workloads).

## How it works

The IBM Cloud VPC offering provides logical isolation from other networks in all regions. A Virtual Private Cloud is subdivided into subnets of various sizes, using a range of private IP addresses, depending on user need. Subnets are contained within a single Zone, so they cannot span Zones--but the entire IBM Cloud VPC can consist of resources in one or more Zones. By default, all resources (such as VSIs) within the same Virtual Private Cloud can communicate to each other, regardless of their subnet.

More details about [connectivity](vpc-connectivity.html) and [security](vpc-security.html) are available.

General information about how to use IBM Cloud VPC with subnets and regions is available [here](vpc-regions-and-subnets.html).

**Note: For the Beta release, there is only one Zone and one Region.**

### Terminology 
 
For general definitions of IBM Virtual Private Cloud terminology, see the [glossary](vpc-glossary.html).

## Use IBM Cloud VPC for cloud-native workloads

IBM Cloud Virtual Private Cloud (VPC) focuses on cloud-native workloads. We aim to create the best cloud for cognitive, AI, and Machine Learning workloads, which are important types of cloud-native workloads. Meanwhile, we continue supporting IBM Cloud Classic for traditional workloads.

The feature set described in the folllowing section is part of the **Planned IBM Cloud VPC experience**, and many are already available in the Beta release.

### Cloud-Native workloads generally require:

 * IBM Cloud VPC to create & manage isolated application environments through the API
 * Network topologies with BYoIP
 * Security Groups and Network ACLs for flexible, API-driven topologies
 * Availability Zones with high-speed & low-latency connections across Regions
 * Auto-scaling for groups
 * Scaling up or down by 1000s of servers per day
 * Scalable & reliable LBaaS with certificate management
 * Scalable & reliable monitoring
 * Illusion of infinite capacity 


### Example: A Cloud Native Workload's more specific IaaS Requirements

 * Scalable virtual networks
 * Support for availability zones (HA)
 * High-speed networking and storage
 * Always On services (control plane)
 * Multiple regions for disaster recovery and resilience
 * Most core services:  IPAM, VPN, firewalls, SSH, DNS & L4 Load Balancing
 * Other services: auto-scaling, CDNs, 3rd-party NFV
 * Fast VM provisioning with affinity and anti-affinity
 * Scale (10,000+ servers at times)
 * Flexible image management
 * Support for GPUs

**Note:**

 * VSI Fast Provisioning is being handled separately, not as part of VPC.  
 * Virtual Private Cloud does not provide E2E encryption, but supports it.
