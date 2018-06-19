---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# VPC Beta API Reference
The VPC APIs are a portion of the Regional Infrastructure API Service (RIAS) APIs and they are fully integrated into the IBM Cloud APIs. 

For the Beta release, the VPC APIs include Network, Compute, and Geography. These are REST APIs, which include the standard functionalities: CREATE, READ, UPDATE, DELETE.

To see a tested sequence of API calls that you can use, please refer to our [Example Code Tutorial](example-code-tutorial.html).

The detailed parameters are specified in the sections that follow. 

**Note:** Although some API calls do not have required parameters, many calls do have **required** "Request Body" information that must be specified in JSON format. We have provided code examples of the minimum required data in JSON format.

## API for Network
### GET/floating_ips
This request retrieves all floating IPs in the region. Floating IPs allow ingress and egress traffic from the Internet to an instance.

* **Required Parameters**: 
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`: The number of resources to return on a page.
	* `resource_group.id`: Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers.
* **Return**: `200: The floating IPs were retrieved successfully.`

### POST/floating_ips
This request reserves a new floating IP.

* **Required Parameters**: None
* **Request Body**: _required_
	The floating IP template: 

```
	{
  "name": "my-new-floating-ip",
  "target": {
    "id": "69e55145-cc7d-4d8e-9e1f-cc3fb60b1793"
  }
}
```

* **Return**: 
	* `201: The floating IP was reserved successfully.`
	* `400: An invalid floating IP template was provided.`

### DELETE/floating_ips/{id}
This request releases a floating IP. This operation cannot be reversed.

* **Required Parameters**: `id`: The floating IP identifier.
* **Return**: 
	* `204: The floating IP was released successfully.`
	* `404: The specified floating IP could not be found.`

### GET/floating_ips/{id}
This request retrieves a single floating IP specified by the identifier in the URL.

* **Required Parameters**: `id`: The floating IP identifier.
* **Return**: 
	* `200: The floating IP was retrieved successfully.`
	* `404: The specified floating IP could not be found.`

### PATCH/floating_ips/{id}
This request updates a floating IP's name and/or target.

* **Required Parameters**: `id`: The floating IP identifier.
* **Request Body**: _required_

    The floating IP patch:

	```
	{
  	"name": "my-resource",
  	"target": {
    	"id": "69e55145-cc7d-4d8e-9e1f-cc3fb60b1793"
  	}
	}
	```

* **Return**: 
	* `200: The floating IP was updated successfully.`
	* `400: The supplied floating IP patch was invalid.`
	* `404: The specified floating IP could not be found.`

### GET/network_acls
This request retrieves all network ACLs in the region. A network ACL defines a set of packet filtering (5-tuple) rules for all traffic in and out of a subnet. Both allow and deny rules can be defined, and rules are stateless such that reverse traffic in response to allowed traffic is not automatically permitted.

* **Required Parameters**: 
	* `start`: A server-supplied token determining what resource to start the page on.
	* 'limit': The number of resources to return on a page.
	* 'resource_group.id': Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers.
* **Return**: `200: Network ACLs retrieved successfully.`

### POST/network_acls
This request creates a new network ACL from a network ACL template. The network ACL template object is structured in the same way as a retrieved network ACL, and contains the information necessary to create the new network ACL.

* **Required Parameters**: None.
* **Request Body:** _required_

    The network ACL template:

```
{
  "name": "my-network-acl"
}
```

* **Return**: 
	* `201: Network ACL created successfully.`
	* `400: Invalid network ACL template provided.`
	* `404: The specified floating IP could not be found.`

### DELETE/network_acls/{id}
This request deletes a network ACL. This operation cannot be reversed.

* **Required Parameters**: `id`: The network ACL identifier.
* **Return**: 
	* `204: Network ACL deleted successfully.`
	* `404: The network ACL with the specified identifier could not be found.`

### GET/network_acls/{id}
This request retrieves a single network ACL specified by the identifier in the URL.

* **Required Parameters**: `id`: The network ACL identifier.
* **Return**: 
	* `200: Network ACL was retrieved successfully.`
	* `404: The network ACL with the specified identifier could not be found.`

### PATCH/network_acls/{id}
This request updates a network ACL's name.

* **Required Parameters**: `id`: The network ACL identifier.
* **Request Body**: _required_

    The network ACL patch:

```
{
  "name": "my-network-acl"
}
```

* **Return**: 
	* `200: Network ACL was updated successfully.`
	* `400: An invalid network ACL patch was provided.`

### GET/network_acls/{network_acl_id}/rules
This request retrieves all rules for a network ACL. These rules can allow or deny traffic between a source CIDR block and a destination CIDR block over a particular protocol and port range.

* **Required Parameters**: 
	* `network_acl_id`: The network ACL identifier.
	* `limit`: The number of resources to return on a page.
	* `direction`: Filters the collection to rules with the specified direction.
* **Return**: 
	* `200: The rules were retrieved successfully.`
	* `404: The network ACL with the specified identifier could not be found.`

### POST/network_acls/{network_acl_id}/rules
This request creates a new rule from a rule template. The rule template object is structured in the same way as a retrieved rule, and contains the information necessary to create the new rule.

* **Required Parameters**: 
	* `network_acl_id`: The network ACL identifier.
* **Request Body**: _required_

The rule template:

```
{
  "action": "allow",
  "before": {
    "id": "8daca77a-4980-4d33-8f3e-7038797be8f9"
  },
  "destination": "192.168.0.0/24",
  "direction": "ingress",
  "name": "my-acl-rule-2",
  "port_max": 81,
  "port_min": 80,
  "protocol": "tcp",
  "source": "10.0.0.5"
}
```

* **Return**: 
	* `201: The rule was created successfully.`
	* `400: An invalid rule template was provided.`
	* `404: The network ACL with the specified identifier could not be found.`

### DELETE/network_acls/{network_acl_id}/rules/{id}
This request deletes a rule. This operation cannot be reversed.

* **Required Parameters**: 
	* `network_acl_id`: The network ACL identifier.
	* `id`: The rule identifier.
* **Return**: 
	* `204: The rule was deleted successfully.`
	* `404: A rule with the specified identifier could not be found.`

### GET/network_acls/{network_acl_id}/rules/{id}
This request retrieves a single rule specified by the identifier in the URL.

* **Required Parameters**: 
	* `network_acl_id`: The network ACL identifier.
	* `id`: The rule identifier.
* **Return**: 
	* `200: The rule was retrieved successfully.`
	* `404: A rule with the specified identifier could not be found.`

### PATCH/network_acls/{network_acl_id}/rules/{id}
This request updates a rule with the information in a provided rule patch. The rule patch object is structured in the same way as a retrieved rule and contains only the information to be updated.

* **Required Parameters**: 
	* `network_acl_id`: The network ACL identifier.
	* `id`: The rule identifier.
* **Request Body:** _required_

    The rule patch:

```
{
  "action": "allow",
  "destination": "192.168.0.0/24",
  "direction": "ingress",
  "name": "my-acl-rule-2",
  "source": "10.0.0.5",
  "before": {
    "id": "8daca77a-4980-4d33-8f3e-7038797be8f9"
  }
}
```

* **Return**: 
	* `200: The rule was retrieved successfully.`
	* `400': An invalid rule patch was provided.`
	* `404: A rule with the specified identifier could not be found.`

