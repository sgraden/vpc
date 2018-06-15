---

copyright:
  years: 2018
lastupdated: "2018-06-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Verifying your IBM Cloud VPC Access for the Beta release

IBM Virtual Private Cloud (VPC) functionality is available through the IBM Console UI, IBM Cloud CLI, and REST API. For the Beta release, accounts must be granted access before the functionality is available. See [Getting Started](getting-started.html) for the steps of how to be added.

To manage VPC resources and instantiate Virtual Server Instances (VSIs), review each user's [permissions](vpc-user-permissions.html).

To learn how to use the IBM Console UI to manage VPC resources, follow the steps in our [UI guide](console-tutorial.html).

To use the CLI and API, follow the steps below.

## Pre-requisites:

1. Install the [IBM Cloud CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}.
2. Generate a public SSH key to provision Virtual Server Instances (VSIs).

You may have a public SSH key already. Look for a file called ``id_rsa.pub`` under an ``.ssh`` directory under your home directory, for example, ``/Users/<USERNAME>/.ssh/id_rsa.pub``. The file starts with ``ssh-rsa`` and ends with your email address.

If you do not have a public SSH key or if you forgot the password of an existing one, generate a new one by running the ``ssh-keygen`` command and following the prompts.

## CLI Access

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

### Step 2: Log in to IBM Cloud.
    
```
ibmcloud login -sso
ibmcloud sl init
```

### Step 3: To learn how to use the commands, you can run:
    
```
ibmcloud is help
ibmcloud is help vpc-create
ibmcloud is help server-create
```

### Step 4: Start running VPC CLIs!
    
```
ibmcloud is vpcs
ibmcloud is subnets
ibmcloud is servers
ibmcloud is servers --json
```

For more details on CLI capability, see:

- [Network APIs](cli-network-reference.html)
- [Compute APIs](cli-compute-reference.html)

## API Access 

Once your account has been granted access, you will receive an email with the API endpoint. The following steps take you through a simple example using cURL, if you are ready to get more advanced, follow more advanced [sample code](example-code.html).

### Step 1: Log in to IBM Cloud.

```
ibmcloud login --sso
 ```
{: codeblock}

This command returns a URL and prompts for a passcode. Go to that URL in your browser and log in. If successful, you will get a one-time passcode. Copy this passcode and paste it as a response on the prompt. After the authentication steps, you'll be prompted to choose an account. Choose the account that was granted access to participate in the Beta. Respond to any remaining prompts to finish logging in.

### Step 2: Get an IBM Identity and Access Management (IAM) Token 

```
iam_token=$(ibmcloud iam oauth-tokens | awk '/IAM/{ print $4; }')
```
{: codeblock}

This command calls the IBM Cloud CLI, parses out the IAM token, and stores it in a variable you can use in later commands. To view your IAM token, run the command ``echo $iam_token``.

**Note that you must repeat the preceding step to refresh your IAM token every hour, because the token expires.**

### Step 3: Store Endpoint and Credentials as Variables

For `rias_endpoint`, use the API endpoint given to you during onboarding.

```
rias_endpoint="<RIAS_API_ENDPOINT>"
 ```
{: codeblock}

Run the previous command to store the value as a variable in your session. To verify that this variable was saved, run ``echo $rias_endpoint`` and make sure the response is not empty.

### Step 4: Run the GET Regions API

```
curl $rias_endpoint/v1/regions -H "X-Auth-Token: $iam_token"
```
{: codeblock}

The previous command returns the regions available for VPC, in JSON format. At least one object should return. 

### Step 5: Run the GET Flavors API

```
curl $rias_endpoint/v1/flavors -H "X-Auth-Token: $iam_token"
```
{: codeblock}

The previous command returns the flavors available for your VSIs, in JSON format. At least one object should return.

### Step 7: Run the GET Images API

```
curl $rias_endpoint/v1/images -H "X-Auth-Token: $iam_token"
```
{: codeblock}

The previous command returns the images available for your VSIs, in JSON format. At least one object should return.

### Step 7: Run the GET VPCs API

```
curl $rias_endpoint/v1/vpcs -H "X-Auth-Token: $iam_token"
```
{: codeblock}

The previous command returns the VPCs that have been created under your account (if any), in JSON format. 

## What Happens Next

Success! You are ready to move on to more advanced APIs. Check out more [sample code](example-code.html). To see the complete list of available APIs, see [API Reference](apis.html).
