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

# Creating a VPC using the IBM Cloud console (Beta)

This tutorial shows you how to create and configure an IBM Cloud IBM Virtual Private Cloud (VPC) using IBM Cloud console.

Follow these steps to create and configure your VPC:

1. Create a VPC and subnet to define the network.
1. Create a virtual server instance.
1. Reserve and associate a floating IP address to enable your instance to communicate with the Internet.
<!---1. Configure an access control list to limit the subnet's inbound and outbound traffic. By default, all traffic is allowed.--->
## Before you begin

Generate an SSH key, which will be used to connect to the virtual server instance. For example, generate an SSH key on your Linux server by running the command `ssh-keygen -t rsa -C "user_ID"`. That command generates two files. The generated public key is in the `<your key>.pub` file.

## Opening IBM Cloud console

Go to the [VPC Getting Started ![External link icon](../../icons/launch-glyph.svg "External link icon")]( https://console.bluemix.net/is) page in IBM Cloud console.

## Creating a VPC and subnet

To create a VPC and subnet:

1. Click **Create VPC** on the Getting Started page.
1. Enter a name for the VPC, such as `my_vpc`.
1. Enter a name for the new subnet in your VPC, such as `my_subnet`.
1. Select a location for the subnet. The location consists of a region and a zone. For this Beta release, only one location is available.
1. Enter an IP range for the subnet in CIDR notation, for example: `10.240.0.0/22`. The value must be within the IP range that is listed for the selected location.
1. Attach a public gateway to the subnet to allow all attached resources to communicate with the public Internet.
1. Click **Create**.
<!---
1. Select or create the default access control list for new subnets in this VPC. In this tutorial, let's create a new default access control list. We'll configure the access control list later.
1. Select an access control list for the subnet. Let's select **Use VPC default** to use the default access control list that will be created for this VPC.
--->
<!---
## Configuring the access control list 

You can configure the access control list to limit inbound and outbound traffic to the subnet. By default, all traffic is allowed.

Only one access control list can be attached to a subnet at any time. However, one access control list can be attached to multiple subnets. 

To configure the access control list:

1. On the VPC and subnets page, click the **Subnets** tab.
1. Click the subnet that you just created.
1. In the **Subnet details** area, click the name of the access control list.
1. Click **Add rule** to configure inbound and outbound rules.
1. When you're finished creating rules, click the **All access control lists** breadcrumb at the top of the page.

### Example access control list

For example, you can configure inbound rules that do the following:

 - Allow HTTP traffic from the Internet 
 - Allow all inbound traffic from the subnet 10.10.20.0/24
 - Deny all other inbound traffic  

Then, configure outbound rules that do the following:

- Allow HTTP traffic to the Internet 
- Allow all outbound traffic to the subnet 10.10.20.0/24
- Deny all other outbound traffic  

![Shows the sample inbound and outbound rules](images/acl_rules.png)
--->
## Creating a virtual server instance

To create a virtual server instance in the newly created subnet:

1. Click **Virtual server instance** in the navigation panel and click **New instance**.
1. Enter a name for the instance, such as `my_instance`.
1. Select the VPC that you created.
1. Note the **Location** field (read-only) that shows the location of the subnet where the instance is created.
1. Select an image (that is, operating system and version) such as Ubuntu 16.04.
1. Select one of the popular profiles, or click **All profiles** to choose a different core and RAM combination that is most appropriate for your workload.
1. Select an existing SSH key or add an SSH key that will be used to access the virtual server instance. To add an SSH key, click **Add SSH key** and name the key. After you enter your previously generated public key value, click **Add SSH key**.
1. Optional: Enter user data or metadata for the instance. This data is typically used with custom provisioning scripts.
1. Note the boot volume. For the Beta release, 100 GB is allotted for the boot volume.
1. In the **Network interfaces** area, you can change the name and port speed of the interface. If you have more than one subnet in your VPC, you can select the subnet that you want to attach to the instance.
1. Click **Create**.

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

<!--- an access control list,--->
