---
title: Clinical Decision Support API Conformance Overview
sidebar: overview_sidebar
permalink: cds-api-conformance-overview.html
toc: true
summary: A summary of the conformance approach NHS Digital is taking for assessing Clinical Systems conformance to the CDS API Implementation Guide 1.0.
folder: business_capabilities
---

## Introduction
UEC System Suppliers must undergo a technical Conformance process to achieve CDS API Guide Conformance certification for their product. The purpose of CDS API Guide Conformance is for NHS Digital to validate that the developed product (Encounter Management System or Clinical Decision Support System) follows the <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/">CDS API Implementation Guide</a> and is compliant with the guidance.  System suppliers will have access to a detailed requirements list and a Toolkit Workbench through which simple tests are carried out, to provide the required evidence to NHS Digital.

View the <a href="https://developer.nhs.uk/apis/uec-tech-standards/cds-api-overview.html">CDS API overview</a> for further information on the CDS API Implementation Guide.

## Basic Technical Overview
The API service being assured is the technical message interaction between an Encounter Management System (EMS) and a Clinical Decision Support System (CDSS) using <a href="http://www.hl7.org/fhir/STU3/summary.html">FHIR STU3</a> as detailed in the <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/">CDS API Implementation Guide</a>. 

The CDS API Implementation Guide supports the following interactions for both the EMS and the CDSS acting as either consumer or provider:

<table>
  <tr>
    <th>Actor</th>
    <th>Read</th>
    <th>Search</th>
    <th>Create</th>
    <th>Update</th>
    <th>Delete</th>
  </tr>
  <tr>
    <td>Consumer</td>
    <td class="text-center"><i class="fa fa-check text-success"></i></td>
    <td class="text-center"><i class="fa fa-check text-success"></i></td>
    <td class="text-center"><i class="fa fa-check text-success"></i></td>
    <td class="text-center"><i class="fa fa-check text-success"></i></td>
    <td class="text-center"><i class="fa fa-times text-danger"></i></td>
  </tr>
  <tr>
    <td>Provider</td>
    <td class="text-center"><i class="fa fa-times text-danger"></i></td>
    <td class="text-center"><i class="fa fa-times text-danger"></i></td>
    <td class="text-center"><i class="fa fa-check text-success"></i></td>
    <td class="text-center"><i class="fa fa-check text-success"></i></td>
    <td class="text-center"><i class="fa fa-times text-danger"></i></td>
  </tr>
</table>


### Encounter Management System
An EMS is used for workflow management and to record, manage and track patient encounters of care through UEC settings. The EMS enables the triage and clinical assessment of patients to determine their health needs and signpost them to the appropriate care setting or support the provision of clinical consultation and treatment; this is expected to be achieved through integration with one or more supporting systems and services.

The EMS is responsible for invoking the decision support process on the CDSS. The EMS will typically also manage elements like user authentication, workflow and user interactions.

As per the <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/overview_concepts.html">CDS API Implementation Guide</a>, the EMS MUST be able to:

- Initiate the search and selection of a <code>ServiceDefinition</code>
- Initiate the evaluation of a <code>ServiceDefinition</code>
- Read appropriate resources from the CDSS (e.g. <code>Questionnaire</code>)
- Write (Create & Update) appropriate resources (e.g. <code>QuestionnaireResponse</code>)

The Encounter Management System MAY:
- Write (Create & Update) resources which are not core (e.g. <code>Condition</code>)

### Clinical Decision Support System
A Clinical Decision Support System (CDSS) is a health information technology system that is designed to provide clinical and non-clinical UEC personnel undertaking triage or consultation, with clinical decision support (CDS); that is, assistance with clinical decision-making tasks.

The CDSS is responsible for making clinical decisions, and communicating these as recommendations to the EMS.

As per the <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/overview_concepts.html">CDS API Implementation Guide</a>, the CDSS MUST be able to:

- Respond to filtered searches for <code>ServiceDefinition</code>
- Respond to evaluation of a <code>ServiceDefinition</code>
- Read appropriate resources from the EMS (e.g. <code>QuestionnaireResponse</code>)
- Write (Create & Update) appropriate resources (e.g. <code>Questionnaire</code>, <code>Observation</code>)

## Conformance Approach
As with all NHS Digital services, the approach to CDS API Guide Conformance must be efficient, appropriate to risk, and demonstrate clear reasoning and rationale.

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
        <p>The detailed conformance requirements list will be published on these pages of the NHS Digital developer site. The requirements list will detail all requirements that are needed to provide evidence against and achieve a passing level of conformance as determined by NHS Digital.</p>
        <p>A copy of the Toolkit Workbench Tool will be made available with test scripts for suppliers to develop their systems to, and generate conformance evidence.</p>
    </li>
    <li>
        <strong>Collect conformance evidence</strong><br>
        <p>Using the detailed requirements list Suppliers can collate their evidence. Evidence will be in the form of self-certifying statements and TKW log outputs.</p>
    </li>
    <li>
        <strong>Submit conformance evidence</strong><br>
        <p>Once evidence has been collected against the detailed requirements list this can be submitted to NHS Digital for assessment.</p>
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
        <p>The conformance process tests systems at a point in time. If a Supplier system has a version increment that affects the implementation of the CDS API Guidance in the product, then Suppliers can work with the Solutions Assurance team to retest the affected requirements in scope to achieve an uplift of the conformance status.</p>
    </li>
</ol>


## Pre-requisites for CDS API Guide Conformance
As per the <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/api_overview.html">CDS API Implementation Guide</a>:

Consumer / Provider Server API Conformance
<ul>
    <li>MUST support <a href="https://www.hl7.org/fhir/stu3/">HL7 FHIR STU3 version 3.0.1</a>.</li>
    <li>MUST Implement REST behaviour according to the <a href="http://www.hl7.org/fhir/STU3/http.html">FHIR specification</a>.</li>
    <li>MUST support XML <strong>or</strong> JSON formats for all API interactions.</li>
    <li>MUST expose a valid CDS FHIR <a href="https://www.hl7.org/fhir/STU3/capabilitystatement.html">CapabilityStatement</a> identifying the list of resources, operations and search parameters supported.</li>
</ul>

## Test requirements
Suppliers undergoing conformance testing are required to provide:

- Contact details of relevant individuals within the organisation
- Details of the product and deployment scenarios
- Technical API compliance evidence (the detailed requirements list will reference the automated tooling and associated tests to be executed)
- A declaration regarding clinical safety to confirm the obligations under [DCB0129 - Clinical Risk Management: its Application in the Manufacture of Health IT Systems](http://content.digital.nhs.uk/isce/publication/scci0129)


## Contact details

If you are an Urgent and Emergency Care technology supplier interested in achieving CDS API conformance for your product, please contact us at: <a href="mailto:enquiries@nhsdigital.nhs.uk">enquiries@nhsdigital.nhs.uk</a>

