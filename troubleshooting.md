---

copyright:
  years: 2018
lastupdated: "2018-06-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Troubleshooting your IBM Cloud VPC in the Beta release

This document covers common difficulties you might encounter, and offers some helpful tips.

## Using DEBUG mode or `verbose` mode 

When you're having trouble diagnosing a difficulty, you can use the CLI to get into DEBUG mode, by giving the following command before any other call you make to the IBM Cloud CLI. For example, for the command `ibmcloud is pubgws` you'd write:

```
RIAAS_DEBUG=yes ibmcloud is pubgws
```
The debug information is helpful to you and also to the support team who may be called upon to diagnose your problem.

**Another option is to use verbose mode**

For example, you can add `--verbose` to your `curl` command and send us the `x-request-id:` value so we can troubleshoot the problem. The `--verbose` flag is particularly helpful if you are experiencing connectivity problems.

**Another option is to add the `-i` flag to your `curl` command** so that the support team can see the headers in the response of your request. This flag is helpful in most situations when you need to contact support. Here's an example of what you might see when you use the `-i`flag:

```
curl -i https://${credentials}@rias.wrig.me:5000/v1/vpcs/0ba0c6f1-705a-4e37-9e26-0f2d7e505329 -H X-Auth-Token:$iam_token -H X-Subject-Token:$subject_token
HTTP/2 200 
server: nginx/1.13.5
date: Fri, 25 May 2018 14:45:31 GMT
content-type: application/json; charset=utf-8
content-length: 246
x-request-id: 98a977bd-020b-422b-beb5-0843ab500c41
strict-transport-security: max-age=15724800; includeSubDomains;

{"id":"0ba0c6f1-705a-4e37-9e26-0f2d7e505329","crn":"","name":"VPC-a-late-making-modified","href":"https://rias.wrig.me:5000/v1/vpcs/0ba0c6f1-705a-4e37-9e26-0f2d7e505329","status":"available","is_default":false,"created_at":"2018-04-25T03:30:28Z"}
```


### If Trace ID is blank

Usually, when the Trace ID is blank, it is because the JSON returned does not match what is expected from the Swagger. Try `RIAAS_DEBUG=yes ibmcloud is server-rm 3fb7c1eb-45fd-4c85-962e-617f216e7393` (substitute your correct server ID token) and check the output.

## Other Issues

Here are a few difficulties you might encounter:

### Not on the Whitelist

If this is your problem, you'll see a 401 or 403 error. Contact your support team.

### Permissions not set up in IBM Cloud Infrastructure (SoftLayer)

Before you can create Virtual Servers, you need the correct permissions to be set up on the IBM Cloud Infrastructure (SoftLayer) side. If your permissions are not correct, you can create a server and it will show `Pending` status, which quickly turns into `Failed` status. Make sure the master of the account assigns you the correct [permissions](vpc-user-permissions.html).

### Servers are all in Unknown status

Most likely you do not have adequate permissions to view the server status. Make sure you have the correct [permissions](vpc-user-permissions.html). It also could be caused by an expired IMS token. Run `bx sl init` again and rebuild the `ims_subject` with the new token. Make sure you are passing in the `X-Subject-Token:$ims_subject` parameter in the request header.

### IAM token expired

**Problem:** Service is no longer returning any JSON, instead of just giving an HTTP 403 status to all of my requests.  My earlier requests were going through. What happened?

**Answer:** This error will happen after about an hour if your IAM token has expired. Refresh your IAM token by re-running `iam_token=$(ibmcloud iam oauth-tokens | awk '/IAM/{ print $4; }')`. 