### GET/public_gateways
This request retrieves all public gateways. A public gateway is a virtual network device associated with a VPC which allows access to the Internet. A public gateway resides in a zone and can only be connected to subnets in the same zone.

* **Required Parameters**: 
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`: The number of resources to return on a page.
	* `resource_group.id`: Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers.
* **Return**: 
	* `200: The public gateways were retrieved successfully.`
	* `400': An invalid rule patch was provided.`
	* `404: A rule with the specified identifier could not be found.`

### POST/public_gateways
This request creates a new public gateway from a public gateway template. A public gateway can be created with an existing unbound floating address. If a floating address is not supplied, one will be created and bound to the public gateway. Once a public gateway is created, its external address cannot be unbound. The only way to rebind a floating address bound to a public gateway is to delete the gateway.

* **Required Parameters**: None.
* **Request Body**: _required_

    The public gateway template:

```
{
  "name": "my-gateway",
  "floating_ip": {
    "address": "203.0.113.1"
  },
  "resource_group": {
    "id": "56969d60-43e9-465c-883c-b9f7363e78e8"
  },
  "vpc": {
    "id": "4727d842-f94f-4a2d-824a-9bc9b02c523b"
  },
  "zone": {
    "name": "us-south-1"
  }
}
```

* **Return**: 
	* `201: The public gateway was created successfully.`
	* `400': An invalid public gateway was provided.`

### DELETE/public_gateways/{id}
This request deletes a public gateway. This operation cannot be reversed.

* **Required Parameters**: `id`: The public gateway identifier.
* **Return**: 
	* `204: The public gateway was deleted successfully.`
	* `400: A public gateway with the specified identifier could not be found.`

### GET/public_gateways/{id}
This request retrieves a single public gateway specified by the identifier in the URL.

