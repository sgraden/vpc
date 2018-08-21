---



copyright:
  years: 2017,2018
lastupdated: "2018-08-16"


---

<!-- Common attributes used in the template are defined as follows: -->
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Using VPN with your IBM Cloud VPC

VPN service allows you to connect private networks in a secure fashion.

For the {{site.data.keyword.cloud}} VPC Beta release, you can use VPN to set up an IPSec site-to-site tunnel between your VPC and
your on-premise private network or another VPC. Only policy-based routing is supported in the current release.

## Features

* IKEv1 and IKEv2
* Authentication algorithms: `md5`, `sha1`, `sha256`
* Encryption algorithms: `3des`, `aes128`, `aes256`
* Diffie-Hellman (DH) groups: 2, 5, 14
* IKE negotiation mode: main
* IPSec transform protocol: ESP
* IPSec encapsulation mode: tunnel
* Perfect Forward Secrecy (PFS)
* Dead Peer Detection
* Routing: Policy-based
* Authentication Mode: Pre-shared key

## APIs Available

The following section gives details about APIs you can use for VPN in your VPC environment.

### VPN Gateways and VPN Connections

| Description | API |
|-------------|-----|
| Creates a VPN gateway | POST /vpn_gateways |
| Retrieves VPN gateways | GET /vpn_gateways |
| Retrieves a VPN gateway | GET /vpn_gateways/{id} |
| Deletes a VPN gateway | DELETE /vpn_gateways/{id} |
| Updates a VPN gateway | PATCH /vpn_gateways/{id} |
| Creates a new VPN connection | POST /vpn_gateways/{vpn_gateway_id}/connections |
| Retrieves VPN connections | GET /vpn_gateways/{vpn_gateway_id}/connections |
| Retrieves a VPN connection | GET /vpn_gateways/{vpn_gateway_id}/connections/{id} |
| Deletes a VPN connection | DELETE /vpn_gateways/{vpn_gateway_id}/connections/{id} |
| Updates a VPN connection | PATCH /vpn_gateways/{vpn_gateway_id}/connections/{id} |
| Retrieves all local CIDRs for a VPN connection | GET /vpn_gateways/{vpn_gateway_id}/connections/{id}/local_cidrs |
| Deletes a local CIDR from a VPN connection | DELETE /vpn_gateways/{vpn_gateway_id}/connections/{id}/local_cidrs/{prefix_address}/{prefix_length} |
| Checks if a specific local CIDR exists on a VPN connection | GET /vpn_gateways/{vpn_gateway_id}/connections/{id}/local_cidrs/{prefix_address}/{prefix_length} |
| Sets a local CIDR on a VPN connection | PUT /vpn_gateways/{vpn_gateway_id}/connections/{id}/local_cidrs/{prefix_address}/{prefix_length} |
| Retrieves all peer CIDRs for a VPN connection | GET /vpn_gateways/{vpn_gateway_id}/connections/{id}/peer_cidrs |
| Deletes a peer CIDR from a VPN connection | DELETE /vpn_gateways/{vpn_gateway_id}/connections/{id}/peer_cidrs/{prefix_address}/{prefix_length} |
| Checks if a specific peer CIDR exists on a VPN connection | GET /vpn_gateways/{vpn_gateway_id}/connections/{id}/peer_cidrs/{prefix_address}/{prefix_length} |
| Sets a peer CIDR on a VPN connection | PUT /vpn_gateways/{vpn_gateway_id}/connections/{id}/peer_cidrs/{prefix_address}/{prefix_length} |

### IKE Policies

| Description | API |
|-------------|-----|
| Retrieves all IKE policies | GET /ike_policies |
| Creates an IKE policy | POST /ike_policies |
| Deletes an IKE policy | DELETE /ike_policies/{id} |
| Retrieves an IKE policy | GET /ike_policies/{id} |
| Updates an IKE policy | PATCH /ike_policies/{id} |
| Retrieves all the connections that use the specified IKE policy | GET /ike_policies/{id}/connections |

### IPSec Policies

| Description | API |
|-------------|-----|
| Retrieves all IPSec policies | GET /ipsec_policies |
| Creates an IPSec policy | POST /ipsec_policies |
| Deletes an IPSec policy | DELETE /ipsec_policies/{id} |
| Retrieves an IPSec policy | GET /ipsec_policies/{id} |
| Updates an IPSec policy | PATCH /ipsec_policies/{id} |
| Retrieves all the connections that use the specified IPsec policy | GET /ipsec_policies/{id}/connections |

## VPN Demo Examples

In the following example, you'll be able to connect two VPCs together using VPN, which means you can connect
subnets in two separate VPCs as if they were a single network. The IP addresses of the subnets must not overlap.
Here is what the scenario looks like (with some VMs added in each VPC):
![An example VPN scenario](images/vpc-vpn.png)

### Example Steps

The example steps that follow skip the prerequsite steps of using IBM Cloud Internal Beta API or CLI to create VPCs. For more information, see [Getting Started](getting-started.html) and [VPC setup with APIs](example-code.html).

