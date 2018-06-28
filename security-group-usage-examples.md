---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Security Group Usage Examples

The following examples demonstrate how to create and manage security groups, using the IBM Cloud VPC (Beta) REST APIs.


## Prerequisites

In order to use security groups you must first have a valid IBM Cloud VPC.

For the rest of these examples, you'll need to know the ID of your IBM Cloud VPC. Paste its ID into a variable, as shown:

```bash
# Something like this: `vpc="35fb0489-7105-41b9-99de-033fae723006"`
vpc="<YOUR_VPC_ID>"
```
{: codeblock}


## Create Security Group

Create a security group named `my-security-group` in your IBM Cloud VPC.

```bash
curl -X POST $rias_endpoint/v1/security_groups \
  -H "X-Auth-Token: $iam_token" \
  -d '{
        "name": "my-security-group",
        "vpc": { "id": "'$vpc'" }
      }'
```
{: codeblock}

Similar to the VPC, save off the security group ID in a variable.
```bash
# Something like this: `security_group="35fb0489-7105-41b9-99de-033fae723006"`
security_group="<YOUR_SECURITY_GROUP_ID>"
```
{: codeblock}


## Add an allow SSH Rule

Create a rule on the security group that will allow inbound connections on port 22.

```bash
curl -X POST $rias_endpoint/v1/security_groups/$security_group/rules \
  -H "X-Auth-Token: $iam_token" \
  -d '{
        "direction": "ingress",
        "protocol": "tcp",
        "port_min": 22,
        "port_max": 22
      }'
```


## Delete Security Group

To clean up the security group, it cannot be associated with any network interfaces, or be referenced by a rule in a different security group.

```bash
curl -X DELETE $rias_endpoint/v1/security_groups/$security_group \
  -H "X-Auth-Token: $iam_token"
```
