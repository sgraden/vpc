---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Get your IBM Cloud Account Information

To locate your account information, log into the [IBM Cloud CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}, and run `ibmcloud target` to view your account.

```
ibmcloud login --sso -a https://api.ng.bluemix.net
ibmcloud target
```

**You should see something like this:**
```
ibmcloud target


API endpoint:     https://api.ng.bluemix.net (API version: 2.92.0)   
Region:           us-south   
User:             your-email@ibm.com
Account:          Your Account (abcdefghijklmnopqrstuvwxyz123456) <-> 1234567
Resource group:   No resource group targeted, use 'bx target -g RESOURCE_GROUP'
Org:                 
Space:

```

**Tip: If you are managing Cloud Foundry applications and services**

 * Use the command `ibmcloud target --cf` to target Cloud Foundry org/space interactively.
 * Use `ibmcloud target -o ORG -s SPACE` to target the org/space.
 * Use `ibmcloud cf` if you want to run the Cloud Foundry CLI with the current IBM Cloud CLI context.
