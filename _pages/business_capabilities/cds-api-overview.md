---
title: Clinical Decision Support API Overview
sidebar: overview_sidebar
permalink: cds-api-overview.html
toc: true
summary: This page is intended as an orientation guide for API developers, who are making systems compliant to the Clinical Decision Support API (CDS API)
folder: business_capabilities
---

NHS Digital is committed to setting strong, open standards for inter-operable internet-first digital service provision. Development of standards, frameworks and Application Programming Interfaces (APIs) are the chosen route for improving data sharing and giving clinicians better access to patient information.

The [Clinical Decision Support API Specification v1.0.0](https://developer.nhs.uk/apis/cds-api-1-0-0/) is the first standard published to support the interactions between a Clinical Decision Support System (CDSS) and an Encounter Management System (EMS) to support patient triage using open standards.

## Business Context 

The CDS API will enable better data flow between care providers clinical systems and services to get patients the right care in the right place at the right time.

The CDS API enables coded transfer of clinical information at key points of handover. This means:

1. Information can be easily transferred between different services such as online and telephony or post event messaging from 111 to GPs
2. Clinicians will be able to connect patients to the right care more easily
3. Patients don’t have to repeat themselves when moving around the system

By reporting consistent data we will be able to analyse blind spots between systems and services, driving continuous improvement. Open standards with no proprietary code sets will make it easier for new technology to emerge and be integrated. 

The aim of the CDS API is to enable EMS and CDSS interactions to support the inter-operable triage of a patient. This is with a view to give care providers the greatest choice and enable a personalised and seamless triage journey for a patient, using open standards. 


## CDS API in a patient journey 
The patient Journey starts when a patient contacts the NHS service with a health issue.  

<p style="text-align:center;"><img src="images/cds-api-simplified-patient-journey.png" alt="A simplified patient journey through any UEC channel" title="A simplified patient journey through any UEC channel" style="width:100%">
<br>
A simplified patient journey through any UEC channel
</p>

 <table>
    <tr>
        <td>
            <p><strong>Patient contact</strong></p>
            <p>The patient contacts an NHS service. Contact may be
                <ul>
                    <li>
                        Self-directed (to 111, 999, GP out of hours service, emergency department) or as a result of being transferred from another care setting (disposition outcome). 
                    </li>
                    <li>
                        Through a variety of channels (phone, face to face, video call).
                    </li>
                    <li>
                        Through a third party (phoning on behalf of...)
                    </li>
                </ul>
            </p>
        </td>
    </tr>
    <tr>
        <td>
            <p><strong>Access to data</strong></p>
            <p>The system user initiates this as a patient encounter on the EMS.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>At the start of the contact, the EMS establishes the reason for contact.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p><strong>Triage and consult</strong></p>
            <p>The patient is triaged to determine the health need. <br>
        Triage may be conducted by a non-clinical call handler, a clinician, or both. Some triage may be automated (using IVR, chatbots or other AI agents). Usually a Clinical Decision Support tool helps in this clinical triage and assessment.</p>
    </td>
    </tr>
    <tr>
        <td><p>Following triage, the CDSS recommends a triage outcome. <br> 

            <ul>
                <li>
                    Redirection for further assessment <br>
                    For example, a call being transferred to a clinician for further triage and assessment or call back from clinician agreed.
                </li>

                <li>
                    Referral <br>
                    Have an ambulance dispatched (note that this is a special form of transfer)
                    <br>
                    or referral to other service, for example to pharmacy or GP.
                </li>
                
                <li>
                    Care advice <br>
                    For example, providing the patient with self-care instructions
                    <br>
                </li>

            </ul>
                    These recommendation are carried by EMS system users outside of the CDS API interactions and as such the role of the CDS API ends here. 
        </p>
    </td>
</tr>
</table>




## Scope

The scope of the CDS API encompasses the interactions between the EMS and CDSS using open standards.

<p style="text-align:center;"><img src="images/cds-api-operational-representation.png" alt="EMS CDSS Sample Operational representation" title="EMS CDSS Sample Operational representation" style="width:80%">
<br>
EMS CDSS Sample Operational representation
</p>

The key requirement is to build APIs such that the two disparate systems interact, and by which the EMS can call the CDSS and get responses back through the API, following the HL7 FHIR standard detailed in the [CDSS API specification Implementation Guide v1.0](https://developer.nhs.uk/apis/cds-api-1-0-0/). 

Below is a generic example workflow for the patient journey related interactions between the EMS and the CDSS for triage:

<table>
    <tr>
        <td style="width:100px;">
            Start
        </td>
        <td>
            The patient approaching an NHS Service with a complaint needing urgent attention, marks the start of the patient encounter. This could be through any channel explained above. 
            <br>
            The EMS will drive the start of the patient journey on the system.
        </td>
    </tr>
    <tr>
        <td>
            Step 1
        </td>
        <td>
            The CDS API specification defines how the CDSS can be called by the EMS to start a triage. 
        </td>
    </tr>
    <tr>
        <td>
            Step 2
        </td>
        <td>
            The CDSS in return will pose questions to be answered by the patient through the EMS.
            <br>
            The CDSS should be able to make use of information already collected.
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
            Outcome or result (disposition) reached. 
            <br>
            The CDSS should be able to package up key data collected and post to the EMS as 'Provenance'.
            <br>
            This data should include the outcome of the CDSS flow i.e. a coded disposition or health need.
            <br>
            The session with CDSS is terminated.
        </td>
    </tr>
    <tr>
        <td>
            End
        </td>
        <td>
            The patient journey continues from the EMS
        </td>
    </tr>
</table>

The EMS will typically also manage elements like user authentication, workflow and user interactions which are considered 'out of scope' from the CDS API usage point of view.

<!-- 
## Messaging architecture overview 

<p style="text-align:center;"><a href="/images/cds-api-uec-system-architecture.png"><img src="/images/cds-api-uec-system-architecture.png" alt="Messaging architecture simplified representation" title="Messaging architecture simplified representation" style="width:75%"></a>
<br>
Messaging architecture simplified representation
</p>

### National Systems

PDS - [Personal Demographics Service](https://developer.nhs.uk/apis/uec-tech-standards/personal_demographics_service.html)

SCR - [Summary Care Record](https://developer.nhs.uk/apis/uec-tech-standards/summary_care_record.html)

CP-IS - [Child Protection - Information Sharing](https://digital.nhs.uk/services/child-protection-information-sharing-project)

RCS - [Repeat Caller Service](https://developer.nhs.uk/apis/uec-tech-standards/repeat_caller_service.html)

DoS - [Directory of Services](https://developer.nhs.uk/apis/uec-tech-standards/dos_in_iuc.html)

IDT - [Intelligent Data Tool](https://developer.nhs.uk/apis/uec-tech-standards/intelligent_data_tool.html)


### Messaging

PEM - [Post Event Message](https://developer.nhs.uk/apis/uec-tech-standards/post_event_messaging.html)

ITK - [Interoperability Toolkit](https://developer.nhs.uk/apis/uec-tech-standards/itk_overview.html)


### Local Systems

EMS - Encounter Management System

CDSS - Clinical Decision Support System
 -->