* **Required Parameters**: `id`: The public gateway identifier.
* **Return**: 
	* `200: The public gateway was retrieved successfully.`
	* `400: A public gateway with the specified identifier could not be found.`

### PATCH/public_gateways/{id}
This request updates a public gateway's name.

* **Required Parameters**: `id`: The public gateway identifier.
* **Request Body**: _required_

    The public gateway patch:

```
{
  "name": "my-gateway"
}
```

* **Return**: 
	* `200: The public gateway was updated successfully.`
	* `400: The supplied public gateway patch was invalid.`

### GET/security_groups
Retrieves a paginated list of all security groups belonging to this account.

* **Required Parameters**: 
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`': The number of resources to return on a page.
	* `resource_group.id`: Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers
* **Return**: `200: The security groups were retrieved successfully.`

### POST/security_groups
Creates a new security group. Security group rules created as part of this operation use IPv4 by default.

* **Required Parameters**: None.
* **Request Body**: _required_

    The properties of the security group to be created:

```
{
  "name": "allow_ssh",
  "resource_group": {
    "id": "56969d60-43e9-465c-883c-b9f7363e78e8"
  },
  "rules": [
    {
      "direction": "ingress",
      "port_max": 22,
      "port_min": 22,
      "protocol": "tcp",
      "remote": {
        "cidr_block": "192.168.0.0/24"
      }
    }
  ],
  "tags": [
    "production",
    "backend"
  ],
  "vpc": {
    "id": "4727d842-f94f-4a2d-824a-9bc9b02c523b"
  }
}
```

* **Return**: 
	* `201: The security group was created successfully.`
	* `400: An invalid security group template was provided.`

### DELETE/security_groups
Deletes a security group. This operation cannot be reversed.

* **Required Parameters**: `id`: The security group identifier.
* **Return**: 
	* `204: The security group was deleted successfully.`
	* `404: A security group with the specified identifier could not be found.`

### GET/security_groups/{id}
Retrieves a single security group specified by the identifier in the URL path.

* **Required Parameters**: `id`: The security group identifier.
* **Return**: 
	* `200: The security group was retrieved successfully.`
	* `404: A security group with the specified identifier could not be found.`

### PATCH/security_groups/{id}
Updates the properties of an existing security group.

* **Required Parameters**: `id`: The security group identifier.
* **Request Body**:   _required_

  The security group patch:

```
{
  "name": "allow_ssh"
}
```

* **Return**: 
	* `200: The security group was updated successfully.`
	* `400: An invalid security group patch was provided.`

### GET/security_groups/{security_group_id}/network_interfaces
Retrieves a paginated collection of all the network interfaces in a security group.

* **Required Parameters**: `security_group_id`: The security group identifier.
* **Return**: 
	* `200: The network interfaces were retrieved successfully.`
	* `404: A security group with the specified identifier could not be found.`

### DELETE/security_groups/{security_group_id}/network_interfaces/{id}
Removes a network interface from a security group.

* **Required Parameters**: 
	* `security_group_id`: The security group identifier.
	* `id`: The network interface identifier.
* **Return**: 
	* `204: The network interface was successfully removed from the security group.`
	* `404: The specified network interface was not in the specified security group.`

### GET/security_groups/{security_group_id}/network_interfaces/{id}
Gets a network interface in a security group.

* **Required Parameters**: 
	* `security_group_id`: The security group identifier.
	* `id`: The network interface identifier.
* **Return**: 
	* `200: The requested network interface was retrieved successfully.`
	* `404: The specified network interface was not in the specified security group.`

### PUT/security_groups/{security_group_id}/network_interfaces/{id}
Adds an existing network interface to an existing security group.

* **Required Parameters**: 
	* `security_group_id`: The security group identifier.
	* `id`: The network interface identifier.
* **Return**: 
	* `201: The network interface was successfully added to the security group.`
	* `400: The specified network interface could not be added to the specified security group.`
	* `404: The specified network interface or security group could not be found.`

### GET/security_groups/{security_group_id}/rules
Retrieves all the rules of a particular security group.

* **Required Parameters**: `security_group_id`: The security group identifier.
* **Return**: 
	* `200: The security group rules were retrieved successfully.`
	* `404: A security group with the specified identifier could not be found.`

### POST/security_groups/{security_group_id}/rules
Retrieves all the rules of a particular security group. The IP address defaults to IPv4.

* **Required Parameters**: `security_group_id`: The security group identifier.
* **Request Body**: _required_

    The properties of the security group rule to be created:

```
{
  "direction": "ingress",
  "port_max": 22,
  "port_min": 22,
  "protocol": "tcp",
  "remote": {
    "cidr_block": "192.168.0.0/24"
  }
}
```

* **Return**: 
	* `200: The security group rules were retrieved successfully.`
	* `404: A security group with the specified identifier could not be found.`

### DELETE/security_groups/{security_group_id}/rules/{id}
Deletes a rule from a security group. This operation cannot be reversed.

* **Required Parameters**: 
	*  `security_group_id`: The security group identifier.
	* `id`: The network interface identifier. 
* **Return**: 
	* `204: The rule was deleted successfully.`
	* `404: A rule with the specified identifier could not be found.`

### GET/security_groups/{security_group_id}/rules/{id}
Retrieves a single security group rule specified by identifier.

* **Required Parameters**: 
	* 	* `security_group_id`: The security group identifier.
	* `id`: The network interface identifier. 
* **Return**: 
	* `200: The rule was retrieved successfully.`
	* `404: A rule with the specified identifier could not be found.`

### PATCH/security_groups/{security_group_id}/rules/{id}
Updates the properties of an existing rule on a security group. The IP address defaults to IPv4.

* **Required Parameters**: 
	* `security_group_id`: The security group identifier.
	* `id`: The network interface identifier. 
* **Request Body**: _required_

    The security group rule patch.

```
{
  "direction": "ingress",
  "port_max": 22,
  "port_min": 22,
  "protocol": "tcp",
  "remote": {
    "cidr_block": "192.168.0.0/24"
  }
}
```

* **Return**: 
	* `200: The security group rule was updated successfully.`
	* `400: An invalid security group patch was provided.`
	* `404: A rule with the specified identifier could not be found.`

### GET/subnets
This request retrieves all subnets in the region. Subnets are contiguous ranges of IP addresses specified in CIDR block notation. Each subnet is within a particular zone and cannot span multiple zones or regions.

* **Required Parameters**: 
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`': The number of resources to return on a page.
	* `resource_group.id`: Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers 
