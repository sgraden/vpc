---

copyright:
  years: 2018
lastupdated: "2018-06-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:generic: .ph data-hd-programlang='generic'}
{:java: .ph data-hd-programlang='java'}
{:ruby: .ph data-hd-programlang='ruby'}
{:c#: .ph data-hd-programlang='c#'}
{:objectc: .ph data-hd-programlang='Objective C'}
{:python: .ph data-hd-programlang='python'}
{:node: .ph data-hd-programlang='node'}
{:php: .ph data-hd-programlang='PHP'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:node: .ph data-hd-programlang='node'}
{:middle: .ph data-hd-position='middle'}
{:right: .ph data-hd-position='right'}


# Error handling in the IBM Cloud VPC Beta API

This API uses standard HTTP response codes to indicate whether a method completed successfully. A `200` response always indicates success. A `400` type response is some sort of failure, and a `500` type response usually indicates an internal system error.

Here are some model code examples for error handling in the IBM Cloud VPC Beta API:

## Success 200 Example Code

```
200 The API was retrieved succcessfully

{
  "first": {
    "href": "https://iaas.bluemix.net/v1/floating_ips?limit=20"
  },
  "limit": 20,
  "next": {
    "href": "https://iaas.bluemix.net/v1/floating_ips?start=9d5a91a3e2cbd233b5a5b33436855ed1&limit=20"
  },
  "floating_ips": [
    {
      "id": "39300233-9995-4806-89a5-3c1b6eb88689",
      "crn": "crn:v1:bluemix:public::us-south::gt:floating-ip:39300233-9995-4806-89a5-3c1b6eb88689",
      "href": "https://iaas.bluemix.net/v1/floating_ips/39300233-9995-4806-89a5-3c1b6eb88689",
      "address": "203.0.113.1",
      "name": "my-floating-ip",
      "created_at": "2018-06-20T20:45:34.611Z",
      "resource_group": {
        "id": "56969d60-43e9-465c-883c-b9f7363e78e8",
        "href": "https://resource-manager.bluemix.net/v1/resource_groups/56969d60-43e9-465c-883c-b9f7363e78e8",
        "name": "my-resource-group"
      },
      "status": "available",
      "tags": [
        "production",
        "backend"
      ],
      "zone": {
        "name": "us-south-1",
        "href": "https://iaas.bluemix.net/v1/regions/us-south/zones/us-south-1"
      }
    }
  ]
}
```

## Success 201 Example Code for ACL

```
201 The rule was created successfully

{
  "action": "allow",
  "before": {
    "id": "8daca77a-4980-4d33-8f3e-7038797be8f9"
  },
  "destination": "192.168.0.0/24",
  "direction": "ingress",
  "name": "my-acl-rule-2",
  "port_max": 81,
  "port_min": 80,
  "protocol": "tcp",
  "source": "10.0.0.5"
}
```
## Success 201 Example Code for security group

``` 
201 The security group was created successfully

{
  "id": "be5df5ca-12a0-494b-907e-aa6ec2bfa271",
  "crn": "crn:v1:bluemix:public:gt:us-south-1:a/123456::security-group:be5df5ca-12a0-494b-907e-aa6ec2bfa271",
  "href": "https://iaas.bluemix.net/v1/security_groups/be5df5ca-12a0-494b-907e-aa6ec2bfa271",
  "name": "allow_ssh",
  "resource_group": {
    "id": "56969d60-43e9-465c-883c-b9f7363e78e8",
    "href": "https://resource-manager.bluemix.net/v1/resource_groups/56969d60-43e9-465c-883c-b9f7363e78e8",
    "name": "my-resource-group"
  },
  "rules": [
    {
      "direction": "ingress",
      "ip_version": "ipv4",
      "port_max": 81,
      "port_min": 80,
      "protocol": "tcp",
      "remote": {
        "cidr_block": "192.168.0.0/24"
      },
      "id": "6f2a6efe-21e2-401c-b237-620aa26ba16a"
    }
  ],
  "tags": [
    "production",
    "backend"
  ],
  "vpc": {
    "id": "4727d842-f94f-4a2d-824a-9bc9b02c523b"
  },
  "created_at": "2018-06-20T21:03:13.675Z",
  "network_interfaces": [
    {
      "id": "10c02d81-0ecb-4dc5-897d-28392913b81e",
      "href": "https://iaas.bluemix.net/v1/instances/1e09281b-f177-46fb-baf1-bc152b2e391a/network_interfaces/10c02d81-0ecb-4dc5-897d-28392913b81e",
      "name": "my-network-interface",
      "primary_ipv4_address": "string"
    }
  ]
}
```

## Failure 400 Example Code

```
400 An Invalid Floating IP Template was Provided

{
  "errors": [
    {
      "code": "missing_field",
      "message": "The `flavor.id` field is required.",
      "more_info": "https://console.bluemix.net/docs/iaas/instances.html#template",
      "target": {
        "name": "flavor.id",
        "type": "field"
      }
    }
  ],
  "trace": "86780a34-e651-4b47-9fb0-184a169cc9af"
}
```

## Failure 404 Example Code

```

404 The specified Floating IP could not be found

{
  "errors": [
    {
      "code": "missing_field",
      "message": "The `flavor.id` field is required.",
      "more_info": "https://console.bluemix.net/docs/iaas/instances.html#template",
      "target": {
        "name": "flavor.id",
        "type": "field"
      }
    }
  ],
  "trace": "86780a34-e651-4b47-9fb0-184a169cc9af"
}
```
