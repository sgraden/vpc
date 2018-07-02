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

# Use IBM Cloud VPC for cloud-native workloads

IBM Cloud Virtual Private Cloud (VPC) focuses on cloud-native workloads. We aim to create the best cloud for cognitive, AI, and Machine Learning workloads, which are important types of cloud-native workloads. Meanwhile, we continue supporting IBM Cloud Classic for traditional workloads.

The features described are part of the Planned IBM Cloud VPC experience, and many are already available in the Beta release.

## Cloud-Native workloads require:

 * IBM Cloud VPC to create & manage isolated application environments through the API
 * Network topologies with BYoIP
 * Security Groups and Network ACLs for flexible, API-driven topologies
 * Availability Zones with high-speed & low -atency connections across Regions
 * Auto-scale groups
 * Scaling up or down by 1000s of servers per day
 * Scalable & reliable LBaaS with certificate management
 * Scalable & reliable monitoring
 * Illusion of infinite capacity 


## Example: A Cloud Native Workload's IaaS Requirements

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
