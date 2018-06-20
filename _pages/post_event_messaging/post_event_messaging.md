---
title: Post Event Messaging
sidebar: overview_sidebar
keywords: ITK, pem, discharge
permalink: post_event_messaging.html
toc: true
folder: messaging
---

All encounters with the Integrated Urgent Care service must be followed up with a message back to the patient's registered GP surgery upon completion. This message is referred to as a Post Event Message (PEM).

## Requirements

### ITK should be used where possible
All areas must have plans in place to implement ITK within the GP systems. ITK is proven to reduce the workload on GP’s, as the current practice of using DTS increases workload on NHS 111, GP’s, and increases the amount of faxing within NHS 111 service in particular for Out of Area calls

### "For Action"  messages should contain the DoS Service ID
GP Primary Recipient messages must contain the Directory of Services (DoS) Service ID in the distribution envelope for routing purposes and the ODS code if it is available

### "For Information"  messages should contain the ODS Code
GP Copy Recipient messages must contain the Organisation Data Service (ODS) code in the distribution envelope for routing purposes and the DoS Service ID if it is available

### PEM should not be sent when the patient is referred to specific services e.g. Out of Hours  (OOH)
GP Copy Recipient messages must not be sent when successfully referring to OOH by the **urn:nhs-itk:interaction:primaryOutofHourRecipientNHS111CDADocument-v2-0** interaction, this should be determined by the DOS Service Type ID of GP Out of Hours. The current suppression of a copy message where it is the same GP as the primary message should continue to operate.

The PEM Suppression rules are [here](pem_suppression.html). Suppression should be built as configurable functionality within the application to ensure the suppression of PEM to any Service Type ID’s can be turned back on should it be required.

### PEM must contain the correct sections and headings
Within all CDA documents at the /ClinicalDocument/component/structuredBody/component/section/component/section element MUST contain the following items only in the order presented, using the titles (/ClinicalDocument/component/structuredBody/component/section/component/section/title) shown here, and appropriate text (/ClinicalDocument/component/structuredBody/component/section/component/section/text):

    a. Patient’s Reported Condition;

    b. Pathways Disposition (this should include selected service);

    c. Consultation Summary;

    d. Pathways Assessment;

    e. Advice Given

## Non ITK Transmission

In circumstances where ITK messaging is not yet available for PEM, the following mandatory requirements are specified:

**The CDA_NPfIT_Document_Renderer_NHS111.xsl renderer should no longer be used**

**For primary recipient messages NHS111_CDA_Renderer_PrimaryRecipients.xsl renderer must be used**

**For copy recipient messages NHS111_CDA_Renderer_CopyRecipients.xsl renderer must be used.**

The renderers are now available to the NHS 111 system vendors via the private repository used for distribution hosted on bitbucket.org.

These requirements are applicable for all transport mechanisms including email, DTS, and any other mechanism that is not ITK routed.

It is not acceptable to use Fax for PEM.