* **Return**: 
	* `200: The subnets were retrieved successfully.`

### POST/subnets
This request creates a new subnet from a subnet template. The subnet template object is structured in the same way as a retrieved subnet, and contains the information necessary to create the new subnet.

* **Required Parameters**: None
* **Request Body**: _required_

    The subnet template:

```
{
  "total_ipv4_address_count": 256,
  "vpc": {
    "id": "4727d842-f94f-4a2d-824a-9bc9b02c523b"
  },
  "zone": {
    "name": "us-south-1"
  }
}
```

* **Return**: 
	* `201: The subnet was created successfully.`
	* `400: An invalid subnet template was provided.`

### DELETE/subnets/{id}
This request deletes a subnet. This operation cannot be reversed.

* **Required Parameters**:`id`: The subnet identifier. 
* **Return**: 
	* `200: The subnet was deleted successfully.`
	* `404: A subnet with the specified identifier could not be found.`

### GET/subnets/{id}
This request retrieves a single subnet specified by the identifier in the URL.

* **Required Parameters**:`id`: The subnet identifier. 
* **Return**: 
	* `200: The subnet was retrieved successfully.`
	* `404: A subnet with the specified identifier could not be found.`

### PATCH/subnets/{id}
This request updates a subnet with the information in a provided subnet patch. The subnet patch object is structured in the same way as a retrieved subnet and contains only the information to be updated.

* **Required Parameters**:`id`: The subnet identifier. 
* **Request Body**: _required_

    The subnet patch:

```
{
  "name": "my-subnet",
  "network_acl": {
    "id": "a4e28308-8ee7-46ab-8108-9f881f22bdbf"
  },
  "public_gateway": {
    "id": "dc5431ef-1fc6-4861-adc9-a59d077d1241"
  }
}
```

* **Return**: 
	* `200: The subnet was updated successfully.`
	* `400: The supplied subnet patch was invalid.`
	* `404: A subnet with the specified identifier could not be found.`

### GET/subnets/{id}/network_acl
This request retrieves the network ACL attached to the subnet specified by the identifier in the URL.

* **Required Parameters**:`id`: The subnet identifier. 
* **Return**: 
	* `200: The attached network ACL was retrieved successfully.`
	* `404: The specified subnet could not be found.`

### PUT/subnets/{id}/network_acl
This request attaches the network ACL specified in the request body to the subnet specified by the subnet identifier in the URL. If a network ACL is already attached to the subnet, it is detached before the new network ACL is attached.

* **Required Parameters**:`id`: The subnet identifier. 
* **Return**: 
	* `201: The network ACL was attached successfully.`
	* `400: The specified network ACL could not be attached to the specified subnet.`
	* `404: The specified subnet could not be found.`

