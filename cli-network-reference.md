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

# VPC Beta Network CLI reference

This document provides a reference of the CLI commands available for the Network functionality of the IBM Cloud Virtual Private Cloud Beta release. Similar commands to execute these functions also are available as [API commands](apis.html).

## Floating IPs

### `ibmcloud is floating-ips`

List all floating IPs

#### Syntax

`ibmcloud is floating-ips [--zone ZONE] [--json]`

##### Options

- `--zone`: List floating IPs which belongs to given zone
- `--json`: Format output in JSON

---

### `ibmcloud is floating-ip`

View details of a floating IP

#### Syntax

`ibmcloud is floating-ip FLOATING_IP_ID [--json]`

##### Options

- `FLOATING_IP_ID `: ID of the floating IP
- `--json`: Format output in JSON

---

### `ibmcloud is floating-ip-reserve`

Reserve a floating IP in current resource group

#### Syntax

`ibmcloud is floating-ip-reserve FLOATING_IP_NAME (--zone ZONE | --nic-id NIC_ID) [--json]`

##### Options

- `FLOATING_IP_NAME`: Name of the floating IP
- `--zone `: Name of the target zone. This is exclusive with `--nic`
- `--nic`: ID of the target network interface. This is exclusive with `--zone` 
- `--json`: Format output in JSON

---

### `ibmcloud is floating-ip-release`

Release a floating IP

#### Syntax

`ibmcloud is floating-ip-release FLOATING_IP_ID [-f, --force]`

##### Options

- `FLOATING_IP_ID `: ID of the floating IP
- `	-f, --force`: Release without confirmation

---

### `ibmcloud is floating-ip-update`

Update a floating IP

#### Syntax

`ibmcloud is floating-ip-update  FLOATING_IP_ID [--name NEW_NAME] [--nic-id NIC_ID]`

##### Options

- `FLOATING_IP_ID `: ID of the floating IP
 - `--name`: New name of the floating IP
- `--nic`: ID of the new network interface to associate with

---


## Public gateway 

### `ibmcloud is public-gateways`

List all public gateways 

#### Syntax

`ibmcloud is public-gateways [--vpc VPC_ID] [--zone ZONE]  [--json]`

##### Options

- `--vpc`: List public gateways which contain the specified VPC.  
- `--zone`: List public gateways which belong to given zone
- `--json`: Format output in JSON

---

### `ibmcloud is public-gateway`

View details of a public gateway

#### Syntax

`ibmcloud is public-gateway GATEWAY_ID [--json | --id]`

##### Options

- `GATEWAY_ID `: ID of the public gateway
- `--json`: Format output in JSON

---

### `ibmcloud is public-gateway-create`

Create a new public gateway in current resource group

#### Syntax

`ibmcloud is public-gateway-create GATEWAY_NAME VPC_ID ZONE [--floating-ip IP_ID]`

##### Options

- `GATEWAY_NAME `: Name of the public-gateway
- `VPC_ID`: ID of the VPC
- `ZONE`: Name of the zone
- `--floating-ip`: ID of the floating IP bound to the public gateway


---

### `ibmcloud is public-gateway-update`

Update a public gateway

#### Syntax

`ibmcloud is public-gateway-update GATEWAY_ID --name NEW_NAME`

##### Options

- `GATEWAY_ID `: ID of the public gateway
- `--name`: New name of the public gateway

---

### `ibmcloud is public-gateway-delete`

Delete a public gateway

#### Syntax

`ibmcloud is image-delete GATEWAY_ID [-f, --force]`

##### Options

- `GATEWAY_ID `: ID of the public gateway
- `-f, --force`: Delete without confirmation

## Network ACL 

### `ibmcloud is network-acls`

List all network ACLs 

#### Syntax

`ibmcloud is network-acls [--json]`

##### Options

- `--json`: Format output in JSON

---

### `ibmcloud is network-acl`

View details of a network ACL

#### Syntax

`ibmcloud is network-acl ACL_ID [--json]`

##### Options

