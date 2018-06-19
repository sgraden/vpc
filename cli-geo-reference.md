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

# VPC Beta Regions and Rones CLI Reference

This document gives details about the CLI commands available for working with regions and zones.

## Region

`bx is region --help`

NAME:
   region - View details about a region

USAGE:
   bx is region <region name>

OPTIONS:
   --json  Format output in JSON

## Regions

`bx is regions --help`

NAME:
   regions - List all regions

USAGE:

   bx is regions

OPTIONS:
   --json  Format output in JSON

## Zones

`bx is zones --help`

NAME:
   zones - List all zones in a region

USAGE:
   bx is zones <region name>

OPTIONS:
   --json  Format output in JSON

## Zone

`bx is zone --help`

NAME:
   zone - View details about a zone

USAGE:
   bx is zone <region name> <zone name>

OPTIONS:
   --json  Format output in JSON
