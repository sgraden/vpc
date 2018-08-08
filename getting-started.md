---

copyright:
  years: 2017, 2018
lastupdated: "2018-08-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Getting started with IBM Cloud Virtual Private Cloud Beta release

You can create, name, and resize your IBM Cloud VPC using the [IBM Console](console-tutorial.html), the [`ibmcloud` CLI](cli-network-reference.html), or the [VPC REST API](apis.html) provided by IBM Cloud. For step-by-step instructions, refer to these documents:

 * [Using the IBM Consule UI to set up your VPC and its resources](console-tutorial.html)
 * [Using the `ibmcloud` command line interface to set up your VPC and its resources](how-to-verify-access.html#cli-access)
 * [Using the IBM Cloud VPC REST API to set up your VPC and its resources](how-to-verify-access.html#api-access)

## Before you begin

Depending on which interface you decide to use, you may need to perform some or all of these prerequisites before you can start creating a VPC:

 * **Permissions**: Be sure that you have sufficient permissions to create and manage resources in your VPC. For a list of required permissions, see [Granting permissions needed for VPC users](vpc-user-permissions.html).

 * **Get your SSH key**: You will use the SSH key to connect to your virtual server instance(s). 
 
   * **Look for a file** called `id_rsa.pub` under an `.ssh` directory under your home directory, for example, `/Users/<USERNAME>/.ssh/id_rsa.pub`. The file starts with `ssh-rsa` and ends with your email address.

   * **Or Generate an SSH Key**: If you do not have a public SSH key or if you forgot the password of an existing one, generate a new one by running the `ssh-keygen` command and following the prompts. For example, you can generate an SSH key on your Linux server by running the command `ssh-keygen -t rsa -C "user_ID"`. That command generates two files. The generated public key is in the `<your key>.pub` file. 

* **Download the CLI plugin to use the CLI**: If you plan to use the `ibmcloud` CLI, first [download and install the VPC plugin for IBM Cloud](how-to-verify-access.html#cli-access).

* **API endpoint**: For API access, you will receive an endpoint through email.

## Overview steps for setting up your IBM Cloud VPC

Here's the general flow for how to get going, using whichever interface method you may choose:

1. Create a Virtual Private Cloud.
2. Create one or more subnets in the Virtual Private Cloud in one or more zones.
3. Create network Access Control Lists (ACLs) to manage traffic to your subnets.
4. Select the profiles of virtual server instances (VSIs) you'd like to run, and instantiate them.
5. Create security groups to manage traffic to your virtual servers.
6. Reserve a Floating IP address, and associate it with a server.
7. Create a public gateway (PGW) if you want public internet traffic to your subnet.
8. Create servers in one or more zones of a Virtual Private Cloud.
9. Deploy your service or applications across those servers


**Note: You can delete a Virtual Private Cloud if there are no running instances in it.**
