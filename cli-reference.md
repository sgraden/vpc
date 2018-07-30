---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# IBM Cloud VPC Beta CLI Reference

This document provides a reference of the command line interface (CLI) commands available for the functionality of the IBM Cloud Virtual Private Cloud Beta release. Similar commands to execute these functions also are available as [API commands](apis.html).

This document is organized into three sections:
* [Network CLI commands](#network)
* [Compute CLI commands](#compute)
* [Regions and Zones CLI commands](#geography)

You can scroll through the Table of Contents menu at the right side of your screen to view the functional groupings of commands, such as those related to subnets, Floating IPs, and so forth.

<p style="font-size:24px">Network CLI Commands</p>
{: #network}

This section provides a reference for the command line interface (CLI) commands available for the network functionality.

## Floating IPs

### `ibmcloud is floating-ips`

List all floating IPs

**Syntax**

`ibmcloud is floating-ips [--zone ZONE] [--json]`

**Options**

- `--zone`: List floating IPs which belongs to given zone
- `--json`: Format output in JSON

---

### `ibmcloud is floating-ip`

View details of a floating IP

**Syntax**

`ibmcloud is floating-ip FLOATING_IP_ID [--json]`

**Options**

- `FLOATING_IP_ID `: ID of the floating IP
- `--json`: Format output in JSON

---

### `ibmcloud is floating-ip-reserve`

Reserve a floating IP in current resource group

**Syntax**

`ibmcloud is floating-ip-reserve FLOATING_IP_NAME (--zone ZONE | --nic-id NIC_ID) [--json]`

**Options**

- `FLOATING_IP_NAME`: Name of the floating IP
- `--zone `: Name of the target zone. This is exclusive with `--nic`
- `--nic`: ID of the target network interface. This is exclusive with `--zone` 
- `--json`: Format output in JSON

---

### `ibmcloud is floating-ip-release`

Release a floating IP

**Syntax**

`ibmcloud is floating-ip-release FLOATING_IP_ID [-f, --force]`

**Options**

- `FLOATING_IP_ID `: ID of the floating IP
- `	-f, --force`: Release without confirmation

---

### `ibmcloud is floating-ip-update`

Update a floating IP

**Syntax**

`ibmcloud is floating-ip-update  FLOATING_IP_ID [--name NEW_NAME] [--nic-id NIC_ID]`

**Options**

- `FLOATING_IP_ID `: ID of the floating IP
- `--name`: New name of the floating IP
- `--nic`: ID of the new network interface to associate with

---


## Public gateway 

### `ibmcloud is public-gateways`

List all public gateways 

**Syntax**

`ibmcloud is public-gateways [--vpc VPC_ID] [--zone ZONE]  [--json]`

**Options**

- `--vpc`: List public gateways which contain the specified VPC.  
- `--zone`: List public gateways which belong to given zone
- `--json`: Format output in JSON

---

### `ibmcloud is public-gateway`

View details of a public gateway

**Syntax**

`ibmcloud is public-gateway GATEWAY_ID [--json | --id]`

**Options**

- `GATEWAY_ID `: ID of the public gateway
- `--json`: Format output in JSON

---

### `ibmcloud is public-gateway-create`

Create a new public gateway in current resource group

**Syntax**

`ibmcloud is public-gateway-create GATEWAY_NAME VPC_ID ZONE [--floating-ip IP_ID]`

**Options**

- `GATEWAY_NAME `: Name of the public-gateway
- `VPC_ID`: ID of the VPC
- `ZONE`: Name of the zone
- `--floating-ip`: ID of the floating IP bound to the public gateway

---

### `ibmcloud is public-gateway-update`

Update a public gateway

**Syntax**

`ibmcloud is public-gateway-update GATEWAY_ID --name NEW_NAME`

**Options**

- `GATEWAY_ID `: ID of the public gateway
- `--name`: New name of the public gateway

---

### `ibmcloud is public-gateway-delete`

Delete a public gateway

**Syntax**

`ibmcloud is image-delete GATEWAY_ID [-f, --force]`

**Options**

- `GATEWAY_ID `: ID of the public gateway
- `-f, --force`: Delete without confirmation

## Network ACL 

### `ibmcloud is network-acls`

List all network ACLs 

**Syntax**

`ibmcloud is network-acls [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is network-acl`

View details of a network ACL

**Syntax**

`ibmcloud is network-acl ACL_ID [--json]`

**Options**

- `ACL_ID`: ID of the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is network-acl-create`

Create a network ACL in current resource group

**Syntax**

`ibmcloud is network-acl-create ACL_NAME [--source-acl SOURCE_ACL_ID]`

**Options**

- `ACL_NAME`: Name of the network acl
- `--source-acl`: the ID the source network ACL to copy from

---

### `ibmcloud is network-acl-update`

Update a network ACL

**Syntax**

`ibmcloud is network-acl-update ACL_ID --name NEW_NAME`

**Options**

- `ACL_ID`: ID of the network ACL
- `--name`: New name of the network ACL

---

### `ibmcloud is network-acl-delete`

Delete a network ACL

**Syntax**

`ibmcloud is network-acl-delete ACL_ID [-f, --force]`

**Options**

- `ACL_ID`: ID of the network ACL
- `-f, --force`: Delete without confirmation


### `ibmcloud is network-acl-rules`

List all the rules of a network ACL

**Syntax**

`ibmcloud is network-acl-rules ACL_ID [--direction DIRECTION] [--json]`

**Options**

- `ACL_ID `: ID of the security group
- `--direction`: Filter with direction.`ingress` and `egress`
- `--json`: show output in JSON format

---

### `ibmcloud is network-acl-rule`

Retrieve the details of a network ACL rule

**Syntax**

`ibmcloud is network-acl-rule ACL_ID RULE_ID [--json]`

**Options**

- `ACL_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---

### `ibmcloud is network-acl-rule-add`

Add a rule to a network ACL

**Syntax**

`ibmcloud is network-acl-rule-add RULE_NAME ACL_ID ACTION DIRECTION SOURCE DEST PROTOCOL [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--before-rule RULE_ID]`

**Options**

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

**Syntax**

`ibmcloud is network-acl-rule-update  ACL_ID RULE_ID [--action ACTION] [--direction DIRECTION] [--source SOURCE] [--dest DEST] [--protocol PROTOCOL] [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--before-rule RULE_ID]`

**Options**

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
- `--port-min`: Minimum port number. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--before-rule`: ID of the rule id that this rule is inserted before. 

---

### `ibmcloud is network-acl-rule-delete`

Delete a rule from network ACL

**Syntax**

`ibmcloud is network-acl-rule ACL_ID RULE_ID [-f, --force]`

**Options**

- `ACL_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---

## Subnets

### `ibmcloud is subnets`

List all subnets 

**Syntax**

`ibmcloud is subnets [--zone ZONE] [--vpc VPC_ID] [--network-acl NETWORK_ACL_ID]  [--json]`

**Options**

- `--zone`: List public gateways which belongs to given zone
- `--vpc: List public gateways which contains the specified VPC. 
- `--network-acl`: Filter with the network ACL with specified ID, this is exclusive with `--network-acl-name`
- `--json`: Format output in JSON

---

### `ibmcloud is subnet`

View details of a subnet

**Syntax**

`ibmcloud is subnet SUBNET_ID [--json | --id]`

**Options**

- `SUBNET_ID `: ID of the subnet
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-create`

Create a subnet in current resource group

**Syntax**

`ibmcloud is subnet-create SUBNET_NAME VPC_ID ZONE (--ipv4_cidr_block CIDR_BLOCK | --ipv4_address_count ADDR_COUNT) [--generation GEN] [--ip-version IP_VERSION] [--network-acl NETWORK_ACL_ID] [--public-gateway PUBLIC_GATEWAY_ID] [--json]`

**Options**

- `SUBNET_NAME `: Name of the subnet
- `VPC_ID`: ID of the VPC
- `ZONE`: name of the zone
- `--ipv4_cidr_block`: the IPv4 range of the subnet, this is exclusive with  `--ipv4_address_count`
- `--ipv4_address_count`: the total number of IPv4 addresses required. This is exclusive with `--ipv4_cidr_block`
- `--generation`:  generation of the subnet. Valid values are `gt` and `gc`. Defauts to `gt`
- `--ip-version`: version of the IP address. Valid values are `ipv4`, `ipv6` and 'both'. Default to `ipv4`
- `--network-acl`: the ID of the network ACL for the subnet
- `--public-gateway`: the ID of the public-gateway for the subnet
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-update`

Update a subnet

**Syntax**

`ibmcloud is subnet-update SUBNET_ID --name NEW_NAME `

**Options**

- `SUBNET_ID `: ID of the subnet 
- `--name`: New name of the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-delete`

Delete a subnet

**Syntax**

`ibmcloud is subnet-delete SUBNET_ID [-f, --force]`

**Options**

- `SUBNET_ID `: ID of the subnet 
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is subnet-pubic-gateway-attach`

Attach a pubic gateway to a subnet

**Syntax**

`ibmcloud is subnet-pubic-gateway-attach SUBNET_ID GATEWAY_ID [--json]`

**Options**

- `SUBNET_ID `: ID of the subnet
- `GATEWAY_ID`: ID of the publie public gateway
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-pubic-gateway-detach`

Detach the public gateway from a subnet

**Syntax**

`ibmcloud is subnet-pubic-gateway-detach SUBNET_ID [--json]`

**Options**

- `SUBNET_ID `: ID of the subnet
- `--json`: Format output in JSON
---

### `ibmcloud is subnet-network-acl-attach`

Attach the network acl to a subnet

**Syntax**

`ibmcloud is subnet-network-acl-attach SUBNET_ID ACL_ID [--json]`

**Options**

- `SUBNET_ID `: ID of the subnet
- `ACL_ID`: ID fo the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is subnet-network-acl-detach`

Detach the network acl from a subnet

**Syntax**

`ibmcloud is subnet-network-acl-detach (SUBNET_NAME | SUBNET_ID) [--json]`

**Options**

- `SUBNET_NAME`: Name of the subnet
- `SUBNET_ID `: ID of the subnet
- `--json`: Format output in JSON
---

## Security Group 

### `ibmcloud is security-groups`

List all security groups 

**Syntax**

`ibmcloud is security-groups [--vpc VPC_ID] [--json]`

**Options**

- `--vpc`: Filter with specified VPC_ID.  
- `--json`: Format output in JSON

---

### `ibmcloud is security-group`

View details of a security group

**Syntax**

`ibmcloud is security-group GROUP_ID [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-create`

Create a security group in current resource group

**Syntax**

`ibmcloud is security-group-create GROUP_NAME VPC_ID [--json]`

**Options**

- `GROUP_NAME `: Name of the subnet
- `VPC_ID`: ID of the VPC
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-update`

Update a subnet

**Syntax**

`ibmcloud is security-group-update GROUP_ID --name NEW_NAME [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `--name`: New name of the network ACL
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-delete`

Delete a security group

**Syntax**

`ibmcloud is security-group-delete GROUP_ID [-f, --force]`

**Options**

- `GROUP_ID `: ID of the security group
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is security-group-network-interface-add`

Add a network interface to a security group

**Syntax**

`ibmcloud is security-group-network-interface-add GROUP_ID NIC_ID [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `NIC_ID `: ID of the network interface
- `--json`: Format output in JSON

---

### `ibmcloud is security-group-network-interface-remove`

Remove a network interface from a security group

**Syntax**

`ibmcloud is security-group-network-interface-remove GROUP_ID NIC_ID [-f, --force]`

**Options**

- `GROUP_ID `: ID of the security group
- `NIC_ID `: ID of the network interface
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is security-group-rules`

List all the rules of a security group

**Syntax**

`ibmcloud is security-group-rules GROUP_ID [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `--json`: show output in JSON format

---

### `ibmcloud is security-group-rule`

Retrieve the details of a security group rule

**Syntax**

`ibmcloud is security-group-rule GROUP_ID RULE_ID [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---

### `ibmcloud is security-group-rule-add`

Add a rule to a security group. The IP version defaults to IPv4.

**Syntax**

`ibmcloud is security-group-rule-add GROUP_ID DIRECTION PROTOCOL (REMOTE_ADDRESS | REMOTE_CIDR_BLOCK | PEER_SECURITY_GROUP_ID) [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `DIRECTION`: Direction of traffic to enforce. Valid values are `ingress` or `egress`
- `PROCOTOL`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `REMOTE_ADDRESS`: IP address from/to which this rule should allow traffic. This is exclusive with `REMOTE_CIDR_BLOCK` and `PEER_SECURITY_GROUP_ID`
- `REMOTE_CIDR_BLOCK`: Range of IPv4 addresses in CIDR format from/to which this rule should allow traffic.  This is exclusive with `REMOTE_ADDRESS` and `PEER_SECURITY_GROUP_ID`
- `PEER_SECURITY_GROUP`: ID of the security group with remote addresses. This is exclusive with `REMOTE_ADDRESS` and `REMOTE_CIDR_BLOCK`
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port nubmer. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--json`: show output in JSON format
---

### `ibmcloud is security-group-rule-update`

Update a rule of a security group. The IP version defaults to IPv4.

**Syntax**

`ibmcloud is security-group-rule-update GROUP_ID RULE_ID [--direction DIRECTION] [--protocol PROTOCOL] [--remote-address REMOTE_ADDRESS  | --remote-cidr-block CIDR_BLOCK ] [--icmp-code ICMP_CODE] [--icmp-type ICMP_TYPE] [--port-max PORT_MAX] [--port-min PORT_MIN] [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `RULE_ID`: ID of the rule
- `--direction`: Direction of traffic to enforce. Valid values are `ingress` or `egress`
- `--protocol`: Protocol to enforce. Valid values are `all`, `icmp`, `tcp` and `udp`
- `--remote-address`: IP address from/to which this rule should allow traffic. This is exclusive with `--remote-cidr-block`
- `--remote-cidr-block`: Range of IPv4 addresses in CIDR format from/to which this rule should allow traffic.  This is exclusive with `--remote-address`
- `--icmp-code`: ICMP traffic code to allow. Valid values from 0 to 255. This is specified only when protocol is set to `icmp`
- `--icmp-type`: ICMP traffic type to allow. Valid values from 0 to 254. This is specified only when protocol is set to `icmp`
- `--port-max`: Maximum port number. Valid values are from 1 to 65535.This is specified only when protocol is set to `tcp` or `udp`
- `--port-min`: Minimum port nubmer. Valid values are from 1 to 65535. This is specified only when protocol is set to `tcp` or `udp`
- `--json`: show output in JSON format
---

### `ibmcloud is security-group-rule-delete`

Delete a rule fom a security group

**Syntax**

`ibmcloud is security-group-rule-delete GROUP_ID RULE_ID [--json]`

**Options**

- `GROUP_ID `: ID of the security group
- `RULE_ID `: ID of the rule
- `--json`: show output in JSON format

---

## VPC 

### `ibmcloud is vpcs`

List all vpcs

**Syntax**

`ibmcloud is vpcs [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is vpc`

View details of a VPC

**Syntax**

`ibmcloud is vpc VPC_ID [--json]`

**Options**

- `VPC_ID `: ID of the VPC 
- `--json`: Format output in JSON

---

### `ibmcloud is vpc-create`

Create a VPC in current resource group

**Syntax**

ibmcloud is vpc-create VPC_NAME [--default] [--default-network-acl ACL_ID] [--json]`

**Options**

- `VPC_NAME `: Name of the VPC
- `--default`: set the VPC default of the account
- `--default-network-acl`: the ID of the default network ACL. This is exclusive with `--default-network-acl-name`
- `--json`: Format output in JSON

---

### `ibmcloud is vpc-update`

Update a vpc

**Syntax**

`ibmcloud is vpc-update VPC_ID --name NEW_NAME [--json]`

**Options**

- `VPC_ID `: ID of the vpc
- `--name`: New name of the vpc
- `--json`: Format output in JSON
---

### `ibmcloud is vpc-delete`

Delete a vpc

**Syntax**

`ibmcloud is subnet-delete VPC_ID [-f, --force]`

**Options**

- `VPC_ID `: ID of the vpc
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is vpc-default-network-acl-set`

Set the default network ACL for a VPC 

**Syntax**

`ibmcloud is vpc-default-network-acl-set VPC_ID NETWORK_ACL_ID [--json]`

**Options**

- `VPC_ID `: ID of the vpc
- `NETWORK_ACL_ID`: ID of the network ACL
- `--json`: Format output in JSON

---

<p style="font-size:24px">Compute CLI commands</p>
{: #compute}


This section contains a reference for the CLI commands related to Compute functionality in the IBM Cloud VPC Beta release. Similar commands to execute these functions also are available as [API commands](apis.html).


## Instance Profile CLI commands

### `ibmcloud is instance-profiles`

List all instance profiles available in the region. 

**Syntax**

`ibmcloud is instance-profiles [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is instance-profile`

View details of an instance profile

**Syntax**

`ibmcloud is instance-profile PROFILE_NAME [--json]`

**Options**

- `PROFILE_NAME `: Name of the profile
- `--json`: Format output in JSON

---

## Image Commands

### `ibmcloud is images`

List all images available in the region

**Syntax**

`ibmcloud is images [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is image`

Show details of an image

**Syntax**

`ibmcloud is image IMAGE_ID [--json]`

**Options**

- `IMAGE_ID `: ID of the image
- `--json`: Format output in JSON

---

## Key Commands

### `ibmcloud is keys`

List all keys

**Syntax**

`ibmcloud is keys [--json]`

**Options**

- `--json`: Format output in JSON

---

### `ibmcloud is key`

Show details of a key

**Syntax**

`ibmcloud is key KEY_ID [--json ]`

**Options**

- `KEY_ID`: ID of the key
- `--json`: Format output in JSON

---

### `ibmcloud is key-create`

Imports an RSA public key

**Syntax**

`ibmcloud is key-create KEY_NAME  (KEY | @KEY_FILE) `

**Options**

- `KEY_NAME`: Name of the key
- `KEY`: The public ssh key. If starts with "@", the rest should be a file name.

---

### `ibmcloud is key-update`

Update the name of a key

**Syntax**

`ibmcloud is key-update KEY_ID --name NEW_NAME`

**Options**

- `KEY_ID`: ID of the key
- `--name NEW_NAME`: New name for the key

---

### `ibmcloud is key-delete`

Delete a key

**Syntax**

`ibmcloud is key-delete  KEY_ID [-f, --force]`

**Options**

- `KEY_ID`: ID of the key
- `-f, --force`: Delete without confirmation

---

## Instance Commands

### `ibmcloud is instances`

List all server instances

**Syntax**

`ibmcloud is instances [--zone ZONE] [--subnet-id SUBNET_ID ] [--vpc-id VPC_ID ] [--json]`

**Options**

- `--zone ZONE`: Zone name to which the server instance belongs.
- `--subnet-id SUBNET_ID`: ID of the subnet to which the server instance belongs. 
- `--vpc-id VPC_ID`: ID of the VPC to which the server instance belongs.
- `--json`: Format output in JSON

---

### `ibmcloud is instance`

Show details of a server instance

**Syntax**

`ibmcloud is instance INSTANCE_ID [--json]`

**Options**

- `INSTANCE_ID`: ID of the server intance
- `--json`: Format output in JSON

---

### `ibmcloud is instance-create`

Create a server instance

**Syntax**

`ibmcloud is instance-create INSTANCE_NAME VPC_ID ZONE PROFILE (--image IMAGE_ID | --boot-volume BOOT_VOLUME_ID) [--generation GENERATION] [--volumes IDS] [--keys IDS] [--user-data DATA]`


**Options**

- `INSTANCE_NAME `: Name of the server instance
- `VPC_ID`: ID of the VPC.
- `ZONE`: Name of the zone
- `PROFILE`: Name of the profile. 
- `--image-id IMAGE_ID`: ID of the image. This is exclusive with `--boot-volume`
- `--boot-volume VOLUME_ID`: ID of the boot volume. This is exclusive with `--image`
- `--volumes VOLUME_ID1,VOLUME_ID2...`: IDs of the volumes to attached to the server instance
- `--keys KEY_ID1,KEY_ID2...`: IDs of the keys
- `--generation GENERATION`: Generation of the server instance. valid values are `gc`, `gt`. Default to `gt`. (`gc` only for beta)
- `--user-data DATA`: User data to transfer to the server instance

---

### `ibmcloud is instance-update`

Update a server instance

**Syntax**

`ibmcloud is instance-update INSTANCE_ID [--name NEW_NAME] [--profile PROFILE]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `--name NEW_NAME`: New name of the server instance
- `--profile PROFILE`: Name of the profile

---

### `ibmcloud is instance-delete`

Delete a server intance 

**Syntax**

`ibmcloud is instance-delete INSTANCE_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is instance-start`

Start a server instance

**Syntax**

`ibmcloud is instance-start INSTANCE_ID `

**Options**

- `INSTANCE_ID `: ID of the server instance

---

### `ibmcloud is instance-stop`

Stop a server instance

**Syntax**

`ibmcloud is instance-stop INSTANCE_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Stop without confirmation

---

### `ibmcloud is instance-reboot`

Reboot a server instance

**Syntax**

`ibmcloud is instance-reboot INSTANCE_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Reboot without confirmation

---

### `ibmcloud is instance-reset`

Reset a server instance

**Syntax**

`ibmcloud is instance-reset INSTANCE_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Reset without confirmation

---

### `ibmcloud is instance-actions`

Retrieves all pending, running, and recent actions on a server instance.

**Syntax**

`ibmcloud is instance-actions INSTANCE_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `--json`: Format output in JSON

---

### `ibmcloud is instance-action`

Show details of an action on a server instance 

**Syntax**

`ibmcloud is instance-action INSTANCE_ID  ACTION_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `ACTION_ID`: ID of the action
- `--json`: Format output in JSON

---

### `ibmcloud is instance-action-cancel`

Cancel a pending server instance action

**Syntax**

`ibmcloud is instance-action-cancel INSTANCE_ID ACTION_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `ACTION_ID`: Action ID
- `-f, --force`: cancel without confirmation

---


### `ibmcloud is instance-network-interfaces`

List all network interfaces of a server instance

**Syntax**

`ibmcloud is instance-network-interfaces INSTANCE_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface`

Show details of a network interface of a server instance

**Syntax**

`ibmcloud is instance-network-interface INSTANCE_ID  NIC_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the network interface
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface-create`

Create a network interface for a server instance

**Syntax**

`ibmcloud is instance-network-interface-create NIC_NAME INSTANCE_ID SUBNET_ID PORT_SPEED [--ipv4 IPV4_ADDRESS] [--ipv6 IPV6_ADDRESS] [--secondary-addresses ADDR1,ADDR2...] [--security-groups SECURITY_GROUP_ID1,SECURITY_GROUP_ID2...]`

**Options**

- `INSTANCE_ID`: ID of the server instance
- `PORT_SPEED`: Speed of the network interface in Mbps
- `--ipv4 IPV4_ADDRESS`: primary IPv4 address
- `--ipv6 IPV6_ADDRESS`: primary IPv6 address (not for beta?)
- `--secondary-addresses ADDR1,ADDR2...`: secondary IP addresses
- `--security-groups SECURITY_GROUP_ID1,SECURITY_GROUP_ID2...`: security group IDs

---

### `ibmcloud is instance-network-interface-update`

Update a network interface of a server instance

**Syntax**

`ibmcloud is instance-network-interface-update INSTANCE_ID NIC_ID [--name NEW_NAME] [--port-speed SPEED]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `--name NEW_NAME`: New name of NIC
- `--port-speed SPEED`: New speed of the NIC

---

### `ibmcloud is instance-network-interface-delete`

Delete a network interface from a server

**Syntax**

`ibmcloud is instance-network-interface-delete INSTANCE_ID NIC_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is instance-network-interface-floating-ips`

List all floating IPs associated with a network interface

**Syntax**

`ibmcloud is instance-network-interface-floating-ips INSTANCE_ID NIC_ID --json`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface-floating-ip`

Show details of a floating IP associated with a network interface

**Syntax**

`ibmcloud is instance-network-interface-floating-ip INSTANCE_ID NIC_ID FLOATING_IP_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `FLOATING_IP_ID`: ID of the floating IP
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface-floating-ip-add`

Associate a floating IP to a network interface

**Syntax**
`ibmcloud is instance-nic-floating-ip-add INSTANCE_ID NIC_ID FLOATING_IP_ID [--json]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `FLOATING_IP_ID`: ID of the floating IP
- `--json`: Format output in JSON
---

### `ibmcloud is instance-network-interface-floating-ip-remove`

Disassociate a floating IP from a server

**Syntax**

`ibmcloud is instance-nic-floating-ip-remove INSTANCE_ID NIC_ID FLOATING_IP_ID [-f, --force]`

**Options**

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `FLOATING_IP_ID`: ID of the floating IP
- `-f, --force`: Remove without confirmation


<p style="font-size:24px">Regions and Zones</p>
{: #geography}

This section gives details about the CLI commands available for working with regions and zones.

## Region

`ibmcloud is region --help`

NAME:
   `region` - View details about a region

USAGE:
   `ibmcloud is region` _`<region name>`_

OPTIONS:
   `--json`  Format output in JSON

## Regions

`ibmcloud is regions --help`

NAME:
   `regions` - List all regions

USAGE:
   `ibmcloud is regions`

OPTIONS:
   `--json`  Format output in JSON

## Zone

`ibmcloud is zone --help`

NAME:
   `zone` - View details about a zone

USAGE:
   `ibmcloud is zone` _`<region name>`_ _`<zone name>`_

OPTIONS:
  ` --json`  Format output in JSON

## Zones

`ibmcloud is zones --help`

NAME:
   `zones` - List all zones in a region

USAGE:
   `ibmcloud is zones` _`<region name>`_

OPTIONS:
   `--json`  Format output in JSON
   
