---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-19"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# VPC Beta Regions and Zones CLI Reference

This document gives details about the CLI commands available for working with regions and zones.

## Region

`ibmcloud is region --help`

NAME:
   `region` - View details about a region

USAGE:
   `ibmcloud is region` _`<region name>`_

OPTIONS:
   `--json`  Format output in JSON

## Regions

`ibmcloud is regions --help`

NAME:
   `regions` - List all regions

USAGE:
   `ibmcloud is regions`

OPTIONS:
   `--json`  Format output in JSON

## Zone

`ibmcloud is zone --help`

NAME:
   `zone` - View details about a zone

USAGE:
   `ibmcloud is zone` _`<region name>`_ _`<zone name>`_

OPTIONS:
  ` --json`  Format output in JSON

## Zones

`ibmcloud is zones --help`

NAME:
   `zones` - List all zones in a region

USAGE:
   `ibmcloud is zones` _`<region name>`_

OPTIONS:
   `--json`  Format output in JSON