- `ACL_ID`: ID of the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is network-acl-create`

Create a network ACL in current resource group

#### Syntax

`ibmcloud is network-acl-create ACL_NAME [--source-acl SOURCE_ACL_ID]`

##### Options

- `ACL_NAME`: Name of the network acl
- `--source-acl`: the ID the source network ACL to copy from

---

### `ibmcloud is network-acl-update`

Update a network ACL

#### Syntax

`ibmcloud is network-acl-update ACL_ID --name NEW_NAME`

##### Options

- `ACL_ID`: ID of the network ACL
- `--name`: New name of the network ACL

---

### `ibmcloud is network-acl-delete`

Delete a network ACL

#### Syntax

`ibmcloud is network-acl-delete ACL_ID [-f, --force]`

##### Options

- `ACL_ID`: ID of the network ACL
- `-f, --force`: Delete without confirmation


### `ibmcloud is network-acl-rules`

List all the rules of a network ACL

#### Syntax

`ibmcloud is network-acl-rules ACL_ID [--direction DIRECTION] [--json]`

##### Options

- `ACL_ID `: ID of the security group
- `--direction`: Filter with direction.`ingress` and `egress`
- `--json`: show output in JSON format

---


### `ibmcloud is network-acl-rule`

Retrieve the details of a network ACL rule

#### Syntax

`ibmcloud is network-acl-rule ACL_ID RULE_ID [--json]`

##### Options

- `ACL_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---

### `ibmcloud is network-acl-rule-add`

Add a rule to a network ACL

#### Syntax

`ibmcloud is security-group-rule-add RULE_NAME ACL_ID ACTION DIRECTION SOURCE DEST PROTOCOL [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--before-rule RULE_ID]`

##### Options

- `RULE_NAME`: Name of the rule
- `ACL_ID`: ID of the security group
- `ACTION`: `allow` or `deny`
- `DIRECTION`: Direction of traffic to enforce. Valid values are `ingress` and `egress`
- `SOURCE`: source IP address or CIDR block
- `DEST`: destination IP address or CIDR block
- `PROCOTOL`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port nubmer. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--before-rule`: ID of the rule id that this rule is inserted before. 

---


### `ibmcloud is network-acl-rule-update`

Update a rule of network ACL

#### Syntax

`ibmcloud is network-acl-rule-update  ACL_ID RULE_ID [--action ACTION] [--direction DIRECTION] [--source SOURCE] [--dest DEST] [--protocol PROTOCOL] [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--before-rule RULE_ID]`


##### Options

- `ACL_ID`: ID of the security group
- `RULE_ID`: ID of the rule
- `--action`: `allow` or `deny`
- `--direction`: Direction of traffic to enforce. Valid values are `ingress` and `egress`
- `--source`: source IP address or CIDR block
- `--dest`: destination IP address or CIDR block
- `--protocol`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port nubmer. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--before-rule`: ID of the rule id that this rule is inserted before. 

---

### `ibmcloud is network-acl-rule-delete`

Delete a rule from network ACL

#### Syntax

`ibmcloud is network-acl-rule ACL_ID RULE_ID [-f, --force]`

##### Options

- `ACL_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---


## Subnets

### `ibmcloud is subnets`

List all subnets 

#### Syntax

`ibmcloud is subnets [--zone ZONE] [--vpc VPC_ID] [--network-acl NETWORK_ACL_ID]  [--json]`

##### Options

- - `--zone`: List public gateways which belongs to given zone
- `--vpc: List public gateways which contains the specified VPC. 
- `--network-acl`: Filter with the network ACL with specified ID, this is exclusive with `--network-acl-name`
- `--json`: Format output in JSON


---

### `ibmcloud is subnet`

View details of a subnet

#### Syntax

`ibmcloud is subnet SUBNET_ID [--json | --id]`

##### Options

- `SUBNET_ID `: ID of the subnet
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-create`

Create a subnet in current resource group

#### Syntax

`ibmcloud is subnet-create SUBNET_NAME VPC_ID ZONE (--ipv4_cidr_block CIDR_BLOCK | --ipv4_address_count ADDR_COUNT) [--generation GEN] [--ip-version IP_VERSION] [--network-acl NETWORK_ACL_ID] [--public-gateway PUBLIC_GATEWAY_ID] [--json]`

##### Options

- `SUBNET_NAME `: Name of the subnet
- `VPC_ID`: ID of the VPC
- `ZONE`: name of the zone
- `--ipv4_cidr_block`: the IPv4 range of the subnet, this is exclusive with  `--ipv4_address_count`
- `--ipv4_address_count`: the total number of IPv4 addresses required. This is exclusive with `--ipv4_cidr_block`
- `--generation`:  generation of the subnet. Valid values are `gt` and `gc`. Defauts to `gt`
- `--ip-version`: versio of the IP address. Valid values are `ipv4`, `ipv6` and 'both'. Default to `ipv4`
- `--network-acl`: the ID of the network ACL for the subnet
- `--public-gateway`: the ID of the public-gateway for the subnet
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-update`