### DELETE/subnets/{id}/public_gateway
This request detaches the public gateway from the subnet specified by the subnet identifier in the URL.

* **Required Parameters**:`id`: The subnet identifier. 
* **Return**: 
	* `204: The public gateway was detached successfully.`
	* `404: The specified subnet could not be found.`

### GET/subnets/{id}/public_gateway
This request retrieves the public gateway attached to the subnet specified by the identifier in the URL.

* **Required Parameters**:`id`: The subnet identifier. 
* **Return**: 
	* `204: The attached public gateway was retrieved successfully.`
	* `404: The specified subnet could not be found.`

### PUT/subnets/{id}/public_gateway
This request attaches the public gateway specified in the request body to the subnet specified by the subnet identifier in the URL. If a public gateway is already attached to the subnet, it is detached before the new public gateway is attached.

* **Required Parameters**:`id`: The subnet identifier. 
* **Request Body**: _required_

    The network ACL identity:

```
{
  "id": "a4e28308-8ee7-46ab-8108-9f881f22bdbf"
}
```

* **Return**: 
	* `201: The public gateway was attached successfully.`
	* `400: The specified public gateway could not be attached to the specified subnet.`
	* `404: The specified subnet could not be found.`

### GET/vpcs
This request retrieves all VPCs. A VPC is a virtual network that belongs to an account and provides logical isolation from other networks. A VPC is made up of resources in one or more zones. VPCs are global and each can contain resources in zones from any region.

* **Required Parameters**:
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`: The number of resources to return on a page. 
	* `resource_group.id`: Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers. 
* **Return**: 
	* `201: The VPCs were retrieved successfully.`
	* `400: The specified public gateway could not be attached to the specified subnet.`
	* `404: The specified subnet could not be found.`

### POST/vpcs
This request creates a new VPC from a VPC template. The VPC template object is structured in the same way as a retrieved VPC, and contains the information necessary to create the new VPC.

* **Required Parameters**: None
* **Request Body**: _required_

    The VPC template:

```
{
  "default_network_acl": {
    "id": "a4e28308-8ee7-46ab-8108-9f881f22bdbf"
  },
  "is_default": true,
  "name": "my-vpc",
  "resource_group": {
    "id": "56969d60-43e9-465c-883c-b9f7363e78e8"
  }
}
```

* **Return**: 
	* `201: The VPC was created successfully.`
	* `400: An invalid VPC template was provided.`

### DELETE/vpcs
This request deletes a VPC. This operation cannot be reversed. For this request to succeed, the VPC must not contain any instances, subnets, security groups, or public gateways.

* **Required Parameters**: `id`: The VPC identifier.
* **Return**: 
	* `204: The VPC was deleted successfully.`
	* `400: The VPC could not be deleted.`
	* `404: A VPC with the specified identifier could not be found.`

### GET/vpcs/{id}
This request retrieves a single VPC specified by the identifier in the URL.

* **Required Parameters**: `id`: The VPC identifier.
* **Return**: 
	* `200: The VPC was retrieved successfully.`
	* `404: A VPC with the specified identifier could not be found.`

### PATCH/vpcs/{id}
This request updates a VPC's name.

* **Required Parameters**: `id`: The VPC identifier.
* **Request Body**: _required_

    The VPC patch:

```
{
  "name": "my-vpc"
}
```

* **Return**: 
	* `200: The VPC was updated successfully.`
	* `400: The supplied VPC patch was invalid.`
	* `404: A VPC with the specified identifier could not be found.`

### GET/vpcs/{vpc_id}/address_prefixes
This request retrieves all address pool prefixes for a VPC.

* **Required Parameters**: `vpc_id`: The VPC identifier.
* **Return**: 
	* `200: The prefixes were retrieved successfully.`
	* `404: The specified VPC could not be found.`

### POST/vpcs/{vpc_id}/address_prefixes
This request creates a new prefix from a prefix template. The prefix template object is structured in the same way as a retrieved prefix, and contains the information necessary to create the new prefix.

* **Required Parameters**: `vpc_id`: The VPC identifier.
* **Request Body**: _required_

    The prefix template:

```
{
  "name": "my-address-pool-prefix-2",
  "cidr": "10.0.0.0/24",
  "zone": {
    "name": "us-south-1"
  }
}
```

* **Return**: 
	* `201: The prefix was created successfully.`
	* `400: An invalid prefix template was provided.`
	* `404: The specified VPC could not be found.`

### DELETE/vpcs/{vpc_id}/address_prefixes/{id}
This request deletes a prefix. This operation cannot be reversed. Delete will fail if existing subnets use addresses from this prefix.

* **Required Parameters**: 
	* `vpc_id`: The VPC identifier.
	* `id`: The prefix identifier.
* **Return**: 
	* `204: The prefix was deleted successfully.`
	* `404: A prefix with the specified identifier could not be found.`

### GET/vpcs/{vpc_id}/address_prefixes/{id}
This request retrieves a single prefix specified by the identifier in the URL.

* **Required Parameters**: 
	* `vpc_id`: The VPC identifier.
	* `id`: The prefix identifier.
* **Return**: 
	* `200: The prefix was retrieved successfully.`
	* `404: A prefix with the specified identifier could not be found.`

### PATCH/vpcs/{vpc_id}/address_prefixes/{id}
This request updates a prefix with the information in a provided prefix patch. The prefix patch object is structured in the same way as a retrieved prefix and contains only the information to be updated. The update will fail if it would result in existing subnets falling outside of the address pool. The update will fail if the new prefix overlaps any other prefix in the VPC's address pools.

* **Required Parameters**: 
	* `vpc_id`: The VPC identifier.
	* `id`: The prefix identifier.
* **Request Body**: _required_

    The prefix patch:

```
{
  "name": "my-address-pool-prefix-2",
  "cidr": "10.0.0.0/24"
}
```

* **Return**: 
	* `200: The prefix was updated successfully.`
	* `400: An invalid prefix patch was provided.`
	* `404: A prefix with the specified identifier could not be found.`
  
## API for Compute
### GET/images
This request retrieves all images available in the region. Images represent a specific software configuration for an instance. Some images are system-provided. Images can also be created from instances or imported from another source.

* **Required Parameters**: 
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`: The number of resources to return on a page. 
	* `resource_group.id`: Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers.
