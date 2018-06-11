---
title: Ambulance Requests
sidebar: overview_sidebar
keywords: ITK
permalink: ambulance_requests.html
toc: true
folder: messaging
---
{% include note.html content="This page is still under development." %}

Integrated Urgent Care services have the ability to directly request an ambulance for a patient where necessary.

A message specification for Ambulance Requests is defined as part of the NHS 111 ITK Domain Message Specification. NHS 111 services, which are using NHS Pathways as a triage too$

These electronic ambulance requests are defined in the [NHS 111 ITK Domain Message Specification](https://isd.hscic.gov.uk/trud3/user/authenticated/group/0/pack/1/subpack/192/rel$


### Identifying the correct ambulance service

To identify the appropriate ambulance service to send a request to, the postcode of the patient's current location is mapped to the ambulance service responsible for that area.

`Postcode -> CCG -> Ambulance Service`

There is currently no central lookup service for Postcode to Ambulance Service mapping, so systems should implement a lookup locally.

1. Upon identifying the need for an ambulance, find the correct ambulance service by using the postcode of the *patient's current location*.

2. Display a clear message to the user on-screen confirming which ambulance service has been selected.

3. Allow the user to confirm the selection and immediately trigger an ambulance request message to that ambulance service.

In the event that an ambulance service cannot be automatically matched to the postcode, allow the user to manually select the ambulance service that they would like to send the request to.


### Ambulance requests from clinical hubs

With the introduction of Clinical Assessment Services (CAS), electronic ambulance requests will be expanded for use by other urgent care services in addition to the current NHS 111 services.
