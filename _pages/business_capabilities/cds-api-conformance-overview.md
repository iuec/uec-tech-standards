---
title: Clinical Decision Support API Conformance Overview
sidebar: overview_sidebar
permalink: cds-api-conformance-overview.html
toc: true
summary: A summary of NHS Digital's Conformance Approach for assessing a System's conformance to the CDS API Implementation Guide.
folder: business_capabilities
---

## Introduction
The CDS API Conformance Approach can be used to validate whether or not a developed product is compliant with the [CDS API Implementation Guide](https://developer.nhs.uk/apis/cds-api/).

It allows NHS Digital to validate that a developed product follows guidance correctly, and therefore is likely to be compatible with other systems using the standard. Suppliers that successfully complete the Technical Conformance process will be granted CDS API Guide Conformance certification for their product. These systems and suppliers will also be listed on NHS Digital’s [Conformance Catalogue](https://digital.nhs.uk/services/interoperability-toolkit/conformance/conformance-catalogue).

The approach centres around suppliers using a requirements list and then providing the required evidence to NHS Digital for assessment. Technical tooling will be provided by NHS Digital to help with the execution of test cases to demonstrate the requirements have been met. Evidence will be in the form of both test tooling log outputs and self-certifying statements.

The CDS API Conformance Approach will be applied to both Encounter Management Systems (EMS) and Clinical Decision Support Systems (CDSS).

Please view the [CDS API overview](https://developer.nhs.uk/apis/uec-tech-standards/cds-api-overview.html) for further information on the CDS API Implementation Guide.


## Basic Technical Overview
The API service being assured is the technical message interaction between an Encounter Management System (EMS) and a Clinical Decision Support System (CDSS) using [FHIR STU3](http://www.hl7.org/fhir/STU3/summary.html) as detailed in the [CDS API Implementation Guide](https://developer.nhs.uk/apis/cds-api/). 

### Encounter Management System
An Encounter Management System (EMS) is used for workflow management and to record, manage and track patient encounters of care through Urgent and Emergency Care (UEC) settings.

The EMS enables the triage and clinical assessment of patients to determine their health needs. It will then signpost them to the appropriate care setting or support the provision of clinical consultation and treatment. This patient journey is expected to be achieved through integration with one or more supporting systems and services.

The EMS is responsible for invoking the decision support process on the Clinical Decision Support System (CDSS). The EMS will typically also manage elements like user authentication, workflow and user interactions.

As per the <a href="https://developer.nhs.uk/apis/cds-api/overview_concepts.html">CDS API Implementation Guide</a>, the EMS MUST be able to:

- Initiate the search and selection of a <code>ServiceDefinition</code>
- Initiate the evaluation of a <code>ServiceDefinition</code>
- Read appropriate resources from the CDSS (e.g. <code>Questionnaire</code>)
- Write (Create & Update) appropriate resources (e.g. <code>QuestionnaireResponse</code>)

The Encounter Management System MAY:
- Write (Create & Update) resources which are not core (e.g. <code>Condition</code>)

### Clinical Decision Support System
A Clinical Decision Support System (CDSS) is a health information technology system that is designed to provide clinical decision support (CDS); that is, assistance with clinical decision-making tasks. A CDSS may provide this support to clinical and non-clinical UEC personnel undertaking triage or consultation.

The CDSS is responsible for making clinical decisions, and communicating these as recommendations to the EMS.

As per the <a href="https://developer.nhs.uk/apis/cds-api/overview_concepts.html">CDS API Implementation Guide</a>, the CDSS MUST be able to:

- Respond to filtered searches for <code>ServiceDefinition</code>
- Respond to evaluation of a <code>ServiceDefinition</code>
- Read appropriate resources from the EMS (e.g. <code>QuestionnaireResponse</code>)
- Write (Create & Update) appropriate resources (e.g. <code>Questionnaire</code>, <code>Observation</code>)

## Conformance Approach
As with all NHS Digital services, the approach to CDS API Guide Conformance must be efficient, appropriate to the level of risk involved, and demonstrate clear reasoning and rationale.

Efficiency, appropriateness, and flexibility are key areas that have been considered when developing this conformance approach, examples being:

- Efficiency by minimizing burden on the UEC Technology suppliers by providing test tooling capabilities, demo implementations and development guidance where possible
- Appropriateness by mapping the technical compliance task to predetermined risks.


## Journey process
The illustration below summarises the key stages and activities a UEC Technology supplier will go through in the conformance journey.

<p style="text-align:center;">
    <a href="images/cds-api-conformance-process-overview.jpg">
        <img src="images/cds-api-conformance-process-overview.jpg" alt="A process diagram detailing the key stanges and activities a UEC Technology supplier will go through in the conformance journey" title="CDS API Conformance process overview" usemap="#conformance-process-overview">
    </a>
</p>

<ol>
    <li>
        <strong>Check published conformance requirements</strong><br>
        <p>Details of the conformance process are published on NHS Digital website for Suppliers to understand the requirements and determine the feasibility of completion.</p>
    </li>
    <li>
        <strong>Access conformance resources</strong><br>
        <p>The conformance requirements list will be published on these pages of the NHS Digital developer site. The requirements list will detail all requirements that are needed to provide evidence towards a passing level of conformance.</p>
        <p>Access to technical tooling will be made available with test scripts for suppliers to develop their systems to, and generate conformance evidence.</p>
    </li>
    <li>
        <strong>Collect conformance evidence</strong><br>
        <p>Using the conformance requirements list Suppliers can collate their evidence. Evidence will be in the form of self-certifying statements and TKW log outputs.</p>
    </li>
    <li>
        <strong>Submit conformance evidence</strong><br>
        <p>Once evidence has been collected against the requirements list this can be submitted to NHS Digital for assessment.</p>
        <p>There may be a period of iteration where Suppliers will revise the submitted evidence until it satisfies our team.</p>
        <p>At the end of the conformance assessment process a report is generated with details of the tests.</p>
    </li>
    <li>
        <strong>Achieve conformance certificate</strong><br>
        <p>Upon passing the assessment criteria a conformance certificate is provided to the Supplier. This can be shared with provider agencies as conformance evidence.</p>
        <p>Conformant systems will also be published to the <a href="https://digital.nhs.uk/services/interoperability-toolkit/conformance/conformance-catalogue">Conformance catalogue</a> on the NHS Digital website.</p>
        <p>The Conformance catalogue is a way to identify all vendors and products that have been awarded Solution Assurance Conformance Certificates.</p>
    </li>
    <li>
        <strong>Tell us of any material change after go live</strong>
        <br>
        <p>The conformance process tests systems at a point in time. If a Supplier system has a version increment that affects the implementation of the CDS API Guide in the product, then Suppliers can work with the Solutions Assurance team to retest the affected requirements in scope to achieve an uplift of the conformance status.</p>
    </li>
</ol>

## Requirements list and technical tooling
Development of the conformance requirements and technical tooling for suppliers to execute test cases to generate evidence is currently underway. These will be linked to from these pages once available for circulation.

The test tooling will provide various technical test features, including the ability to validate HTTP headers, JWT, and FHIR base/profiled resources. The test tooling will also act as a technical HTTP endpoint stub, with pre-configured responses based on specific triggers.

We welcome suppliers wishing to engage with the Conformance approach to contact us via the CDS API [Communication Channels](https://developer.nhs.uk/apis/cds-api/support_communications.html) to access these resources. 


## Pre-requisites for CDS API Guide Conformance

Pre-requisites for CDS API Guide conformance can be viewed on the [pre-requisites](https://developer.nhs.uk/apis/cds-api/api_prerequisites.html) page.



## Test requirements
Suppliers undergoing conformance testing are required to provide:

- Contact details of relevant individuals within the organisation
- Details of the product and deployment scenarios
- Technical API compliance evidence (the detailed requirements list will reference the automated tooling and associated tests to be executed)
- A declaration regarding clinical safety to confirm the obligations under [DCB0129 - Clinical Risk Management: its Application in the Manufacture of Health IT Systems](http://content.digital.nhs.uk/isce/publication/scci0129)



## Scope of the Conformance Approach
The scope of the CDS API Conformance Approach is assuring that a system conforms to V1.1.1 of CDS API Implementation Guide. As such, it solely covers technical certification of a given product to this standard.

## Out of scope of the Conformance Approach
The following areas are out of the scope of the Implementation Guide and Conformance. We have provided useful links to assist individuals in making their own judgements on what additional assessments and accreditation may be needed.

### Clinical safety and risk
The Conformance Approach requires a declaration regarding clinical safety to confirm the obligations under [DCB0129 - Clinical Risk Management: its Application in the Manufacture of Health IT Systems](https://digital.nhs.uk/data-and-information/information-standards/information-standards-and-data-collections-including-extractions/publications-and-notifications/standards-and-collections/dcb0129-clinical-risk-management-its-application-in-the-manufacture-of-health-it-systems). However, management of clinical safety and risk his remains the responsibility of system manufacturers, which should seek assessments and accreditation appropriate for the nature and use of their product.

Useful links:

- NHS Digital: [DCB0160: Clinical Risk Management: its Application in the Deployment and Use of Health IT Systems](https://digital.nhs.uk/data-and-information/information-standards/information-standards-and-data-collections-including-extractions/publications-and-notifications/standards-and-collections/dcb0160-clinical-risk-management-its-application-in-the-deployment-and-use-of-health-it-systems)

### Medical Device assessment and regulation
It is the responsibility of system manufacturers to ensure that any assessment or regulation of their product as a potential Medical Device is carried out.

Useful links:

- Medicines and Healthcare products Regulatory Agency: [Medical devices regulation and safety](https://www.gov.uk/topic/medicines-medical-devices-blood/medical-devices-regulation-safety)
- Medicines and Healthcare products Regulatory Agency: [Medical device stand-alone software including apps](https://www.gov.uk/government/publications/medical-devices-software-applications-apps)

### Security
The Implementation Guide features guidance on how an API should identify authorised access to an endpoint. However, this is just one aspect of information security and it remains the responsibility of system manufacturers to ensure safe and suitable security practices are followed.

### Information Governance
Appropriate handling, storage and consents around patient and system data remain the responsibilities of system manufacturers.

Useful links:
- Gov.UK [Caldicott review: information governance in the health and care system](https://www.gov.uk/government/publications/the-information-governance-review)
- Information Commissioner’s Office: [Guide to the General Data Protection Regulation (GDPR)](https://ico.org.uk/for-organisations/guide-to-data-protection/guide-to-the-general-data-protection-regulation-gdpr/)

## Contact details

To begin the process contact us at: <a href="mailto:uecdi@nhs.net">uecdi@nhs.net</a>