Update a subnet

#### Syntax

`ibmcloud is subnet-update SUBNET_ID --name NEW_NAME `

##### Options

- `SUBNET_ID `: ID of the subnet 
- `--name`: New name of the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-delete`

Delete a subnet

#### Syntax

`ibmcloud is subnet-delete SUBNET_ID [-f, --force]`

##### Options

- `SUBNET_ID `: ID of the subnet 
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is subnet-pubic-gateway-attach`

Attach a pubic gateway to a subnet

#### Syntax

`ibmcloud is subnet-pubic-gateway-attach SUBNET_ID GATEWAY_ID [--json]`

##### Options

- `SUBNET_ID `: ID of the subnet
- `GATEWAY_ID`: ID of the publie public gateway
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-pubic-gateway-detach`

Detach the public gateway from a subnet

#### Syntax

`ibmcloud is subnet-pubic-gateway-detach SUBNET_ID [--json]`

##### Options

- `SUBNET_ID `: ID of the subnet
- `--json`: Format output in JSON
---

### `ibmcloud is subnet-network-acl-attach`

Attach the network acl to a subnet

#### Syntax

`ibmcloud is subnet-network-acl-attach SUBNET_ID ACL_ID [--json]`

##### Options

- `SUBNET_ID `: ID of the subnet
- `ACL_ID`: ID fo the network ACL
- `--json`: Format output in JSON


---
### `ibmcloud is subnet-network-acl-detach`

Detach the network acl from a subnet

#### Syntax

`ibmcloud is subnet-network-acl-detach (SUBNET_NAME | SUBNET_ID) [--json]`

##### Options

- `SUBNET_NAME`: Name of the subnet
- `SUBNET_ID `: ID of the subnet
- `--json`: Format output in JSON
---

## Security Group 

### `ibmcloud is security-groups`

List all security groups 

#### Syntax

`ibmcloud is security-groups [--vpc VPC_ID] [--json]`

##### Options

- `--vpc`: Filter with specified VPC_ID.  
- `--json`: Format output in JSON

---

### `ibmcloud is security-group`

View details of a security group

#### Syntax

`ibmcloud is security-group GROUP_ID [--json]`

##### Options

- `GROUP_ID `: ID of the security group
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-create`

Create a security group in current resource group

#### Syntax

`ibmcloud is security-group-create GROUP_NAME VPC_ID [--json]`

##### Options

- `GROUP_NAME `: Name of the subnet
- `VPC_ID`: ID of the VPC
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-update`

Update a subnet

#### Syntax

`ibmcloud is security-group-update GROUP_ID --name NEW_NAME [--json]`

##### Options

- `GROUP_ID `: ID of the security group
- `--name`: New name of the network ACL
- `--json`: Format output in JSON
---

### `ibmcloud is security-group-delete`

Delete a security group

#### Syntax

`ibmcloud is security-group-delete GROUP_ID [-f, --force]`

##### Options

- `GROUP_ID `: ID of the security group
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is security-group-network-interface-add`

Add a network interface to a security group

#### Syntax

`ibmcloud is security-group-network-interface-add GROUP_ID NIC_ID [--json]`

##### Options

- `GROUP_ID `: ID of the security group
- `NIC_ID `: ID of the network interface
- `--json`: Format output in JSON
---

### `ibmcloud is security-group-network-interface-remove`

Remove a network interface from a security group

#### Syntax

`ibmcloud is security-group-network-interface-remove GROUP_ID NIC_ID [-f, --force]`

##### Options

- `GROUP_ID `: ID of the security group
- `NIC_ID `: ID of the network interface
- `-f, --force`: Delete without confirmation

---


### `ibmcloud is security-group-rules`

List all the rules of a security group

#### Syntax

`ibmcloud is security-group-rules GROUP_ID [--json]`

##### Options

- `GROUP_ID `: ID of the security group
- `--json`: show output in JSON format

---


### `ibmcloud is security-group-rule`

Retrieve the details of a security group rule

#### Syntax

`ibmcloud is security-group-rule GROUP_ID RULE_ID [--json]`

