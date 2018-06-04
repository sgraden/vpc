---

copyright:
  years: 2018
lastupdated: "2018-06-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Creating a VPC using the {{site.data.keyword.cloud_notm}} console (Beta)

This tutorial shows you how to create and configure an {{site.data.keyword.cloud}} IBM Virtual Private Cloud (VPC) using {{site.data.keyword.cloud_notm}} console.

Follow these steps to create and configure your VPC:

1. Create a VPC and subnet to define the network.
1. Create a virtual server instance.
1. Reserve and associate a floating IP address to enable your instance to communicate with the Internet.

## Before you begin

Generate an SSH key, which will be used to connect to the virtual server instance. For example, generate an SSH key on your Linux server by running the command `ssh-keygen -t rsa -C "user_ID"`. That command generates two files. The generated public key is in the `<your key>.pub` file.

## Opening {{site.data.keyword.cloud_notm}} console

Go to the [VPC Getting Started ![External link icon](../../icons/launch-glyph.svg "External link icon")]( https://console.bluemix.net/is) page in {{site.data.keyword.cloud_notm}} console.

## Creating a VPC and subnet

To create a VPC and subnet:

1. Click **Create VPC** on the Getting Started page.
1. Enter a name for the VPC, such as `my_vpc`.
1. Enter a name for the new subnet in your VPC, such as `my_subnet`.
1. Select a location for the subnet. The location consists of a region and a zone. For this Beta release, only one location is available.
1. Enter an IP range for the subnet in CIDR notation, for example: `10.240.0.0/22`. The value must be within the IP range that is listed for the selected location. For the Beta release, you must pick a subnet prefix from a predefined range. When address prefixes are available in the release, you will have the flexibility to add new address prefix pools.
1. Attach a public gateway to the subnet to allow all attached resources to communicate with the public Internet.
1. Click **Create virtual private cloud**.

## Creating a virtual server instance

To create a virtual server instance in the newly created subnet:

1. Click **Virtual server instance** in the navigation panel and click **New instance**.
1. Enter a name for the instance, such as `my_instance`.
1. Select the VPC that you created.
1. Note the **Location** field (read-only) that shows the location of the subnet where the instance is created.
1. Select an image (that is, operating system and version) such as Ubuntu 16.04.
1. Select one of the popular profiles, or click **All profiles** to choose a different core and RAM combination that is most appropriate for your workload.
1. Select an existing SSH key or add an SSH key that will be used to access the virtual server instance. To add an SSH key, click **Add SSH key** and name the key. After you enter your previously generated public key value, click **Add SSH key**.
1. Optional: Enter user data or metadata for the instance. This data is typically used with custom provisioning scripts. For more information, see [User Data](/docs/vsi-is/vsi_is_provisioning_scripts.html).
1. Note the boot volume. For the Beta release, 100 GB is allotted for the boot volume.
1. In the **Network interfaces** area, you can change the name and port speed of the interface. If you have more than one subnet in your VPC, you can select the subnet that you want to attach to the instance.
1. Click **Create virtual server instance**.

## Reserving a floating IP address

Reserve and associate a floating IP address to enable your instance to be reachable from the Internet.

**Tip:** Your instance must be running before you can associate a floating IP address. It can take a few minutes for the instance to be up and running.

To reserve and associate a floating IP address:

1. In the left navigation, click **Floating IP**.
1. Click **Reserve floating IP**.
1. Select the instance that you just created and its network interface that you want to associate with the floating IP address.
1. Click **Reserve IP**. The new IP address is displayed on the Floating IPs page.

## Connecting to your instance

Using the floating IP address that you created, ping your instance to make sure it's up and running:

`ping <public ip address>`

Since you provisioned your instance with a public SSH key, you can now connect to it directly by using your private key:

`ssh -i <path to your private key file> root@<public ip address>`

## Congratulations!

You've successfully created and configured a VPC and subnet, a virtual server instance, and a floating IP address. You can continue to develop your VPC by adding more instances and subnets.
