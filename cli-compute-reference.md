---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# VPC Beta Compute CLI reference

This document serves as a reference for the CLI commands related to Compute functionality in the IBM Cloud VPC Beta release. Similar commands to execute these functions also are available as [API commands](apis.html).


## Instance Profile CLI commands

### `ibmcloud is instance-profiles`

List all instance profiles available in the region. 

#### Syntax

`ibmcloud is instance-profiles [--json]`

##### Options

- `--json`: Format output in JSON

---

### `ibmcloud is instance-profile`

View details of an instance profile

#### Syntax

`ibmcloud is instance-profile PROFILE_NAME [--json]`

##### Options

- `PROFILE_NAME `: Name of the profile
- `--json`: Format output in JSON


---

## Image Comands

### `ibmcloud is images`

List all images available in the region

#### Syntax

`ibmcloud is images [--json]`

##### Options

---

### `ibmcloud is image`

Show details of an image

#### Syntax

`ibmcloud is image IMAGE_ID [--json]`

##### Options

- `IMAGE_ID `: ID of the image
- `--json`: Format output in JSON
---


## Key Commands

### `ibmcloud is keys`

List all keys

#### Syntax

`ibmcloud is keys [--json]`

##### Options

- `--json`: Format output in JSON

---

### `ibmcloud is key`

Show details of a key

#### Syntax

`ibmcloud is key KEY_ID [--json ]`

##### Options

- `KEY_NAME`: Name of the key
- `KEY_ID`: ID of the key
- `--json`: Format output in JSON
- `--id`: show ID only

---

### `ibmcloud is key-create`

Imports an RSA public key

#### Syntax

`ibmcloud is key-create KEY_NAME  (KEY | @KEY_FILE) `

##### Options

- `KEY_NAME`: Name of the key
- `KEY`: The public ssh key. If starts with "@", the rest should be a file name.

---

### `ibmcloud is key-update`

Update the name of a key

#### Syntax

`ibmcloud is key-update KEY_ID --name NEW_NAME`

##### Options

- `KEY_ID`: ID of the key
- `--name NEW_NAME`: New name for the key


---

### `ibmcloud is key-delete`

Delete a key

#### Syntax

`ibmcloud is key-delete  KEY_ID [-f, --force]`

##### Options

- `KEY_ID`: ID of the key
- `-f, --force`: Delete without confirmation

---


## Instance Commands

### `ibmcloud is instances`

List all server instances

#### Syntax

`ibmcloud is instances [--zone ZONE] [--subnet-id SUBNET_ID ] [--vpc-id VPC_ID ] [--json]`

##### Options

- `--zone ZONE`: Zone name to which the server instance belongs.
- `--subnet-id SUBNET_ID`: ID of the subnet to which the server instance belongs. 
- `--vpc-id VPC_ID`: ID of the VPC to which the server instance belongs.
- `--json`: Format output in JSON


---

### `ibmcloud is instance`

Show details of a server instance

#### Syntax

`ibmcloud is instance INSTANCE_ID [--json]`

##### Options

- `INSTANCE_ID`: ID of the server intance
- `--json`: Format output in JSON

---

### `ibmcloud is instance-create`

Create a server instance

#### Syntax

`ibmcloud is instance-create INSTANCE_NAME VPC_ID ZONE PROFILE (--image IMAGE_ID | --boot-volume BOOT_VOLUME_ID) [--generation GENERATION] [--volumes IDS] [--keys IDS] [--user-data DATA]`


##### Options

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

#### Syntax

`ibmcloud is instance-update INSTANCE_ID [--name NEW_NAME] [--profile PROFILE]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `--name NEW_NAME`: New name of the server instance
- `--profile PROFILE`: Name of the profile

---

### `ibmcloud is instance-delete`

Delete a server intance 

#### Syntax

`ibmcloud is instance-delete INSTANCE_ID [-f, --force]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is instance-start`

Start a server instance

#### Syntax

`ibmcloud is instance-start INSTANCE_ID `

##### Options

- `INSTANCE_ID `: ID of the server instance

---

### `ibmcloud is instance-stop`

Stop a server instance

#### Syntax

`ibmcloud is instance-stop INSTANCE_ID [-f, --force]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Stop without confirmation

---

### `ibmcloud is instance-reboot`

Reboot a server instance

#### Syntax

