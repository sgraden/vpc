---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Using 2-factor authentication for IBM Cloud Infrastructure initialization with IBM Cloud VPC

This sequence of commands must be executed from the [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started).

**Step 1. Get the IAM token for the IBM Cloud account**

Log into IBM Cloud, and make sure you select a linked account.

```
ibmcloud login --sso
```
{: codeblock}

You can see the IAM token with:

```
ibmcloud iam oauth-tokens
```
{: codeblock}

The IAM token is cached under:

```
cat ~/.bluemix/config.json
```
{: codeblock}

**Step 2. Get the IMS token for the IBM Cloud Infrastructure account**

```
bx sl init
```
{: codeblock}

If  2-factor authentication (2FA) authentication is enabled in the IBM Cloud Infrastructure account, you will be prompted for security questions, and so forth.

The IMS token is cached under:

```
cat ~/.bluemix/plugins/softlayer/config.json
```
{: codeblock}

**Step 3: Construct IMS Subject token**

Use the values from `~/.bluemix/plugins/softlayer/config.json` to construct the IMS Subject token needed to run Compute Regional API calls.

```
ims_subject={"ims":{"token":"<IMS TOKEN>","account":<ACCOUNT ID>,"user":<USER ID>,"endpoint":"https://api.softlayer.com/mobile/v3.1","username":""},"land":{}}
```
{: codeblock}

**Step 3. Pass both tokens to Regional APIs**

Pass the IAM token as the `X-Auth-Token:` and the IMS Subject token as the `X-Subject-Token:` in the header as parameters to the VPC APIs.