##### Options

- `GROUP_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---

### `ibmcloud is security-group-rule-add`

Add a rule to a security group

#### Syntax

`ibmcloud is security-group-rule-add GROUP_ID DIRECTION IP_VERSION PROTOCOL (REMOTE_ADDRESS | REMOTE_CIDR_BLOCK | PEER_SECURITY_GROUP_ID) [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--json]`

##### Options

- `GROUP_ID `: ID of the security group
- `DIRECTION`: Direction of traffic to enforce. Valid values are `ingress` or `egress`
- `IP_VERSION `: Version of the IP address. Valid values are `ipv4` and `ipv6` 
- `PROCOTOL`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `REMOTE_ADDRESS`: IP address from/to which this rule should allow traffic. This is exclusive with `REMOTE_CIDR_BLOCK` and `PEER_SECURITY_GROUP_ID`
- `REMOTE_CIDR_BLOCK`: Range of IPv4 or IPv6 addresses in CIDR format from/to which this rule should allow traffic.  This is exclusive with `REMOTE_ADDRESS` and `PEER_SECURITY_GROUP_ID`
- `PEER_SECURITY_GROUP`: ID of the security group with remote addresses. This is exclusive with `REMOTE_ADDRESS` and `REMOTE_CIDR_BLOCK`
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port nubmer. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--json`: show output in JSON format
---


### `ibmcloud is security-group-rule-update`

Update a rule of a security group

#### Syntax

`ibmcloud is security-group-rule-update GROUP_ID RULE_ID [--direction DIRECTION] [--ip-version IP_VERSION] [--protocol PROTOCOL] [--remote-address REMOTE_ADDRESS  | --remote-cidr-block CIDR_BLOCK ] [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--json]`

##### Options

- `GROUP_ID `: ID of the security group
- `RULE_ID`: ID of the rule
- `--direction`: Direction of traffic to enforce. Valid values are `ingress` or `egress`
- `--ip-version IP_VERSION`: Version of the IP address. Valid values are `ipv4` and `ipv6` 
- `--protocol`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `--remote-address`: IP address from/to which this rule should allow traffic. This is exclusive with `--remote-cidr-block`
- `--remote-cidr-block`: Range of IPv4 or IPv6 addresses in CIDR format from/to which this rule should allow traffic.  This is exclusive with `--remote-address`
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port nubmer. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--json`: show output in JSON format
---

### `ibmcloud is security-group-rule-delete`

Delete a rule fom a security group

#### Syntax

`ibmcloud is security-group-rule-delete GROUP_ID RULE_ID [--json]`

##### Options

- `GROUP_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---

## VPC 

### `ibmcloud is vpcs`

List all vpcs

#### Syntax

`ibmcloud is vpcs [--json]`

##### Options

- `--json`: Format output in JSON

---

### `ibmcloud is vpc`

View details of a VPC

#### Syntax

`ibmcloud is vpc VPC_ID [--json]`

##### Options

- `VPC_ID `: ID of the VPC 
- `--json`: Format output in JSON

---

### `ibmcloud is vpc-create`

Create a VPC in current resource group

#### Syntax

ibmcloud is vpc-create VPC_NAME [--default] [--default-network-acl ACL_ID] [--json]`

##### Options

- `VPC_NAME `: Name of the VPC
- `--default`: set the VPC default of the account
- `--default-network-acl`: the ID of the default network ACL. This is exclusive with `--default-network-acl-name`
- `--json`: Format output in JSON

---

### `ibmcloud is vpc-update`

Update a vpc

#### Syntax

`ibmcloud is vpc-update VPC_ID --name NEW_NAME [--json]`

##### Options

- `VPC_ID `: ID of the vpc
- `--name`: New name of the vpc
- `--json`: Format output in JSON
---

### `ibmcloud is vpc-delete`

Delete a vpc

#### Syntax

`ibmcloud is subnet-delete VPC_ID [-f, --force]`

##### Options

- `VPC_ID `: ID of the vpc
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is vpc-default-network-acl-set`

Set the default network ACL for a VPC 

#### Syntax

`ibmcloud is vpc-default-network-acl-set VPC_ID NETWORK_ACL_ID [--json]`

##### Options

- `VPC_ID `: ID of the vpc
- `NETWORK_ACL_ID`: ID of the network ACL
- `--json`: Format output in JSON

---