* **Return**: `200: Images retrieved successfully.`

### GET/images/{id}
This request retrieves a single image specified by the identifier in the URL.

* **Required Parameters**: `id`: The image identifier.
* **Return**: 
	* `200: Images retrieved successfully.`
	* `400: An image with the specified identifier could not be found.`

### GET/instance/profiles
This request retrieves all instance profiles available in the region. An instance profile specifies the performance characteristics and pricing model for an instance.

* **Required Parameters**: 
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`: The number of resources to return on a page.  
* **Return**: `200: Instance profiles retrieved successfully.`

### GET/instance/profiles/{name}
This request retrieves a single instance profile specified by the name in the URL.

* **Required Parameters**: `name`: The instance profile name.
* **Return**: 
	* `200: Instance profile retrieved successfully.`
	* `404: An instance profile with the specified name could not be found.`

### GET/instances
This request retrieves all instances in the region.

* **Required Parameters**: 
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`: The number of resources to return on a page. 
	* `resource_group.id`: Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers.
	* `network_interfaces.subnet.id`: Filters the collection to instances on the subnet of the specified identifier. 
	* `network_interfaces.subnet.cm`: Filters the collection to instances on the subnet of the specified CRN.
	* `network_interfaces.subnet.name`: Filters the collection to instances on the subnet of the specified name.
* **Return**: 
	* `200: The instances were retrieved successfully.`

### POST/instances
This request provisions a new instance from an instance template. The instance template object is structured in the same way as a retrieved instance, and contains the information necessary to provision the new instance.

* **Required Parameters**: None
* **Request Body**: _required_

    The instance template:

```
{
  "image": {
    "name": "my-image"
  },
  "keys": [
    {
      "fingerprint": "yxavE4CIOL2NlsqcurRO3xGjkP6m/0mp8ugojH5yxlY"
    }
  ],
  "profile": {
    "name": "gc.balanced.4x16"
  },
  "vpc": {
    "name": "my-vpc"
  }
}
```

* **Return**: 
	* `201: The instance was created successfully.`
	* `400: Invalid instance template provided.`

### DELETE/instances/{id}
This request deletes an instance. This operation cannot be reversed.

* **Required Parameters**: `id`: The instance identifier.
* **Return**: 
	* `204: The instance was deleted successfully.`
	* `404: An instance with the specified identifier could not be found.`

### GET/instances/{id}
This request retrieves a single instance specified by the identifier in the URL.

* **Required Parameters**: `id`: The instance identifier.
* **Return**: 
	* `200: The instance was retrieved successfully.`
	* `404: An instance with the specified identifier could not be found.`

### PATCH/instances/{id}
This request updates an instance with the information in a provided instance patch. The instance patch object is structured in the same way as a retrieved instance and contains only the information to be updated.

