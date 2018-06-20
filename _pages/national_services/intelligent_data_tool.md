---
title: Intelligent Data Tool (IDT)
sidebar: overview_sidebar
keywords: IDT
permalink: intelligent_data_tool.html
toc: true
folder: national_services
---

## Reporting Output Data
Data pertaining to the history of each NHS Pathways triage is required for reporting purposes by host organisations. The data must also be sent to NHS Pathways in order to comply with the Continuous Quality Improvement (CQI) section of the Pathways licence agreement; triage data must be sent in real time to NHS Pathways at the closing of each triage call.

The IDT Web Service, which was originally known as the CQI web service, provides a mechanism to support the transfer of data from the host system back to NSH Pathways.

## IDT Web Service
### Overview
The Pathways IDT webservice is a RESTful service which can be accessed via standard HTTP methods by a variety of programming languages.

### Endpoint URLs
Two endpoint URLs are provided to host system providers as they develop their solution, one is intended for User Acceptance Testing (UAT) and the other for Live operational use.

### Authentication
Traffic passing between the Host system and the IDT Web Service should be encrypted over a connection using Transport Layer Security (TLS). Additionally, encoded access credentials are requested to be sent as part of the http request header.

To obtain a user account and further details on the Web Service interfaces and data structures, please contact a member of the NHS Pathways technical team at [pathwaysidtreports@nhs.net](mailto:pathwaysidtreports@nhs.net).

### Web Methods

| **METHOD** | **URL** | **DESCRIPTION** |
| cqiCase | /api/v1/cqiCase | Main method for posting case, triage and service data to the IDT webservice |
| cqiExceptionCodes | /api/v1/cqiExceptionCodes | List of possible exception codes returned from the WebApi |
