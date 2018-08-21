---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Getting started with IBM Cloud Virtual Private Cloud Beta release

Create an {{site.data.keyword.cloud}} Virtual Private Cloud through the [IBM Console ![External link icon](../../icons/launch-glyph.svg "External link icon")]( https://console.bluemix.net/is), the [IBM Cloud command line interface](cli-reference.html), or via [VPC REST APIs](apis.html).

Whichever interface method you may choose, here's the minimum required steps to get going:

1. Create a Virtual Private Cloud.
2. Create one or more subnets in the Virtual Private Cloud in one or more zones.
4. Select the profiles of virtual server instances (VSIs) you'd like to run, and instantiate them.
6. Reserve a Floating IP address, and associate it with a virtual server instance.
7. Create a public gateway (PGW) if you want public internet traffic to your subnet.
9. Deploy your service or applications across the virtual server instances.

## Pre-requisites:

 * **Account Access**: Access to IBM Cloud Virtual Private Cloud currently is limited and requires approval. Agree to the conditions and see [How to Participate in the IBM Cloud Virtual Private Cloud Beta Release](how-to-participate.html).

 * **User Permissions**: Be sure that your user has sufficient permissions to create and manage resources in your VPC. For a list of required permissions, see [Granting permissions needed for VPC users](vpc-user-permissions.html).

 * **Have your SSH key ready**: You will use an SSH key to connect to your virtual server instance(s).

   * Look for a file called `id_rsa.pub` under an `.ssh` directory under your home directory, for example, `/Users/<USERNAME>/.ssh/id_rsa.pub`. The file starts with `ssh-rsa` and ends with your email address.

   * Or Generate an SSH Key: If you do not have a public SSH key or if you forgot the password of an existing one, generate a new one by running the `ssh-keygen` command and following the prompts. For example, you can generate an SSH key on your Linux server by running the command `ssh-keygen -t rsa -C "user_ID"`. That command generates two files. The generated public key is in the `<your key>.pub` file.

* **Download the IBM Cloud CLI and install the infrastructure plugin to use the CLI**: If you plan to use the `ibmcloud` CLI, you need to [download it and install the infrastructure plugin](cli-reference.html).

* **API endpoint**: For REST API access, the account owner should have received the API endpoint during on-boarding. Check out our [example commands](example-code.html) to get you started.

## What's next?

Start creating your VPC and its resources! Follow our [step-by-step guides](step-by-step-pages.html) to help you along.
