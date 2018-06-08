---

copyright:
  years: 2018

lastupdated: "2018-06-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Using Security Groups in VPC Beta

Security groups give you a convenient way to apply rules that establish filtering to each network interface of a virtual server instance (VSI), based on IP address.

By default, a security group denies all traffic. As rules are added to a security group, it defines the traffic that the security group permits. 

Rules are _stateful_, which means that reverse traffic in response to allowed traffic is automatically permitted. So for example, a rule allowing inbound TCP traffic on port 80 also allows replying outbound TCP traffic on port 80 back to the originating host, without the need for an additional rule.

Security groups are scoped to a single VPC. This scoping implies that security group can be attached _only_ to network interfaces of VSIs within the same VPC.

When a VSI is created without any security groups specified, the VSI's primary network interface is put into the _default_ security group of that VSI's VPC. IBM Cloud VPC Beta release has a defined default security group that does allow certain traffic.

### Default Security Groups

Each VPC has a default group, with rules to allow:

* Inbound traffic from all other members of the group.
* Outbound traffic from all other members of the group.
* Inbound SSH traffic from everywhere.
* Inbound ping traffic from everywhere.

If you edit the rules of the default security group, those edited rules will then apply to all current and future servers in the group.

**Note:** Because Security Groups are not currently editable in the IBM Console UI, rule modifications to the default security group must be made using the REST API, or the experimental `ibmcloud cli`, for example:

```
# Add rules allowing SSH and PING
ibmcloud is sg-rule-add --direction ingress --protocol tcp --ipv 4 --min-port 22 --max-port 22 634533 
ibmcloud is sg-rule-add --direction ingress --protocol icmp --icmp-type 8 --icmp-code 0 634533
```

## APIs and CLIs currently available

These endpoints can be used to manage a VPC's default security group.

| Description | API | CLI |
|-------------|-----|-----|
|Retrieve a single security group specified by the identifier in the URL path. | GET /security_groups/{id}| `ibmcloud is security-group`, `sg`|
|Update a security group with the information provided in a security group patch object. The security group patch object is structured in the same way as a retrieved security group. It contains only the information to be updated. | PATCH /security_groups/{id}| `ibmcloud is security-group-update`, `sgu`|
|Retrieve all the rules for a particular security group. | GET /security_groups/{security_group_id}/rules| `ibmcloud is security-group-rules`, `sg-rules`|
|Retrieve a single security group rule specified by the identifier in the URL path. | GET /security_groups/{security_group_id}/rules/{id}| `ibmcloud is security-group-rule`, `sg-rule`|
|Create a new security group rule from a security group rule template. The rule template object is structured in the same way as a retrieved security group rule. It contains the information necessary to create the rule. The rule is applied to all the networking interfaces in the security group. | POST /security_groups/{security_group_id}/rules| `ibmcloud is security-group-rule-add`, `sg-rulec`|
|Update a security group rule with the information provided in a rule patch object. The patch object is structured in the same way as a retrieved security group rule. It should contain only the information to be updated. | PATCH /security_groups/{security_group_id}/rules/{id}| |
|Delete a security group rule. This deletion does not terminate any existing connections that were allowed by that rule. This operation cannot be reversed. | DELETE /security_groups/{security_group_id}/rules/{id}| `ibmcloud is security-group-rule-delete`, `sg-ruled`|

### Limitations of the current Beta release:

 * Security groups currently are not editable using the UI.

 * The PATCH operation on a security group rule cannot modify the rule's protocol.

## APIs and CLIs experimentally available in this Beta release

The following endpoints are available in this release. Until the 'GET network interfaces' command is released, it's hard to get feedback on their operation, so they are not supported.

| Description | API | CLI |
|-------------|-----|-----|
|Create a server, with the specified existing security groups attached to the server's network interfaces. |POST /servers (with security group parameters)| `ibmcloud is server-create` |
|Retrieve all this account's existing security groups|GET /security_groups| `ibmcloud is security-groups`, `sgs`|
|Create a new security group from a security group template. The template is structured in the same way as a retrieved security group. It contains the information necessary to create the new security group. The template may include an optional array of security group rules, which will be added to the group. | POST /security_groups| `ibmcloud is security-group-create`, `sgc`|
|Delete a security group. A security group cannot be deleted if any other security groups contain rules that refer to it as a remote. This operation cannot be reversed. | DELETE /security_groups/{id}| `ibmcloud is security-group-delete`, `sgd`|
|Add an server's existing network interface to an existing security group. This function applies the group's rules to that interface, allowing new connections to be made, to and from the interface, that conform to those rules.<br /><br />In addition, this network interface is now granted the access specified by the rules of any remote groups that refer to this group.<br /><br />See Limitations, below.  | PUT /security_groups/{security_group_id}/network_interfaces/{id}| `ibmcloud is security-group-network-interface-add`, `sg-nica`|
|Remove a server's network interface from a security group. The group's rules are no longer used to permit new network connections on that interface. <br /><br />In addition, this network interface is no longer granted the access specified by the rules of any remote groups that refer to this group. <br /><br />Existing connections that were permitted by membership of this group are not ended.| DELETE /security_groups/{security_group_id}/network_interfaces/{id}| `ibmcloud is security-group-network-interface-remove`, `sg-nicd`|

