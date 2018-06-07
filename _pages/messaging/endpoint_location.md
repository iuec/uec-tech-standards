---
title: Endpoint Location
sidebar: overview_sidebar
keywords: ITK, endpoints
permalink: endpoint_location.html
toc: false
folder: messaging
---

The current Directory of Services (DOS) has functionality for storing endpoint details for services which are listed on the DOS.

The endpoint details support the routing of patients and cases through the Integrated Urgent Care system but telling clinical systems **how** to get encounter information from one service to another.



## Endpoint Details

The Pathways DOS API has a method called 'ServiceDetailsById' - this allows a system to provide a DOS Service ID or Organisational Data Service (ODS) Code and get back details of any endpoints that are configured for that service.

Endpoint details are structured as a prioritised list of endpoints with various attributes defining how those endpoints can be used.

### Endpoint Records

The following table details each attribute that is stored against an 'endpoint':

| Attribute         | Description                              |
| :---------------- | :--------------------------------------- |
| Priority / Order  | The priority / order is used to 'sort' the entire list of endpoints for a single service. |
| Transport         | The transport type for an endpoint defines the transport method used for getting information to that endpoint (e.g. ITK, Email, Phone). |
| Endpoint Address  | The endpoint address is the actual address identifier that the information will be sent to for that service. |
| Interaction       | The interaction value denotes which ITK interaction sh≥÷/ould be used for the transmission of the information. |
| Format            | The endpoint format defines the format in which the information should be represented (e.g. CDA, HTML, PDF). |
| Business Scenario | The business scenario defines the situation in which a particular endpoint should be used. Currently this can be **Primary** or **Copy**. |
| Compressed        | The compressed flag is used for ITK messages and defines whether or not the endpoint can accept compressed ITK messages. Where the value is **True**, ITK messages should be sent with compression enabled. Where the value is **False** or not present, ITK messages should be sent uncompressed. |

#### Payload Formats

Not all transports support all formats - you can build these rules into your endpoint handling so as to avoid supporting unecessary combinations of transport / format. For example, you do not need to support the sending of a CDA XML document via Email.

The following table shows which formats are currently supported by which transports:

| Transport | Supports CDA? | Supports PDF? | Supports HTML? |
| --------- | ------------- | ------------- | -------------- |
| ITK       | Yes           | No            | No             |
| Email     | No            | Yes           | Yes            |
| Phone     | N/A           | N/A           | N/A            |



#### Business Scenarios

| Business Scenario | Description                              |
| :---------------- | :--------------------------------------- |
| Primary           | This should be used when information is being shared for the purpose of a primary referral of an active encounter. |
| Copy              | This should be used when information is being communicated **for information only** either during or after an active encounter (e.g. Post Event Message to a patient's GP surgery) |



#### Email Endpoints

Where email is used for Transfer of Care messages (sending CDA messages via email instead of ITK), there is a specific list of email domains which should be supported; attempts to send person identifiable data (PID) to any other domain should be blocked by the sending system.

The official list of acceptable domains for transferring person identifiable data (PID) is available on the HSCIC website here: [HSCIC - Sending secure email](http://systems.hscic.gov.uk/nhsmail/secure)

It is possible that this list may change in the future. It is therefore recommended that system suppliers should make it easy to update the list of valid email domains in customer systems so as to avoid having to deploy new product releases if the list changes in the future.

Systems using email to send urgent care messages should also conform to the "Secure email standard" also detailed on the [HSCIC - Sending secure email](http://systems.hscic.gov.uk/nhsmail/secure) page.



## Endpoint Webservice (ServiceDetailsById)

The ServiceDetailsById function is part of the Pathways DOS API - the definition can be found here: [https://www.pathwaysdos.nhs.uk/app/api/webservices?wsdl](https://www.pathwaysdos.nhs.uk/app/api/webservices?wsdl)



A request to the ServiceDetailsById API requires the following mandatory information:

| Item       | Description                              |
| :--------- | :--------------------------------------- |
| Service ID | The identifier of the service for which details are required - can be either a DOS Service ID or an ODS code |



The response from the ServiceByDetailsId API provides a list of 0 or more 'endpoints' each containing the following information:

| Item  | Description                              |
| :---- | :--------------------------------------- |
| Tag   | Currently used to communicate the endpoint transport type e.g. ITK, Email, DTS |
| Name  | A string description of the specific endpoint |
| Value | A concatenated string of endpoint attributes. See the **Endpoint Value Concatenated String** section below for more information. |
| Order | The priority / order number of the specific endpoint |



#### Endpoint Ordering

Upon retrieving a complete list of endpoints from the webservice, the consuming system should then order the returned list in ascending order using the Order attribute for each endpoint. Where there are multiple endpoints that meet a certain criteria (e.g. Primary busines scenario) the system uses the order to identify which endpoint should be attempted first (Order 1), and which should be used as a backup (Order 2).



#### Endpoint Value Concatenated String

The endpoint value is a concatenated string of endpoint attributes which are separated by a custom delimeter of `\|`

The structure of the concatenated string is as follows:

```
Endpoint Address \| Interaction \| Format \| Business Scenario \| Compressed?

http://SampleHostname/SendCDADocument\|urn:nhs-itk:interaction:primaryOutOfHoursRecipientNHS111CDADocument-v2-0\|CDA\|Primary\|Compressed

email.address@nhs.net\|urn:nhs-itk:interaction:primaryEmergencyDepartmentRecipientNHS111CDADocument-v2-0\|PDF\|Primary\|Compressed
```
