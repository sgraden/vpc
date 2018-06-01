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

# Example Code Tutorial

The following example will help you create an IBM Cloud VPC, a subnet, a gateway, a server, and associate a floating IP address, using the IBM CLoud VPC (Beta) REST APIs.

## Verify access to the Regional APIs

Get an IAM token, an IMS token, source your variables, and verify that you have access to the Regional APIs (RIAS) by following these [instructions](how-to-verify-access.html) first. 

If you run into unexpected results, add the `--verbose` (debug) flag after the `curl` command to obtain detailed logging information. You also can check out the commonly encountered errors in our [troubleshooting page](troubleshooting.html).

If you are using 2-factor authentication, you may wish to refer to [this guide](sl-2-factor-auth.html) for more information.

## List your Virtual Private Clouds

Call the `List VPC` API to list any IBM Cloud VPCs that you have.

```bash
curl $rias_endpoint/v1/vpcs \
  -u $credentials \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

## Create a Virtual Private Cloud

Create an IBM Cloud VPC called `my-vpc`.

```bash
curl $rias_endpoint/v1/vpcs \
  -u $credentials \
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

Create a subnet in your IBM Cloud VPC. For example, let's put it in the `us-south-1` zone.

```bash
curl -X POST $rias_endpoint/v1/subnets \
  -u $credentials \
  -H "X-Auth-Token:$iam_token" \
  -d '{
        "name": "my-subnet",
        "ipv4_cidr_block": "10.0.1.0/24",
        "zone": { "name": "us-south-1" },
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

## Create a Public Gateway

To allow servers in the subnet to have access to the public internet, add a public gateway (PGW) to the IBM Cloud VPC in each zone.  

```bash
curl -X POST $rias_endpoint/v1/public_gateways \
  -u $credentials \
  -H "X-Auth-Token:$iam_token" \
  -d '{
        "name": "my-gateway",
        "zone": { "name": "us-south-1" },
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

Create a key with your public SSH key. This key is used during creation of the server, also for logging into the server.

```bash
curl -X POST $rias_endpoint/v1/keys \
  -u $credentials \
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

## Choose a Flavor and Image for your Server

Run the APIs to list all flavor and images available for your server, and choose a combination.

```
curl $rias_endpoint/v1/flavors -u $credentials -H "X-Auth-Token:$iam_token"
```
{: codeblock}

```
curl $rias_endpoint/v1/images -u $credentials -H "X-Auth-Token:$iam_token"
```
{: codeblock}

Save the ID of the Image and Name of the Flavor in variables to be used later to create a server.

```bash
# Something like this: `image_id="660198a6-52c6-21cd-7b57-e37917cef586"`
image_id="<CHOSEN_IMAGE_ID>"
# Something like this: `flavor_name="B1_2X4X100"`
flavor_name="<CHOSEN_FLAVOR_NAME>"
```
{: codeblock}


## Create a Server

Create a server in the newly created subnet. Pass in your public SSH key so that you can log in after it is created. For this step in the procedure, the formatting of `echo $ims_subject` is critical. 
 * Make sure the values are filled in for _token_, _account_,and  _user_. 
 * Make sure the endpoint is set to `https://api.softlayer.com/mobile/v3.1`. 
 * Also make sure the single and double quotes are ones the terminal can parse. 

Here's an example `ims_subject`:

```
{"ims":{"token":"9a369f767fbc2287ad97b400fa226dfaf6f78aa77bbf4f8cdd6be1430f18959f79fcee68dbd1776dea8ecbc954a14c2c591429b67ef89aa68bf03121bf9a8abcb20b1c4e309e747bd9c8e1745684764a5add37c152d15766b37cef0f4ea636d3b0843939839a9b567f0cf436056d746f9cb63698e1d386080c93899aa2189f5e2c31b0f822934ad801de4458cfda954d24db5026299db92876d69a369f767fbc","account":1511647,"user":6938775,"endpoint":"https://api.softlayer.com/mobile/v3.1","username":""},"land":{}}
```

If the `ims_subject` is not formatted correctly, the server will appear to have been created successfully, but it will show a status of `failed` shortly thereafter.


```bash
curl -X POST $rias_endpoint/v1/servers \
  -u $credentials \
  -H "X-Auth-Token:$iam_token" -H "X-Subject-Token:$ims_subject" \
  -d '{
        "name": "server-1",
        "type": "virtual",
        "zone": {
          "name": "us-south-1"
        },
        "vpc": {
          "id": "'$vpc'"
        },
        "primary_network_interface": {
          "port_speed": 10000,
          "subnet": {
            "id": "'$subnet'"
          }
        },
        "keys":[{"id": "'$key'"}],
        "flavor": {
          "name": "'$flavor_name'"
         },
        "image": {
          "id": "'$image_id'"
         },
        "userdata": ""
      }'
```
{: codeblock}

As you did with the other resources, save the ID of the server in a variable.

```bash
# Something like this: `server="35fb0489-7105-41b9-99de-033fae723006"`
server="<YOUR_SERVER_ID"
```
{: codeblock}

Also save the ID of the primary network interface of the server.

```bash
# Something like this: `network_interface="7710e766-dd6e-41ef-9d36-06f7adbef33d"`
network_interface="<YOUR_NETWORK_INTERFACE_ID"
```
{: codeblock}

## Create a Floating IP

Create a floating IP for the server using the server's primary network interface as the target for the new floating IP.

```bash
curl -X POST $rias_endpoint/v1/floating_ips \
  -u $credentials \
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

## Check whether your Server is available

Check the status of your server by listing your server and seeing the status value. 

```bash
curl -X GET $rias_endpoint/v1/servers/$server \
  -u $credentials \
  -H "X-Auth-Token:$iam_token" -H "X-Subject-Token:$ims_subject" 
```
{: codeblock}

A status of `running` means that the server is available for you to log in. To SSH to the server, use the `address` of the Floating IP you created. To get the Floating IP, run the following command:

```bash
curl -X GET $rias_endpoint/v1/floating_ips/$floating_ip \
  -u $credentials \
  -H "X-Auth-Token:$iam_token" -H "X-Subject-Token:$ims_subject" 
```
{: codeblock}


## Delete the Resources

Delete the resources if desired. A resource cannot be deleted if it contains other resources, for example, a Virtual Private Cloud cannot be deleted if it contains subnets and a subnet cannot be deleted if it contains Servers.

### Delete the floating IP.

```bash
curl -X DELETE $rias_endpoint/v1/floating_ips/$floating_ip \
  -u $credentials \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

### Delete the server.

```bash
curl -X DELETE $rias_endpoint/v1/servers/$server \
  -u $credentials \
  -H "X-Auth-Token:$iam_token" -H "X-Subject-Token:$ims_subject" 
```
{: codeblock}

### Delete the key.

```bash
curl -X DELETE $rias_endpoint/v1/keys/$key \
  -u $credentials \
  -H "X-Auth-Token: $iam_token" -H "X-Subject-Token:$ims_subject" 
```
{: codeblock}


### Delete the public gateway.

```bash
curl -X DELETE $rias_endpoint/v1/public_gateways/$gateway \
  -u $credentials \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

### Delete the subnet.

```bash
curl -X DELETE $rias_endpoint/v1/subnets/$subnet \
  -u $credentials \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

### Delete the VPC.

```bash
curl -X DELETE $rias_endpoint/v1/vpcs/$vpc \
  -u $credentials \
  -H "X-Auth-Token:$iam_token"
```
{: codeblock}

## Ready for more?

Check out the [API Reference](apis.html).


