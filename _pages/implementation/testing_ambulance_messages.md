---
title: Testing Ambulance Requests
sidebar: overview_sidebar
keywords: ambulance
permalink: testing_ambulance_messages.html
toc: false
folder: implementation
---
{% include note-furtherupdates.html %}

# Testing Ambulance Requests

It is important that you have completed thorough testing of ambulance interoperability before using it to support a live service. There are several areas that you should be assuring, and this guidance seeks to establish some best practice around this.

*Note: Testing ambulance links can be time-consuming, so it is important that you allow for this testing in your implementation plan.*  

## Map your landscape

In order to plan your testing approach, you need to map out your interoperability landscape. You can think of this as being like a web of 'nodes' and 'connectors'.  

The 'nodes' are your 'organisational entities' - the organisation, its people, and its IT systems. Within our landscape this might be an NHS 111 provider, its call-handlers and clinicians, and its clinical case management system.  

The 'connectors' represent the  links between the nodes - the interoperability links between organisations and their IT systems and the 'pipes' through which messages and data will be flowing. Sometimes (but not always) these connectors also represent the actual path of the clinical responsibility for the patient.  

Within the context of ambulance request messaging, you should identify the following:

* What are the 'nodes' in your map? Which organisations are you going to be interacting with and therefore you need to care about?
* What are the 'connectors'? What is the nature or 'type' of the interoperability links with each of those organisations? Which way does the data or message flow? Who initiates the flow of messages or data?
* What about 'offline' nodes and connectors? Are there any organisations which should be part of this picture, but with which you do not have

## Supplier to supplier testing

This is the responsibility of your software suppliers.