**Step 1. Create a VPN gateway on your VPC subnet.**

```bash
curl -H "X-Auth-Token:$iam_token" -X POST https://us-south.iaas.cloud.ibm.com/v1/vpn_gateways \
    -d '{
            "name": "vpn-gateway-1",
            "subnet": {"id": "<SUBNET-ID-1>"}
        }'
```
{: codeblock}

Sample output:
```bash
{
    "created_at": "2018-07-06T19:19:28.694388Z",
    "href": "https://us-south.iaas.cloud.ibm.com/v1/vpn_gateways/7fd72524-6e2d-49a6-b975-0071efccd89a",
    "id": "7fd72524-6e2d-49a6-b975-0071efccd89a",
    "name": "vpn-gateway-1",
    "public_ip": {
        "address": "169.61.161.167"
    },
    "status": "pending",
    "subnet": {
        "href": "https://us-south.iaas.cloud.ibm.com/v1/subnets/f45ee0be-cf3f-41ca-a279-23139110aa58",
        "id": "f45ee0be-cf3f-41ca-a279-23139110aa58",
        "name": "subnet-1"
    }
}
```
{: codeblock}

Ensure the following fields are saved for subsequent steps.
* `id`. This is the VPN gateway ID and it will be referred to as `VPN-GATEWAY-1-ID`.
* `address`. This is the public IP address of the VPN gateway, and it will be referred to as `VPN-GATEWAY-1-IP`.

NOTE: The gateway status appears as `pending` while the VPN gateway is being created, and the status becomes `available` once creation is complete. Creation may take some time. You can check its status with the following command:
```bash
curl -H "X-Auth-Token:$iam_token" -X GET https://us-south.iaas.cloud.ibm.com/v1/vpn_gateways/<VPN-GATEWAY-1-ID>
```
{: codeblock}

**Step 2. Create a second VPN gateway on a different VPC.**

```bash
curl -H "X-Auth-Token:$iam_token" -X POST https://us-south.iaas.cloud.ibm.com/v1/vpn_gateways \
        -d '{
                "name": "vpn-gateway-2",
                "subnet": {"id": "<SUBNET-ID-2>"}
            }'
```
{: codeblock}

Sample output:
```bash
{
    "created_at": "2018-07-06T19:33:23.789675Z",
    "href": "https://us-south.iaas.cloud.ibm.com/v1/vpn_gateways/f72559a3-2fac-4958-b937-54474e6a8a8d",
    "id": "f72559a3-2fac-4958-b937-54474e6a8a8d",
    "name": "vpn-gateway-2",
    "public_ip": {
        "address": "169.61.161.150"
    },
    "status": "pending",
    "subnet": {
        "href": "https://us-south.iaas.cloud.ibm.com/v1/subnets/f72c7f7c-0fa5-42d1-9bdc-9e0acad53cb4",
        "id": "f72c7f7c-0fa5-42d1-9bdc-9e0acad53cb4",
        "name": "subnet-2"
    }
}
```
{: codeblock}

Be sure to save the following fields for subsequent steps.
* `id`. This is the VPN gateway ID, and it will be referred to as `VPN-GATEWAY-2-ID`.
* `address`. This is the public IP address of the VPN gateway, and it will be referred to as `VPN-GATEWAY-2-IP`.


**Step 3. Create a VPN connection from the first VPN gateway to the second VPN gateway, setting `local_cidrs` to the subnet on VPC one and `peer_cidrs` to the subnet on VPC two.**

```bash
curl -H "X-Auth-Token:$iam_token" -X POST https://us-south.iaas.cloud.ibm.com/v1/vpn_gateways/<VPN-GATEWAY-1-ID>/connections \
        -d '{
                "name": "vpn-connection-to-vpn-gateway-2",
                "peer_address": "<VPN-GATEWAY-2-IP>",
                "psk": "VPNDemoPassword",
                "local_cidrs": [ "<LOCAL-CIDR>" ],
                "peer_cidrs": [ "<PEER-CIDR>" ]
            }'
```
{: codeblock}

**Step 4. Create a VPN connection from the second VPN gateway to the first VPN gateway, setting `local_cidrs` to the subnet on VPC two and `peer_cidrs` to the subnet on VPC one.**

```bash
curl -H "X-Auth-Token:$iam_token" -X POST https://us-south.iaas.cloud.ibm.com/v1/vpn_gateways/<VPN-GATEWAY-2-ID>/connections \
        -d '{
                "name": "vpn-connection-to-vpn-gateway-1",
                "peer_address": "<VPN-GATEWAY-1-IP>",
                "psk": "VPNDemoPassword",
                "local_cidrs": [ "<LOCAL-CIDR>" ],
                "peer_cidrs": [ "<PEER-CIDR>" ]
            }'
```
{: codeblock}

**Step 5. Verify connectivity**
Once the VPN connection is established, you will be able to reach your instances on subnet two from subnet one, and vice versa.