`ibmcloud is instance-reboot INSTANCE_ID [-f, --force]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Reboot without confirmation

---

### `ibmcloud is instance-reset`

Reset a server instance

#### Syntax

`ibmcloud is instance-reset INSTANCE_ID [-f, --force]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `-f, --force`: Reset without confirmation

---

### `ibmcloud is instance-actions`

Retrieves all pending, running, and recent actions on a server instance.

#### Syntax

`ibmcloud is instance-actions INSTANCE_ID [--json]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `--json`: Format output in JSON

---

### `ibmcloud is instance-action`

Show details of an action on a server instance 

#### Syntax

`ibmcloud is instance-action INSTANCE_ID  ACTION_ID [--json]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `ACTION_ID`: ID of the action
- `--json`: Format output in JSON

---

### `ibmcloud is instance-action-cancel`

Cancel a pending server instance action

#### Syntax

`ibmcloud is instance-action-cancel INSTANCE_ID ACTION_ID [-f, --force]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `ACTION_ID`: Action ID
- `-f, --force`: cancel without confirmation

---


### `ibmcloud is instance-network-interfaces`

List all network interfaces of a server instance

#### Syntax

`ibmcloud is instance-network-interfaces INSTANCE_ID [--json]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface`

Show details of a network interface of a server instance

#### Syntax

`ibmcloud is instance-network-interface INSTANCE_ID  NIC_ID [--json]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the network interface
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface-create`

Create a network interface for a server instance

#### Syntax

`ibmcloud is instance-network-interface-create NIC_NAME INSTANCE_ID SUBNET_ID PORT_SPEED [--ipv4 IPV4_ADDRESS] [--ipv6 IPV6_ADDRESS] [--secondary-addresses ADDR1,ADDR2...] [--security-groups SECURITY_GROUP_ID1,SECURITY_GROUP_ID2...]`

##### Options

- `INSTANCE_ID`: ID of the server instance
- `PORT_SPEED`: Speed of the network interface in Mbps
- `--ipv4 IPV4_ADDRESS`: primary IPv4 address
- `--ipv6 IPV6_ADDRESS`: primary IPv6 address (not for beta?)
- `--secondary-addresses ADDR1,ADDR2...`: secondary IP addresses
- `--security-groups SECURITY_GROUP_ID1,SECURITY_GROUP_ID2...`: security group IDs


---

### `ibmcloud is instance-network-interface-update`

Update a network interface of a server instance

#### Syntax

`ibmcloud is instance-network-interface-update INSTANCE_ID NIC_ID [--name NEW_NAME] [--port-speed SPEED]`
##### Options

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `--name NEW_NAME`: New name of NIC
- `--port-speed SPEED`: New speed of the NIC

---

### `ibmcloud is instance-network-interface-delete`

Delete a network interface from a server

#### Syntax

`ibmcloud is instance-network-interface-delete INSTANCE_ID NIC_ID [-f, --force]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `-f, --force`: Delete without confirmation

---

### `ibmcloud is instance-network-interface-floating-ips`

List all floating IPs associated with a network interface

#### Syntax

`ibmcloud is instance-network-interface-floating-ips INSTANCE_ID NIC_ID --json`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface-floating-ip`

Show details of a floating IP associated with a network interface

#### Syntax

`ibmcloud is instance-network-interface-floating-ip INSTANCE_ID NIC_ID FLOATING_IP_ID [--json]`


##### Options

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `FLOATING_IP_ID`: ID of the floating IP
- `--json`: Format output in JSON

---

### `ibmcloud is instance-network-interface-floating-ip-add`

Associate a floating IP to a network interface

#### Syntax
`ibmcloud is instance-nic-floating-ip-add INSTANCE_ID NIC_ID FLOATING_IP_ID [--json]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `FLOATING_IP_ID`: ID of the floating IP
- `--json`: Format output in JSON
---

### `ibmcloud is instance-network-interface-floating-ip-remove`

Disassociate a floating IP from a server

#### Syntax

`ibmcloud is instance-nic-floating-ip-remove INSTANCE_ID NIC_ID FLOATING_IP_ID [-f, --force]`

##### Options

- `INSTANCE_ID `: ID of the server instance
- `NIC_ID `: ID of the NIC
- `FLOATING_IP_ID`: ID of the floating IP
- `-f, --force`: Remove without confirmation
