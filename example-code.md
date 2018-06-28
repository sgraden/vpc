---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Example Code Tutorial

The following example helps you create an IBM Cloud VPC, a subnet, a gateway, a virtual server instance, and then to associate a floating IP address, using the IBM Cloud VPC (Beta) REST APIs.

## Verify access to the Regional APIs

Get an IAM token, source your variables, and verify that you have access to the Regional APIs (RIAS) by following these [instructions](how-to-verify-access.html) first. 

If you run into unexpected results, add the `--verbose` (debug) flag after the `curl` command to obtain detailed logging information. You also can check out the commonly encountered errors in our [troubleshooting page](troubleshooting.html).

If you are using 2-factor authentication, you may wish to refer to [this guide](sl-2-factor-auth.html) for more information.

## List your Virtual Private Clouds

Call the `List VPC` API to list any IBM Cloud VPCs that you have.

```bash
curl $rias_endpoint/v1/vpcs \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

## Create a Virtual Private Cloud

Create an IBM Cloud VPC called `my-vpc`.

```bash
curl $rias_endpoint/v1/vpcs \
  -H "X-Auth-Token:$iam_token" \
  -d '{
      	"is_default": true,
      	"name": "my-vpc"
      }'
```
{: codeblock}

For the rest of the calls, you'll need to know the ID of the newly created IBM Cloud VPC. Paste its ID into the variable, as shown:

```bash
# Something like this: `vpc="35fb0489-7105-41b9-99de-033fae723006"`
vpc="<YOUR_VPC_ID>"
```
{: codeblock}

## Create a Subnet

Create a subnet in your IBM Cloud VPC. For example, let's put it in the `us-south-2` zone.

```bash
curl -X POST $rias_endpoint/v1/subnets \
  -H "X-Auth-Token:$iam_token" \
  -d '{
        "name": "my-subnet",
        "ipv4_cidr_block": "10.0.1.0/24",
        "zone": { "name": "us-south-2" },
        "vpc": { "id": "'$vpc'" }
      }'
```
{: codeblock}

As with the Virtual Private Cloud, save the ID of the subnet in a variable.

```bash
# Something like this: `subnet="35fb0489-7105-41b9-99de-033fae723006"`
subnet="<YOUR_SUBNET_ID"
```
{: codeblock}

## Check the Status of your Subnet

To provision resources in your subnet, the subnet must be in `available` status. Query the subnet resource and make sure the status is `available` before you continue. If the status is `failed`, contact [support](getting-help.html) with the details. You can attempt to continue by trying to provision another subnet. 

```bash
curl $rias_endpoint/v1/subnets/$subnet -H "X-Auth-Token: $iam_token"
```
{: codeblock}


## Create a Public Gateway

To allow virtual server instances in the subnet to have access to the public internet, add a public gateway (PGW) to the subnet.  

```bash
curl -X POST $rias_endpoint/v1/public_gateways \
  -H "X-Auth-Token:$iam_token" \
  -d '{
        "name": "my-gateway",
        "zone": { "name": "us-south-2" },
        "vpc": { "id": "'$vpc'" }
      }'
```
{: codeblock}

As you did with the Virtual Private Cloud and the subnet, save the ID of the public gateway in a variable.

```bash
# Something like this: `gateway="35fb0489-7105-41b9-99de-033fae723006"`
gateway="<YOUR_GATEWAY_ID"
```
{: codeblock}


## Create an SSH Key

Create a key with your public SSH key. This key is used when creating the virtual server instance, and it is needed to log into the virtual server instance.

```bash
curl -X POST $rias_endpoint/v1/keys \
  -H "X-Auth-Token:$iam_token" \
  -d '{
        "name": "my-key",
        "public_key": "ssh-rsa AAA....n",
        "type": "rsa"
      }'
