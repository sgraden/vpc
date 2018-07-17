---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Summary of Supported APIs for IBM Cloud VPC Beta

Here is a comprehensive list of REST APIs that are supported in the VPC Beta release.

| Component | Functions | Comments |
|-----------|------------|-----------|
| **Network:** |   |   |
| VPCs | Create, Get, Get All, Update, Delete |   |
| External_addresses | Create, Get, Update, Delete | AKA Floating IPs aka Elastic IPs. These are 1-to-1 NATed to specific private addresses |
| Public_Gateways | Create, Get, Get All, Update, Delete | AKA NAT Gateway. Provides SNAT for many-to-1 internal private instances to one external public address |
| Subnets | Create, Get, Get All, Update, Delete |   |
| Floating IP | Associate, Get, Get All, Update, Release |  |
| Security Groups | Create, Get, Get All, Set, Remove | |
| Security Group Rules | Create, Get, Get All, Set, Remove | |
| ACLs |   |   |
| VPN Gateways | Create, Get, Get All, Update, Delete | |
| VPN Connections | Create, Get, Get All, Update, Delete | |
| IKE Policies | Create, Get, Get All, Update, Delete | |
| IPsec Policies | Create, Get, Get All, Update, Delete | |
| **Compute:** |   |   |
| Profiles  | Get, Get All|   |
| Images | Get, Get All | Initially only Ubuntu 16.04 and CentOS 7.x are supported |
| Keys | Create, Get, Get All, Update, Delete |   |
| Servers | Create, Get, Get All, Update, Delete |   |
| Network_Interfaces | Get, Get All | Only 1 interface per instance. Allows "one arm" firewall or router scenarios |
| **Geo:** |   |   |
| Regions | Get, Get All | Initially one region |
| Zones | Get, Get All | Only one zone initially |  