You can check the status of the VPN connection as follows.
```bash
curl -H "X-Auth-Token:$iam_token" -X GET https://us-south.iaas.cloud.ibm.com/v1/vpn_gateways/<VPN-GATEWAY-1-ID>/connections
```
{: codeblock}

Sample output:
```bash
{
    "connections": [
        {
            "admin_state_up": true,
            "authentication_mode": "psk",
            "created_at": "2018-07-06T19:50:49.252072Z",
            "dead_peer_detection": {
                "action": "none",
                "interval": 30,
                "timeout": 120
            },
            "href": "https://us-south.iaas.cloud.ibm.com/v1/vpn_gateways/7fd72524-6e2d-49a6-b975-0071efccd89a/connections/a252d380-0784-45ff-8fc0-c2b58e446b4d",
            "id": "a252d380-0784-45ff-8fc0-c2b58e446b4d",
            "local_cidrs": [
                "192.168.100.0/24"
            ],
            "name": "vpn-connection-to-vpn-gateway-2",
            "peer_address": "169.61.161.150",
            "peer_cidrs": [
                "192.168.0.0/24"
            ],
            "psk": "VPNDemoPassword",
            "route_mode": "policy",
            "status": "up"
        }
    ]
}
```
{: codeblock}

## Quotas

The following list shows the current resource limitations per account:
* Maximum 7 VPN gateways
* Maximum 10 VPN connections per VPN gateway
* Maximum 50 peer subnets across VPN connections on a given VPN gateway
  * Maximum 15 peer subnets on a given VPN connection
* Maximum 50 local subnets across VPN connections on a given VPN gateway
  * Maximum 15 local subnets on a given VPN connection
* Maximum 20 IKE policies
* Maximum 20 IPSec policies

## Policy Auto-negotiation

The use of IKE and IPSec policies to configure a VPN connection is optional.
When no policy is selected, default proposals are chosen automatically for
a process referred to as _auto-negotiation_. The proposals used as part of
auto-negotiation are as follows.

**NOTE:** As an initiator, IBM Cloud uses **IKEv2**. As a responder, IBM Cloud accepts
both **IKEv1** and **IKEv2**.

### IKE Autonegotiation (Phase 1)

|    | Encryption | Authentication | DH Group |
|----|------------|----------------|----------|
| 1  | aes128 | sha1   | 2  |
| 2  | aes128 | sha1   | 5  |
| 3  | aes128 | sha1   | 14 |
| 4  | aes128 | sha256 | 2  |
| 5  | aes128 | sha256 | 5  |
| 6  | aes128 | sha256 | 14 |
| 7  | aes128 | md5    | 2  |
| 8  | aes128 | md5    | 5  |
| 9  | aes128 | md5    | 14 |
| 10 | aes256 | sha1   | 2  |
| 11 | aes256 | sha1   | 5  |
| 12 | aes256 | sha1   | 14 |
| 13 | aes256 | sha256 | 2  |
| 14 | aes256 | sha256 | 5  |
| 15 | aes256 | sha256 | 14 |
| 16 | aes256 | md5    | 2  |
| 17 | aes256 | md5    | 5  |
| 18 | aes256 | md5    | 14 |
| 19 | 3des   | sha1   | 2  |
| 20 | 3des   | sha1   | 5  |
| 21 | 3des   | sha1   | 14 |
| 22 | 3des   | sha256 | 2  |
| 23 | 3des   | sha256 | 5  |
| 24 | 3des   | sha256 | 14 |
| 25 | 3des   | md5    | 2  |
| 26 | 3des   | md5    | 5  |
| 27 | 3des   | md5    | 14 |

### IPsec Autonegotiation (Phase 2)

|    | Encryption | Authentication | DH Group |
|----|------------|----------------|----------|
| 1  | aes128 | sha1   | disabled  |
| 2  | aes128 | sha256 | disabled  |
| 3  | aes128 | md5    | disabled  |
| 4  | aes256 | sha1   | disabled  |
| 5  | aes256 | sha256 | disabled  |
| 6  | aes256 | md5    | disabled  |
| 7  | 3des   | sha1   | disabled  |
| 8  | 3des   | sha256 | disabled  |
| 9  | 3des   | md5    | disabled  |

## FAQ

#### When I create a VPN gateway, can I create VPN connections at the same time?
If you use the API or CLI, VPN connections must be created after the VPN gateway is created. In the IBM Cloud console, you can create the gateway and a connection at the same time.

#### If I delete a VPN gateway that has VPN connections attached, what will happen to the connections?
The VPN connections are deleted along with the VPN gateway.

#### Will IKE or IPSec policies be deleted if I delete a VPN gateway or VPN connection?
No, IKE and IPSec policies can apply to multiple connections.

#### What will happen to a VPN gateway if I try to delete the subnet that the gateway is located on?
The subnet cannot be deleted if any instances are present, including the VPN gateway.

#### Are there default IKE and IPSec policies?
When you create a VPN connection without referencing a policy ID (IKE or IPSec), auto-negotiation is used.