* **Required Parameters**: `id`: The instance identifier.
* **Request Body**: _required_

    The instance patch:

```
{
  "name": "my-instance",
  "profile": {
    "name": "gc.balanced.4x16"
  }
}
```

* **Return**: 
	* `200: The instance was updated successfully.`
	* `400: The supplied instance patch was invalid.`
	* `404: An instance with the specified identifier could not be found.`

### GET/instances/{instance_id}/actions
This request retrieves all pending, running, and recent actions on an instance.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`: The number of resources to return on a page.   
* **Return**: 
	* `200: The instance actions were retrieved successfully.`
	* `404: An instance with the specified identifier could not be found.`

### POST/instances/{instance_id}/actions
This request creates a new action which will be queued up to run as soon as any currently pending or running actions have completed.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
* **Request Body**: _required_

    The instance action template:

```
{
  "type": "start"
}
```

* **Return**: 
	* `201: The action was created successfully and will run in the order it was received.`
	* `400: The specified action could not be created.`
	* `404: An instance with the specified identifier could not be found.`

### GET/instances/{instance_id}/actions
This request retrieves all pending, running, and recent actions on a virtual server instance.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`: The number of resources to return on a page.   
* **Return**: 
	* `200: The instance actions were retrieved successfully.`
	* `404: An instance with the specified identifier could not be found.`

### DELETE/instances/{instance_id}/actions/{id}
This request deletes an instance action. It will only succeed if the action is currently pending.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `id`: The instance action identifier.
* **Return**: 
	* `204: The instance action was deleted successfully, preventing the action from being executed.`
	* `400: The specified action could not be deleted.`
	* `404: An action with the specified identifier could not be found for the specified instance.`

### GET/instances/{instance_id}/actions/{id}
This request retrieves a single instance action specified by the identifier in the URL.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `id`: The instance action identifier.
* **Return**: 
	* `200: The instance action was retrieved successfully.`
	* `404: An action with the specified identifier could not be found for the specified instance.`

### GET/instances/{instance_id}/network_interfaces
This request retrieves all network interfaces on an instance. A network interface is an abstract representation of a network interface card and connects an instance to a subnet. Instances may have more than one network interface, but each network interface can be attached to only one subnet.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `resource_group.id`: Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers
* **Return**: 
	* `200: The network interfaces were retrieved successfully.`
	* `404: An instance with the specified identifier could not be found.`

### GET/instances/{instance_id}/network_interfaces/{id}
This request retrieves a single network interface specified by the identifier in the URL.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `id`: The network interface identifier.
* **Return**: 
	* `200: The network interface was retrieved successfully.`
	* `404: A network interface with the specified identifier could not be found.`

### PATCH/instances/{instance_id}/network_interfaces/{id}
This request updates a network interface with the information in a provided network interface patch. The network interface patch object is structured in the same way as a retrieved network interface and can contain an updated name and/or port speed.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `id`: The network interface identifier.
* **Request Body**: _required_

    The network interface patch:

```
{
  "name": "my-network-interface",
  "port_speed": 10000
}
```
 
* **Return**: 
	* `200: The network interface was updated successfully.`
	* `400: An invalid network interface patch was provided.`
	* `404: A network interface with the specified identifier could not be found.`

### GET/instances/{instance_id}/network_interfaces/{network_interface_id}/floating_ips
This request retrieves all floating IPs associated with a network interface.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `network_interface_id`: The network interface identifier.
* **Return**: 
	* `200: The associated floating IPs were retrieved successfully.`
	* `404: A network interface with the specified identifier could not be found.`

### DELETE/instances/{instance_id}/network_interfaces/{network_interface_id}/floating_ips/{id}
This request disassociates all floating IPs associated with a network interface.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `network_interface_id`: The network interface identifier.
	* `id`: The floating IP identifier.
* **Return**: 
	* `200: The floating IP was disassociated successfully.`
	* `400: The specified floating IP could not be disassociated.`
	* `404: The specified floating IP address is not associated with the network interface with the specified identifier.`

### GET/instances/{instance_id}/network_interfaces/{network_interface_id}/floating_ips/{id}
This request a retrieves a specified floating IP address if it is associated with the network interface and instance specified in the URL.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `network_interface_id`: The network interface identifier.
	* `id`: The floating IP identifier.
* **Return**: 
	* `200: The associated floating IP was retrieved successfully.`
	* `404: The floating IP address is not associated with a network interface with the specified identifier.`

### PUT/instances/{instance_id}/network_interfaces/{network_interface_id}/floating_ips/{id}
This request associates the specified floating IP with the specified network interface.

