---
title: Repeat Caller Service
sidebar: overview_sidebar
keywords: ITK
permalink: repeat_caller_service.html
toc: false
folder: national_services
---

## What is the Repeat Caller Service?
The Repeat Caller Service is a national service operated by HSCIC and is a core part of the Integrated Urgent Care national architecture.

### Functionality
The current functions provided by the Repeat Caller Service (RCS) is as follows:

- Respond to NHS 111 Repeat Caller Queries at the start of every NHS 111 encounter
- Receive NHS 111 CDA submissions at the end of every NHS 111 encounter


## How does it work?
NHS 111 services are required to search the Repeat Caller Service (RCS) at the beginning of each urgent care encounter. The search contains a minimal set of patient demographics which are used to identify the caller.

If a caller's identity has been verified against the Personal Demographics Service (PDS), the person's NHS number will be used as the primary search term.

If a caller's identity has not been verified against the PDS, recorded demographic information will be used to try and match the person to existing records. The demographic items supported are:

- Verified NHS Number (only included if person is verified against the PDS)
- First Name
- Last Name
- Date Of Birth
- Gender
- Postcode


Using the available search criteria, the RCS will respond to the query to answer the question "Has this caller already called twice in the last 96 hours?".

| If                                       | Then                                     | Status                  |
| ---------------------------------------- | ---------------------------------------- | ----------------------- |
| There are not two previous calls for the caller | The RCS will respond '**No**'            | Not A Repeat Caller     |
| There are two or more previous calls for the caller and the caller was identified by verified NHS number | The RCS will respond '**YES**' and will include the previous call reports in the response | Confirmed Repeat Caller |
| There are two or more previous calls for the caller and the caller was identified using 4 or more of the 5 additional demographic details | The RCS will respond '**YES**' and will include the previous call reports in the response | Confirmed Repeat Caller |
| There are two or more previous calls for the caller and the caller was identified using 3 of the 5 additional demographic details | The RCS will respond '**PARTIAL**' without including call reports, and the NHS 111 is prompted to ask the caller to confirm verbally | Potential Repeat Caller |


### Record Retention
Submitted documents are stored for a maximum of 96 hours before they are deleted.


## Implementation Requirements
All IT systems used for receiving initial urgent care encounters must have connectivity to the Repeat Caller Service.

Systems should support both Repeat Caller Queries and CDA submissions at the end of encounters.


### Querying The RCS

Any system, that is used to manage people who are making first contact with Integrated Urgent Care, should query the Repeat Caller Service to identify whether that person has previously made contact with the Integrated Urgent Care service.

**If a caller's identity has been verified against the Personal Demographics Service (PDS), their NHS number should be included in the query and will be used as the primary search term.**

**If a person's identity has not been verified against the PDS, their NHS number should not be included within the query - the query should only include recorded demographic details.**

If a person is identified as having called twice previously within the preceeding 96 hours the service then they should be transferred to a clinician as a minimum level of priority (anything of a higher priority should be followed).


### Submitting To The RCS

**All systems should submit a CDA document to the Repeat Caller Service upon completion of an encounter.**

### Managing Failure
**If a submission attempt is unsuccessful, the system must continue trying to submit the document for 96 hours.**

**Systems should continue to retry the submission unless the queued submission is explcitly removed from the submission queue by a user.**



#### Configuration
**Systems should provide the ability to disable Repeat Caller Service queries when necessary.**

In the event that Repeat Caller Service queries are disabled, the system should always prompt the user to confirm whether the caller has called before to establish whether they are a repeat caller.

### General

- All systems should submit a valid CDA document to the Repeat Caller Service upon completion of an encounter.

### Configurability

- The following settings should be configurable in the system without requiring new development / releases:
  - Ability to Enable / Disable Repeat Caller Service interactions
  - Endpoint URL for the Repeat Caller Service (endpoints for Submissions and Queries should be separately configured)
  - ​

### Submission Interface
#### Retry Logic
- If a submission attempt is unsuccessful, the submission should be queued to retry the submission.
- Systems should continue to retry the submission until a reasonable number of attempts have failed, or until submission is removed from the queue by a user.
- Systems should implement retry logic which increases the amount of time between retries with each subsequent retry. This is to ensure that retries attempts do not generate

#### Monitoring
- Systems should appropriate users to failure of submissions, and provide them with appropriate tools to monitor and respond to issues.
