---
title: Post Event Messaging
sidebar: overview_sidebar
keywords: ITK, pem, discharge
permalink: post_event_messaging.html
toc: false
folder: messaging
---

All encounters with the Integrated Urgent Care service must be followed up with a message back to the patient's registered GP surgery.


1. All areas must have plans in place to implement ITK within the GP systems. ITK is proven to reduce the workload on GP’s, as the current practice of using DTS increases workload on NHS 111, GP’s, and increases the amount of faxing within NHS 111 service in particular for Out of Area calls

2. GP Primary Recipient messages must contain the DoS Service ID in the distribution envelope for routing purposes and the ODS code if it is available;

3. GP Copy Recipient messages must contain the ODS code in the distribution envelope for routing purposes and the DoS Service ID if it is available;

4. GP Copy Recipient messages must not be sent when successfully referring to OOH by the **urn:nhs-itk:interaction:primaryOutofHourRecipientNHS111CDADocument-v2-0** interaction, this should be determined by the DOS Service Type ID of GP Out of Hours. The current suppression of a copy message where it is the same GP as the primary message should continue to operate.

5. Item 4 must be developed as a configuration item within the application to ensure the suppression of PEM to any Service Type ID’s can be turned back on should it be required.

6. Within all CDA documents at the /ClinicalDocument/component/structuredBody/component/section/component/section element MUST contain the following items only in the order presented, using the titles (/ClinicalDocument/component/structuredBody/component/section/component/section/title) shown here, and appropriate text (/ClinicalDocument/component/structuredBody/component/section/component/section/text):

    a. Patient’s Reported Condition;

    b. Pathways Disposition (this should include selected service);

    c. Consultation Summary;

    d. Pathways Assessment;

    e. Advice Given

### Non ITK Transmission

In all circumstances where ITK is not used the following requirements are mandatory.

This is applicable for all transport mechanisms including email, faxing, DTS or any other mechanism that is not ITK routed or is transmitted via an intermediary HUB:

1. The CDA_NPfIT_Document_Renderer_NHS111.xsl renderer should no longer be used;

2. For primary recipient messages NHS111_CDA_Renderer_PrimaryRecipients.xsl renderer must be used;

3. For copy recipient messages NHS111_CDA_Renderer_CopyRecipients.xsl renderer must be used.

The renderers are now available to the NHS 111 system vendors via the private repository used for distribution hosted on bitbucket.org.