### Limitations of experimental features

 * Default security groups are available for VPCs created after May 24 only.

 * Adding or removing network interfaces from a security group works for network interfaces on servers ordered after May 19 only.

 * Although network interfaces added to a security group should be functional, you are not able to view them through the API, until the "GET network interfaces" functionality is available (**coming soon**).

## APIs and CLIs coming soon in this Beta release

| Description | API | CLI |
|-------------|-----|-----|
|Retrieve all the the network interfaces associated with the security group. These are the network interfaces to which the rules in the group are applied. | GET /security_groups/{security_group_id}/network_interfaces| `ibmcloud is security-group-network-interfaces`, `sg-nics`|
|Retrieve a single network interface specified by the identifier in the URL path. The network interface must be an existing member of the security group. | GET /security_groups/{security_group_id}/network_interfaces/{id}| `ibmcloud is security-group-network-interface`, `sg-nic`

## Security groups demo example

In the example that follows, you'll create a VSI with a security group enabled, using the command line interface (CLI). Here's what the scenario looks like.

![image3](/images/security-groups-demo-schematic.png)

Notice in the figure that the VSI named **SG4** has a floating IP `169.60.208.144` assigned to it, in addition to its internal VPC address `10.0.0.5`; therefore, it can talk to the public internet. The security group assigned to VSI **SG4** is named "demosg".

The VSI named **SG8** is internal-only to the VPC, with a private IP address. The security group assigned to VSI **SG8** is named "my_vpc_sg". Both of these VSIs exist within the VPC named `sgvpc` and also on the same subnet `10.0.0.0/28` so they can communicate with each other. For the internal Beta release, it is a limitation that the security groups for these VSIs cannot be deleted once the VSI has been created with an attached security group, but the security group rules can be modified at will.

## Example code

The example code that follows shows how to set up the security group rules for "my_vpc_sg" to include basic functions of SSH, PING, and outbound TCP.

Notice that you must create the security group first, with the `ibmcloud is sg-create` command, and then create the VSI that will include this newly-created security group. Essentially, you will just add a parameter at the end of your VSI creation command, which specifies the ID of the security group (that you just created). In the example below, the security group ID is `581969`.

This example code skips a few steps, so here's where you can find more information:

 * If you're new to the VPC Beta release, the procedure for how to log in is included in [another file](sl-2-factor-auth.html#how-to-use-2-factor-authentication-for-softlayer-initialization-with-ibm-cloud-vpc).

 * Instructions for creating a VPC and a subnet are available in our [example code document](example-code.html#example-code-tutorial).

You can copy and paste commands from this example CLI code to get you started creating a VSI that has a security group attached. System responses are not shown completely in this sample code. You'll need to update your commands with the correct resource IDs for your _VPC_, _subnet_, _image_, and _key_, and the correct _security group ID number_.

**Step 1. Log in**

```
ibmcloud login -sso
ibmcloud sl init
```
{: codeblock}

**Step 2. Choose how to configure IBM Cloud Infrastructure (Softlayer) authentication:**

1. Login with your Softlayer user name and password or API key

2. Use Bluemix Single-Sign-On

```
Enter a number> 2                                             # choose option 2
API endpoint URL: [https://api.softlayer.com/mobile/v3.1]>    # make sure this is your API endpoint
```

**Step 3. Create Security Group “my_vpc_sg”**

```
ibmcloud is sg-create --name my_vpc_sg --vpc e636a5de-391d-456d-badb-9a9570259a51
```
{: codeblock}

The response includes your newly created SG ID: **581969** (in this case, yours may differ)

**Step 4. Add rules allowing SSH, PING, and outbound TCP**

```
ibmcloud is sg-rule-add --direction ingress --protocol tcp --ipv 4 --min-port 22 --max-port 22 581969
ibmcloud is sg-rule-add --direction ingress --protocol icmp --icmp-type 8 --icmp-code 0 581969
ibmcloud is sg-rule-add --direction egress --protocol tcp
```
{: codeblock}

**Step 5. Create VSI with newly created SG**

```
ibmcloud is server-create --name sg8 --gen gc --type virtual --subnet 42e0789f-ee21-42b5-a448-37e4f6302ef6 --zone us-south-1 --vpc e636a5de-391d-456d-badb-9a9570259a51 --flavor B1_1X2X25 --image cc8debe0-1b30-6e37-2e13-744bfb2a0c11 --key 51ddf6e5-d717-4202-a242-82612b2864fd --port 100 --sec-group 581969
```
{: codeblock}

## Command list cheat sheet

For a complete list of the available VPC CLI commands for security groups, type:

```
ibmcloud is help | grep sg
```

To see your security group and its metadata including rules, you'd type (for the previous example):

```
ibmcloud is sg-get 581969
```

**Note:** For the general case, substitute the correct security group ID for your own VSI's security group.

To add a security group rule, here's an example command for adding a PING ingress rule to a security group with ID 569403:

```
ibmcloud is sg-rule-add --direction ingress --protocol icmp --icmp-type 8 --icmp-code 0 569403
```
{: codeblock}

