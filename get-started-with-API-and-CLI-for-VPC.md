---

copyright:
  years: 2018
lastupdated: "2018-07-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Getting started with the API and CLI for VPC

{{site.data.keyword.cloud}} Virtual Private Cloud (VPC) functionality is available through the IBM Console UI, IBM Cloud CLI, and REST API. For the Beta release, accounts must be granted access before the functionality is available. See [How to Participate](how-to-participate.html) for the steps of how to be added to the Beta release.

To manage VPC resources and instantiate Virtual Server Instances (VSIs), first review each user's [permissions](vpc-user-permissions.html).

To learn how to use the IBM Console UI to manage VPC resources, follow the steps in our [UI guide](console-tutorial.html).

To use the CLI and API, follow the steps below.

## Pre-requisites:

1. Install the [IBM Cloud CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}.

2. [Create an API Key ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/iam/userid_keys.html#creating-an-api-key ){: new_window}.


## Processes:

1. Install the infrastructure-services plugin for CLI

1. Generate IAM token

1. Get API access and run cURL commands


## Process 1: Setup the infrastructure-services plugin for CLI

The VPC CLI actions use the extension `is`.

### Step 1: Install or update the VPC Plugin to the IBM Cloud CLI.

```
ibmcloud plugin install infrastructure-service
```
{: codeblock}

Or to update:

```
ibmcloud plugin update
```
{: codeblock}

To view installed plugins and versions:

```
ibmcloud plugin list
```
{: codeblock}

### Step 2: Log in to IBM Cloud.

If you have a federated account:
```
ibmcloud login -sso
```
{: codeblock}

otherwise
```
ibmcloud login
```
{: codeblock}

### Step 3: To learn how to use the commands, you can run:

```
ibmcloud is help <Command name>
```

### Step 4: Start running VPC CLI commands!

```
ibmcloud is regions
ibmcloud is zones _region-name_ (For example, _us-south_)
ibmcloud is instances --json
```

For more details on CLI capability, see:

- [Network CLI](cli-reference.html#network)
- [Compute CLI](cli-reference.html#compute)
- [Regions and Zones CLI](cli-reference.html#geography)


## Process 2: Generate an IAM token

```
iam_token=$(ibmcloud iam oauth-tokens | awk '/IAM/{ print $4; }')
```
{: codeblock}

This command calls the IBM Cloud CLI, parses out the IAM token, and stores it in a variable you can use in later commands. To view your IAM token, run the command ``echo $iam_token``.

**Note that you must repeat the preceding step to refresh your IAM token every hour, because the token expires.**


## Process 3: Get API access and run cURL commands

Once your account has been granted access, you will receive an email with the API endpoint. The following steps take you through a simple example using cURL, if you are ready to get more advanced, follow more advanced [sample code](example-code.html).

**NOTE:** add ``` | json_pp ``` after curl command to get readable JSON string

### Step 1: Login into the CLI (See above) <Hotlink to anchor above?>

### Step 2: Get an IBM Identity and Access Management (IAM) token and store it
```
iam_token=$(ibmcloud iam oauth-tokens | awk '/IAM/{ print $4; }')
```
{: codeblock}

This command calls the IBM Cloud CLI, parses out the IAM token, and stores it in a variable you can use in later commands. To view your IAM token, run the command ``echo $iam_token``.

**Note that you must repeat the preceding step to refresh your IAM token every hour, because the token expires.**

### Step 3: Store the endpoint
For `rias_endpoint`, use the API endpoint given to you during on-boarding.

```
rias_endpoint="<RIAS_API_ENDPOINT>"
 ```
{: codeblock}

Run the previous command to store the value as a variable in your session. To verify that this variable was saved, run ``echo $rias_endpoint`` and make sure the response is not empty.


### Step 4: Run a couple commands using the stored variables

#### GET Regions API
```
curl $rias_endpoint/v1/regions -H "X-Auth-Token: $iam_token"
```
{: codeblock}

The previous command returns the regions available for VPC, in JSON format. At least one object should return.

### GET Zone API
Note that currently, there is only one region `us-south` available.

```
curl $rias_endpoint/v1/regions/us-south/zones -H "X-Auth-Token: $iam_token"
```
{: codeblock}

The previous command returns the zones available for VPC in region `us-south`, in JSON format. At least one object should return.


#### Create VPC API
Create an IBM Cloud VPC called `my-vpc`.

```bash
curl -X POST $rias_endpoint/v1/vpcs \
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

#### Create Subnet API
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
subnet="<YOUR_SUBNET_ID>"
```
{: codeblock}


## What Happens Next

Success! You are ready to move on to more advanced API and CLI usage. Check out more [sample code](example-code.html). To see the complete list of available APIs, see [API Reference](apis.html).