* **Required Parameters**: 
	* `instance_id`: The instance identifier.
	* `network_interface_id`: The network interface identifier.
	* `id`: The floating IP identifier.
* **Return**: 
	* `201: The floating IP was successfully associated with the network interface.`
	* `400: The specified IP could not be associated with the specified network interface.`
	* `404: An instance with the specified identifier could not be found.`
	
### GET/keys
This request retrieves all keys. A key contains a public 2048-bit RSA SSH key which may be installed on instances when they are created. Private keys are not stored by the system.

* **Required Parameters**: 
	* `start`: A server-supplied token determining what resource to start the page on.
	* `limit`: The number of resources to return on a page. 
	* `resource_group.id`: Filters the collection to resources within one of the resource groups identified in a comma-separated list of resource group identifiers.
* **Return**: `200: The keys were retrieved successfully.`

### POST/keys
This request imports a new key from a key template containing a public 2048-bit RSA SSH key.

* **Required Parameters**: None.
* **Request Body**: _required_

   The key template:

```
{
  "name": "my-key",
  "public_key": "AAAAB3NzaC1yc2EAAAADAQABAAABAQDDGe50Bxa5T5NDddrrtbx2Y4/VGbiCgXqnBsYToIUKoFSHTQl5IX3PasGnneKanhcLwWz5M5MoCRvhxTp66NKzIfAz7r+FX9rxgR+ZgcM253YAqOVeIpOU408simDZKriTlN8kYsXL7P34tsWuAJf4MgZtJAQxous/2byetpdCv8ddnT4X3ltOg9w+LqSCPYfNivqH00Eh7S1Ldz7I8aw5WOp5a+sQFP/RbwfpwHp+ny7DfeIOokcuI42tJkoBn7UsLTVpCSmXr2EDRlSWe/1M/iHNRBzaT3CK0+SwZWd2AEjePxSnWKNGIEUJDlUYp7hKhiQcgT5ZAnWU121oc5En",
  "resource_group": {
    "id": "56969d60-43e9-465c-883c-b9f7363e78e8"
  },
  "type": "rsa"
}
```

* **Return**: 
	* `201: The key was created successfully.`
	* `400: An invalid key template was provided.`

### DELETE/keys/{id}
This request deletes a key. This operation cannot be reversed.

* **Required Parameters**: `id`: The key identifier.
* **Return**: 
	* `204: The key was deleted successfully.`
	* `400: The key could not be deleted.`
	* `404: A key with the specified identifier could not be found.`

### GET/keys/{id}
This request retrieves a single key specified by the identifier in the URL.

* **Required Parameters**: `id`: The key identifier.
* **Return**: 
	* `200: The key was retrieved successfully.`
	* `404: A key with the specified identifier could not be found.`

### PATCH/keys/{id}
This request updates a key's name.

* **Required Parameters**: `id`: The key identifier.
* **Request Body**: _required_

    The key patch:

```
{
  "name": "my-key"
}
```

* **Return**: 
	* `200: The key was updated successfully.`
	* `400: The supplied key patch was invalid.`
	* `404: A key with the specified identifier could not be found.`
  
## API for Geography
### GET/regions
This request retrieves all regions. Each region is a separate geographic area containing multiple isolated zones. Resources can be provisioned into a one or more zones in a region. Each zone is isolated, but connected to other zones in the same region with low-latency and high-bandwidth links. Regions represent the top-level of fault isolation available. Resources deployed within a single region also benefit from the low latency afforded by geographic proximity.

* **Required Parameters**: None
* **Return**: `200: The regions were retrieved successfully.`

### GET/regions/{name}
This request retrieves a single region specified by the name in the URL.

* **Required Parameters**: `name`: The region name.
* **Return**: 
	* `200: The region name was retrieved successfully.`
	* `404: A region with the specified name could not be found.`

### GET/regions/{region_name}/zones
This request retrieves all zones in a region. Zones represent logically-isolated data centers with high-bandwidth, low-latency interconnects to other zones in the same region. Faults in a zone do not impact other zones.

* **Required Parameters**: `region_name`: The region name.
* **Return**: 
	* `200: The zones were retrieved successfully.`
	* `404: A region with the specified name could not be found.`

### GET/regions/{region_name}/zones/{zone_name}
This request retrieves a single zone specified by the region and zone names in the URL.

* **Required Parameters**: 
	* `region_name`: The region name.
	* `zone_name`: The zone name.
* **Return**: 
	* `200: The zone was retrieved successfully.`
	* `404: A zone with the specified name could not be found.`
