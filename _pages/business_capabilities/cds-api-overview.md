---
title: Clinical Decision Support API Overview
sidebar: overview_sidebar
permalink: cds-api-overview.html
toc: true
folder: business_capabilities
---

The aim of the CDS API is to enable Encounter Management System (EMS) and Clinical Decision Support System (CDSS) interactions to support the interoperable triage of a patient, with a view to giving providers the greatest choice, and enable personalised and seamless triage journey for a patient using open standards. 

## Context 
The patient journey starts when a patient calls in with a health issue.  

`TODO insert image: (A simple patient journey illustration)`


The patient contacts the service. The system user initiates this as a patient encounter on the EMS. This may either be self-directed (via 111, 999, Out of hours GP, Emergency Department) or as a result of being transferred from another UEC care setting (disposition outcome). Contact may be through a wide variety of channels, including phone, face to face or video call. Contact may also be through a third party (e.g. phoning on behalf of…)

At the start of contact, the EMS establishes their reason for contact.

The patient is triaged to determine the health needs. Triage may be done by either a non-clinical call handler, or a clinician, or both. Some triage may be done by technology (e.g. IVR, chatbots, robots or other AI agents). Usually a Clinical Decision Support tool helps in this clinical triage and assessment. The scope of CDS API encompasses the interactions between the EMS and CDSS. 

Following triage, the patient will either: 
- be transferred to another UEC care setting 
- have a clinical consultation 
- be given self-care instructions, 
- have an ambulance dispatched – note that this is a special form of transfer

The actions on outcome are carried by EMS system users outside of the CDS API interactions and as such the role of the CDS API ends here. 


## EMS and CDSS interaction using Open standards 

`TODO`
`- insert image: EMS CDSS Sample Operational representation`
`- add links for FHIR  STU3 and CDS API Implementation guide`

The key requirement is to build APIs such that the two disparate systems interact, and by which the EMS can call the CDSS and get responses back through the API, following the HL7 FHIR standard detailed in the CDSS API specification Implementation Guide v1.1.  

A logical flow for the patient journey related interactions between the EMS and the CDSS for triage could be as described below- 


<table>
    <tr>
        <td style="width:100px;">
            Start
        </td>
        <td>
            The Patient approaches the Health Professional (EMS system user) with a complaint needing urgent attention, marks the start of patient encounter starts.

            This could be through any channel explained above. 

            The EMS will drive the start of the patient journey.
        </td>
    </tr>
    <tr>
        <td>
            Step 1
        </td>
        <td>
            The CDS API specification provides information on how the CDSS can be called by EMS to start a triage. 

            This should be able to make use of information already collected, and not asking for information that has already been provided.
        </td>
    </tr>
    <tr>
        <td>
            Step 2
        </td>
        <td>
            The CDSS in return will pose questions to be answered by the patient through EMS.
        </td>
    </tr>
    <tr>
        <td>
            Step 3
        </td>
        <td>
            The EMS-CDSS messaging interactions continue until a disposition or result is reached.

        </td>
    </tr>
    <tr>
        <td>
            Step 4
        </td>
        <td>
            Outcome or result (disposition reached). The session with CDSS is terminated.

            This should be able to package up data collected and posting to the EMS.

            This data should include the outcome of the CDSS flow i.e. a coded disposition or health need.

        </td>
    </tr>
    <tr>
        <td>
            End
        </td>
        <td>
            Patient journey transferred back and continues from the EMS

        </td>
    </tr>
</table>



## Messaging architecture overview 

`TODO Insert diagram`

Simplified diagrammatic representation


