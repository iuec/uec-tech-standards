---
title: Clinical Decision Support API Demo Implementation
sidebar: overview_sidebar
permalink: cds-api-demo-implementation.html
toc: false
folder: emerging
---

## Demo application
For suppliers interested in understanding more about the CDS-API, a working demo of an Encounter Management System compliant to the [CDS-API standard](https://developer.nhs.uk/apis/cds-api/) is available at [http://uecdi-tom-emsui.s3-website.eu-west-2.amazonaws.com](http://uecdi-tom-emsui.s3-website.eu-west-2.amazonaws.com).

### Credentials to access the solution
`TODO: confirm credentials`
- Username: Guest
- Password: xxx

### Using the application

Once logged in, the home page will be displayed

`TODO: Update with current image`
<p style="text-align:center;"><a href="images/ems-demo-homepage.png"><img src="images/ems-demo-homepage.png" alt="The EMS Test Harness home page" title="The EMS Test Harness home page" style="max-width:100%"></a></p>

This gives a selection of patients and CDSS suppliers. The list of suppliers can be changed by going to Admin > Manage CDSS Suppliers. New suppliers can be added, removed or altered (using the Edit button). New scenarios can be added when editing a supplier but please note that new scenarios will not work unless the scenario is also added into the supplier stub database.

To run through a scenario you must 
- Begin on the Home page
- Select a patient by clicking on one of their names
- Select a test stub
- Once a stub is selected the user is given a list of service definitions
- Select the service definition you wish to run and click the Launch button.

When running through a scenario you will be presented with a series of questions. Answer the questions and click Continue until the scenario ends. Previous answers may be amended using the Back button. When the scenario ends the user is shown a suggested action or care plan. Start over by clicking on the Home link at the top of the page and selecting a new patient and supplier.

### Setup instructions 

The setup instructions for each application can be found in the corresponding public repositories:

[https://gitlab.com/ems-test-harness/ems-poc-public-v1](https://gitlab.com/ems-test-harness/ems-poc-public-v1)

## Demo Specification (1.0.0-alpha)

### EMS (Encounter Management System)

While helping to validate the EMS side of the CDS API specification, the EMS Test Harness application aims to provide the minimum functionality required to fulfil the following: 

The EMS enables the triage and clinical assessment of patients to determine their health needs and signpost them to the appropriate care setting or support the provision of clinical consultation and treatment; this is expected to be achieved through integration with one or more supporting systems and services.

### CDSS (Clinical Decision Support System) Stub

While helping to validate the CDSS side of the CDS API specification, the CDSS Stub application aims to provide the minimum functionality required to fulfil the following: 

A health information technology system that is designed to provide clinical and non-clinical UEC personnel undertaking triage or consultation, with clinical decision support (CDS); that is, assistance with clinical decision-making tasks.

### CDSS (Clinical Decision Support System) Pathways Stub

The CDSS Pathways Stub application aims to make use of the data included within the [NHS Pathways](https://digital.nhs.uk/services/nhs-pathways) application, to provide a much richer and more rigorous CDSS Stub that can be used to help better validate the CDSS side of the CDS API specification.

### Additional Functionality:

#### PCI (Post Call Information)

Enables the EMS to generate a 111 Patient consultation report page, from the "Handover Message" produced by the EMS at the end of the triage process.

#### ITK Validation Service

Enables the EMS to validate that the [Integrated Urgent Care Report](https://data.developer.nhs.uk/dms/IUC-3.0-RC1/Domains/IntegratedUrgentCare/Tabular%20View/POCD_RM200001GB02.html)/[Ambulance Request](https://data.developer.nhs.uk/dms/IUC-3.0-RC1/Domains/IntegratedUrgentCare/Tabular%20View/REPC_RM200001GB02.html) XML generated at the end of the triage process is valid.