```
{: codeblock}

Save the ID of the key in a variable.

```bash
# Something like this: `key="35fb0489-7105-41b9-8764-033fae723006"`
key="<YOUR_KEY_ID>"
```
{: codeblock}

## Choose a Profile and Image for your Virtual Server Instance

Run the APIs to list all profiles and images available for your virtual server instance, and choose a combination.

```
curl $rias_endpoint/v1/instance/profiles -H "X-Auth-Token:$iam_token"
```
{: codeblock}

To get additional details about the profiles, you can query the global catalog using the IBM Cloud CLI command `ibmcloud catalog entry <profile-name> --json`. For example, 

```
ibmcloud catalog entry b-2x8 --json
```
{: codeblock}

```
curl $rias_endpoint/v1/images -H "X-Auth-Token:$iam_token"
```
{: codeblock}

Save the Name of the profile and the ID of the image in variables, which will be used later to provision a virtual server instance.

```bash
# Something like this: `profile_name="b1-2x4"`
profile_name="<CHOSEN_PROFILE_NAME>"
# Something like this: `image_id="660198a6-52c6-21cd-7b57-e37917cef586"`
image_id="<CHOSEN_IMAGE_ID>"
```
{: codeblock}


## Provision a Virtual Server Instance

Provision a virtual server instance in the newly created subnet. Pass in your public SSH key so that you can log in after the instance is provisioned. 

```bash
curl -X POST $rias_endpoint/v1/instances \
  -H "X-Auth-Token:$iam_token" \
  -d '{
        "name": "server-1",
        "type": "virtual",
        "zone": {
          "name": "us-south-2"
        },
        "vpc": {
          "id": "'$vpc'"
        },
        "primary_network_interface": {
          "port_speed": 1000,
          "subnet": {
            "id": "'$subnet'"
          }
        },
        "keys":[{"id": "'$key'"}],
        "profile": {
          "name": "'$profile_name'"
         },
        "image": {
          "id": "'$image_id'"
         },
        "userdata": ""
      }'
```
{: codeblock}

As you did with the other resources, save the ID of the virtual server instance in a variable.

```bash
# Something like this: `server="35fb0489-7105-41b9-99de-033fae723006"`
server="<YOUR_SERVER_ID"
```
{: codeblock}

Also save the ID of the primary network interface of the virtual server instance.

```bash
# Something like this: `network_interface="7710e766-dd6e-41ef-9d36-06f7adbef33d"`
network_interface="<YOUR_NETWORK_INTERFACE_ID"
```
{: codeblock}

You can find more information, including examples about how to provision a VSI with security groups, in our [Security Group Usage Examples document](security-groups-usage-examples.html).

## Check the Status of your Virtual Server Instance

Provisioning a Virtual Server Instance may take several seconds to a few minutes. Before continuing, query the status of the server and make sure it is `running`.

```bash
curl $rias_endpoint/v1/instances/$server -H "X-Auth-Token: $iam_token"
```
{: codeblock}

## Create a Floating IP

Create a floating IP for the virtual server instance, by using the instance's primary network interface as the target for the new floating IP address.

```bash
curl -X POST $rias_endpoint/v1/floating_ips \
  -H "X-Auth-Token:$iam_token" \
  -d '{
        "name": "my-server-floatingip",
        "target": {
            "id":"'$network_interface'"
        }
      }
'
```
{: codeblock}


Save the ID of the floating IP.

```bash
# Something like this: `floating_ip="35fb0489-7105-41b9-99de-033fae723006"`
floating_ip="<YOUR_FLOATING_IP_ID>"
```
{: codeblock}

## SSH into your Virtual Server Instance

To SSH to the server, use the `address` of the Floating IP you created. To get the `address` of the Floating IP, run the following command:

```bash
curl -X GET $rias_endpoint/v1/floating_ips/$floating_ip \
  -H "X-Auth-Token:$iam_token" 
```
{: codeblock}

Use the `address` of the Floating IP to connect to the virtual server instance with SSH:

```ssh -i <private_key_file> root@<floating ip address>```


## Delete the Resources

Delete the resources if desired. A resource cannot be deleted if it contains other resources. For example, a Virtual Private Cloud cannot be deleted if it contains subnets, and a subnet cannot be deleted if it contains virtual server instances.

### Delete the floating IP.

```bash
curl -X DELETE $rias_endpoint/v1/floating_ips/$floating_ip \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

### Delete the virtual server instance.

```bash
curl -X DELETE $rias_endpoint/v1/instances/$server \
  -H "X-Auth-Token:$iam_token" 
```
{: codeblock}

### Delete the key.

```bash
curl -X DELETE $rias_endpoint/v1/keys/$key \
  -H "X-Auth-Token: $iam_token" 
```
{: codeblock}


### Delete the public gateway.

```bash
curl -X DELETE $rias_endpoint/v1/public_gateways/$gateway \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

### Delete the subnet.

```bash
curl -X DELETE $rias_endpoint/v1/subnets/$subnet \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

### Delete the VPC.

```bash
curl -X DELETE $rias_endpoint/v1/vpcs/$vpc \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

## Ready for more?

Check out the [API Reference](apis.html).


