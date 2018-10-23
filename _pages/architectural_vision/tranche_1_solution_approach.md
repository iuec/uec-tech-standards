---
title: Tranche 1 Solution Approach
sidebar: overview_sidebar
keywords: architecture
permalink: tranche_1_solution_approach.html
toc: false
toc_h3: true
folder: architectural_vision
---

## Introduction

###	Background
The Clinical Triage Platform (CTP) programme supports the delivery of the key recommendations and drivers for change that resulted from a number of NHS strategies, policies, frameworks and reviews, including the NIB Health & Care 2020 framework, the Urgent and Emergency Care Review, and the Five Year Forward View. To achieve the transformation of Urgent and Emergency Care (UEC) people need to be directed or connected with the right service to meet their needs and not be sent or conveyed to high end dispositions such as Accident and Emergency (A&E) or GP’s unless absolutely necessary.

###	Purpose
The purpose of this document is to provide third party suppliers with the view of the Solution approach to Tranche 1 of CTP delivery.

The solution approach details the agreement and specification of the highest priority set of CTP Platform APIs covering decoupling of the CDSS and use of Patient Records (input Data) during the triage process.

This will include engagement with the market and stakeholders on potential solutions.

###	Scope
The scope of the document is defining the approach to identifying and developing the solution for the first delivery tranche (of 3).  Specifically, this includes the following deliverables of the CTP Programme:
<ul>
	<li>
		Documented interoperability specifications which support the personalisation of triage
	</li>
	<li>
		Documented CDSS decoupling API specification
	</li>
</ul>
Note that the specifications delivered by NHS Digital will be based on open standards.  The delivery date for the specifications is end of September 2018.

Note that delivery and migration of appointment booking is in the scope of Access to Service Information (A2SI) programme.

#### Exclusions
This document does not define UEC or CTP interoperability artefacts, nor the commercial, legal or governance frameworks for adopting or assuring conformance to processes, APIs or standards.  Note also that the following elements are explicitly out of scope of this document:

<ul>
	<li>
		Appointment booking and the Directory of Services – these are in the scope of the Access to Service Information (A2SI) programme
	</li>
	<li>
		Migration of existing NHS Digital national services unless specifically stated.
	</li>
	<li>
		Any common platform services such as service management and security management
	</li>
	<li>
		Functional services concerned with the support processes, for example workforce management.
	</li>
	<li>
	The mechanics of any Market Engagement process or procurement.
</li>
</ul>

###	Intended Document Audience
This document is intended for use by NHS England, the CTP programme team and suppliers engaged on the Clinical Triage Platform.

## Executive Summary
The first tranche of delivery for the Clinical Triage Platform programme will deliver a specification for a modular solution for service providers, where the Clinical Decision Support System can be implemented separately from the Encounter Management System, and a number of CDSS may be used with a single EMS.  This will mean more choice for providers, and a more open market for suppliers.

The process to final delivery of programme benefits is outlined in the sections in this paper.  The process consists of the following five steps:
<ol>
<li>
NHS Digital will define the scope of tranche 1 – this has been done, and is detailed in the <a href="#scope-definition">scope definition</a> section
</li>
<li>NHS Digital will develop a specification with suppliers which will allow CDSS and EMS systems to work together.</li>
<li>
Following the publishing of this specification, system suppliers will be able to develop new versions of their applications (or entirely new applications) in line with the new specification.
</li>
<li>
NHS Digital will establish a process for CDSS to be made available on the framework.  This will ensure that the CDSS are compliant with the specifications, and fit for purpose.  Suppliers will be able to place their CDSS on the framework.
</li>
<li>
Service providers will be able to purchase and implement CDSS from the framework which will enable the benefits specified in the programme business case to be realised.
</li>
</ol>

In addition, personalisation of the triage process will mean that information already known about the patient can be used during the triage process.

The CTP programme will publish specifications for the personalisation of triage, and for the decoupling of CDSS from EMS, which can then be developed against by suppliers.  Once developed, systems will undergo an agreed assurance process which will lead to the system being eligible for inclusion on a commercial framework from which providers can purchase with confidence.

The CTP programme will work closely with suppliers and providers through the development, framework and implementation stages, to ensure that the initial tranche of CTP delivery is successful, and delivers the benefits specified in the CTP programme business case.

The CTP programme are engaging with system suppliers, through a series of Proof of Concepts, to create the specifications. The programme will also work with standards development organisations, such as <a href="https://www.interopen.org/">InterOPEN</a> and <a href="https://theprsb.org/">PRSB</a>, to ensure that the specifications are open, appropriate and will serve for future development.
The CTP programme will publish the initial version of the tranche 1 specifications by the end of September 2018, and will consult the market at that point before issuing further versions.

## CTP Roadmap
The CTP capability will deliver incrementally to support the release phases of the programme and will continue through to the end of the CTP programme and beyond.  At the end of the programme, the CTP will be set up to enable continuous evolution and the adoption of new products and suppliers.

This staged release approach allows the initial delivery of CTP to provide the capability required to meet the baseline needs whilst enabling iterative increments in capability to deliver the future state in a controlled manner whilst maximising initial investment without the overhead of unused functionality.

To implement this approach, the architecture must be designed with future growth in mind and enables future increments to “fail fast” without detriment to the existing capability and accommodate inevitable changes to the roadmap towards the target state over time.

###	Overview

<p style="text-align:center;"><a href="images/ctp_tranche_1_solution_approach_evolution_of_ctp.png"><img src="images/ctp_tranche_1_solution_approach_evolution_of_ctp.png" alt="Table 1: Evolution of CTP" title="Table 1: Evolution of CTP" style="width:75%"></a>
<br>
Table 1: Evolution of CTP
</p>


The CTP roadmap currently has three tranches of delivery, as illustrated below.

### Tranche 1 – Enable

<p style="text-align:center;"><a href="images/ctp_tranche_1_solution_approach_tranche_1.png"><img src="images/ctp_tranche_1_solution_approach_tranche_1.png" alt="Figure 1: Tranche 1" title="Figure 1: Tranche 1" style="width:75%"></a>
<br>
Figure 1: Tranche 1
</p>

In tranche 1, the initial work to input data for personalisation of triage will be implemented through interoperability standards to provide access to records.  The CDSS triage logic will be decoupled from the Encounter Management Systems.

Personalisation of the triage process will be piloted.

### Tranche 2 – Improve

<p style="text-align:center;"><a href="images/ctp_tranche_1_solution_approach_tranche_2.png"><img src="images/ctp_tranche_1_solution_approach_tranche_2.png" alt="Figure 2: Tranche 2" title="Figure 2: Tranche 2" style="width:75%"></a>
<br>
Figure 2: Tranche 2
</p>

In tranche 2, the Access to Service Information programme will provide a national appointment broker for dispositions.  Clinical data will be extended through the Access to Records programme to include more sources of clinical information, including local records.  Third party CDSS, compliant to the decoupling API, will be available as an alternative to Pathways.

Predictive Modelling of Patient Risk will be piloted during this phase.

###	Tranche 3 – Innovate
<p style="text-align:center;"><a href="images/ctp_tranche_1_solution_approach_tranche_3.png"><img src="images/ctp_tranche_1_solution_approach_tranche_3.png" alt="Figure 3: Tranche 3" title="Figure 3: Tranche 3" style="width:75%"></a>
<br>
Figure 3: Tranche 3
</p>

During the third tranche, triage logic in CDSS will be more widely used by other UEC care settings.  The PMPR service will be available to all services, and updates to clinical content will be driven by innovative processes such as NLP.  Triage outcomes will be easily shared to all UEC end-points, providing a seamless journey for patients as they move from initial contact to resolution.

## Scope Definition
The scope definition of tranche 1 of the CTP is given below.  The scope of tranche 1 is the decoupling of the CDSS from the EMS and use of personalised information during triage where available.

<p style="text-align:center;"><a href="images/ctp_tranche_1_solution_approach_tranche_1.png"><img src="images/ctp_tranche_1_solution_approach_tranche_1.png" alt="Figure 4: Tranche 1" title="Figure 4: Tranche 1" style="width:75%"></a>
<br>
Figure 4: Tranche 1
</p>

In tranche 1, the initial work to input data for personalisation of triage will be implemented through interoperability standards to provide access to records.  This is applicable where structured data sets exist.  The CDSS triage logic will be decoupled from the Host Provider systems.  Personalisation of the triage process will be piloted.

###	Architecture Overview

<p style="text-align:center;"><a href="images/ctp_tranche_1_solution_approach_tranche_1_architecture.png"><img src="images/ctp_tranche_1_solution_approach_tranche_1_architecture.png" alt="Figure 4: Tranche 1" title="Figure 4: Tranche 1" style="width:75%"></a>
<br>
Figure 5: Tranche 1 Architecture
</p>

The figure above shows the technical architecture outline of the CTP solution architecture in tranche 1.

###	Encounter Management Systems (EMS)
#### Overview
The EMS will be multi-vendor and there will not be a single national instance for the EMS, with a logical instance for each UEC service provider.  Note particularly that EMS will be available in care settings through Urgent & Emergency Care, such as Emergency Departments, Urgent Treatment Centres, Out of Hours GPs, Minor Injury Units as well as the current 111 and 999 service providers.

The requirements, and delivery, of EMS may vary between care settings based on the local needs.  For example, an EMS in an Emergency Department or GP Surgery may have greater access to local care information.

EMS are logically distinct from the person engagement systems (e.g. current 111 phone provider systems use CTI and a call handler to link the EMS to the phone call) but can embed different person engagement systems as needed.  The link between EMS and Person Engagement is left for supplier definition, and no definition will be provided.

#### Interoperability
The EMS must interoperate with one or more decoupled CDSS.

The EMS must interoperate with a variety of national systems.

The EMS must report data to the centralised data repository.

#### Data
The EMS will store much of the data associated with the triage journey, and will be responsible for data reporting functions.  In particular, the host system must be able to identify frequent callers (as distinct from repeat callers).

#### Physical
EMS are typically deployed locally and with an instance for each provider, though there are exceptions.  It is expected that EMS may have a variety of physical implementations, including multi-tenant services, and some deployed as SaaS.

###	Clinical Decision Support System
#### Overview
The CDSS component will be multi-vendor. The CDSS instances will be procured by each service provider.  A given service provider can have one or more CDSS, depending on the scope of functionality provided, the users supported, and the speciality modules needed.  In order to support the set of requirements around different specialities and different users, it is anticipated that most providers will have a range of CDSS.  Note also that different versions of the same CDSS can be used by a single provider, where user training levels make this a preferred solution.

The CDSS must integrate with any of the UEC Care Settings, and the EMS for that care setting.

#### Interoperability
The CDSS must interoperate with the EMS.  It must also interoperate with other CDSS, though this will be brokered through the EMS.
The CDSS may have the option to interoperate with the wider national systems.
#### Data
The CDSS stores and retains a set of clinical content rules which guide the triage process to an outcome.  The CDSS does not store any operational information.  It is generally considered to be stateless.
#### Physical
It is expected that most providers will manage locally the CDSS which they license.  However, it is left for suppliers to determine their own delivery method.

## Specification Creation
The sections below describe the activities being undertaken for each of the platform components to deliver specifications.
### CDSS Decoupling
There are three phases of work in the CDSS decoupling workstream – work to prepare an initial draft of the specification, work to ratify the draft with appropriate groups and then publishing the specification.  This is illustrated in Figure 6 below:

<p style="text-align:center;"><a href="images/ctp_tranche_1_solution_approach__CDSS_decoupling.png"><img src="images/ctp_tranche_1_solution_approach__CDSS_decoupling.png" alt="Figure 6: CDSS Decoupling" title="Figure 6: CDSS Decoupling" style="width:75%"></a>
<br>
Figure 6: CDSS Decoupling
</p>

#### Proofs of Concept
A PoC to test a decoupled CDSS working with a separate EMS (or test harness) and a second CDSS has been defined and shared with existing CDSS suppliers that support a telephony channel.  The programme will work with as many of the suppliers as possible in parallel to test both existing integration approaches, and the HL7 FHIR standard for CDS interoperability.

The starting assumption is that HL7 FHIR is the appropriate open standard that the specification will be based on.  This is based on the NHS Digital policy for APIs & messaging (NAT-API-001).  Any specifications already in use by suppliers will also be assessed.

The PoC will be considered successful if it has proved or disproved the success criteria outlined below.

##### Demonstrated decoupling with an open standard
This criterion will be met if at least one CDSS supplier can provide a CDSS which can carry out at least one patient triage journey, decoupled from the EMS, with conformance to a clearly defined open standard.

##### CDSS Switching - receive
This criterion will be met if at least one CDSS supplier demonstrates the capability to pick up a patient triage journey partway through without requesting information which has already been provided.

##### CDSS Switching - pass
This criterion will be met if at least one CDSS supplier demonstrates the capability to pass on a patient triage journey partway through while providing all information which has been collected.

Following the conclusion of the PoCs, an assessment exercise will drive the first draft of the specification.

For full details of the Decoupling Proof of Concept, see <a href="_pages/architectural_vision/CDSS_Proof_of_Concept_FINAL_v.1.0.docx">CDSS Proof of Concept v1.0</a>.

Following the successful proofs of concept, and the other stages below, the specification will be made available for suppliers to develop against.

#### Passing of structured data for personalisation
The specification for decoupling will cover the data required by the CDSS.  Although most of this information will be supplied by the patient, some may come from existing sources of data (see the <a href="#personalisation-of-triage">Personalisation of Triage</a> section for full details) and the specification will include this structured data.

#### End user engagement
The wider user community of service providers and commissioners will be engaged to ensure that the proposed technology specification will meet the operational needs of providers and commissioners.

#### Technical Ratification
The initial draft of the specification will be shared with existing standards bodies, including InterOPEN and PRSB, as well as with system suppliers, to ensure that the specification is fit for purpose in the widest possible context.
The relationship between NHS Digital and InterOPEN is managed through the NHS Digital Interoperability and Architecture programme.  The CTP programme will manage the engagement with InterOPEN through this programme.

#### Publish
The agreed initial release of the specification for CDSS decoupling will be published in accordance with the normal NHS process, through the developer.nhs.uk website.

### Personalisation of Triage
The personalisation of triage stream has two elements – one is testing to see if personalising the triage process is possible and leads to improvement, and the other is the identification and testing of structured patient data sources’.

<p style="text-align:center;"><a href="images/ctp_tranche_1_solution_approach_personalisation_of_triage.png"><img src="images/ctp_tranche_1_solution_approach_personalisation_of_triage.png" alt="Figure 7: Personalisation of Triage" title="Figure 7: Personalisation of Triage" style="width:75%"></a>
<br>
Figure 7: Personalisation of Triage
</p>


#### Proof of Concept
A PoC has been running to test that use of personalised data improves the triage process (as tested in a test environment against a Live Service environment).  The assessment at the conclusion of the PoC will form part of the specification for personalisation.

The success criteria of the PoC are shown below:

##### Personalised Triage Functionality Specifications
The primary success criteria for the PoC will be establishing which of the requirements listed in the PoC document are possible within CDSS solutions. All requirements should be considered in scope for development and further discovery but will be discussed with suppliers on a case-by-case basis to fit with their existing expertise.
##### Personalised Triage Data Specifications
The POC should establish the Personalised Data Specifications baseline for CTP against which future CDSS should be implemented. These data specifications will incorporate the learning from integrating structured records within the test environment and the modification of triage pathways or consultations based on patient data within the supplier CDSS.  Further details on the format for this specification will be contained within the CTP Data Specification documentation.
##### Personalised Triage Pathways
The PoC should look to demonstrate which care pathways and consultation scenarios exhibit the best examples for the incorporation of personalised data to directly inform triage. There is no quantity associated with this success criteria although it is expected there will be a number of pathways identified which can then be either examined in future PoCs or built upon by suppliers as part of their product offering.  Identifying the care pathways amenable to personalisation will drive market innovation and the development of new products.
For full details of the Personalisation Proof of Concept, see <a href="_pages/architectural_vision/Personalised_Triage_SUPPLIER_Proof_of_Concept_v2.0.docx">Personalised Triage SUPPLIER Proof of Concept v2.0</a>

#### Pilots of existing structured data sources
The programme is working with a set of existing providers of structured clinical data (including the Medical Interoperability Gateway and Redwood technology) to identify how clinical structured data that could be of use in improving the triage process (such as conditions) can be made available to service provider implementations.  This will also feed into the initial specification.
#### Acccess to Records
Access to structured clinical information is being pursued in areas other than Urgent & Emergency Care.  NHS Digital are currently working on a separate programme (Access to Records) which has the aim of providing all clinical information in a structured form wherever it is needed.  As the requirements of the personalised triage process are further refined, these will continue to be fed into the A2R programme.

## Component Development
### Local System suppliers
Following the publishing of the specifications, the market place of system suppliers will be able to develop new versions of their applications, or entirely new applications, which will conform to the specification.

One of the key aims of the CTP programme is to widen access to the current supplier market for UEC service providers.  The Encounter Management System (EMS) and Clinical Decision Support System (CDSS) components are both intended to have multiple third party suppliers delivering these components.

The two components of the CTP which will need development to meet the new tranche 1 specification are the EMS and the CDSS.  These will be developed by third party suppliers to the specification provided by NHS Digital.

The CTP programme will support any third party suppliers with guidance on the published specifications, and the associated assurance processes.

For early adoption supplier, this assistance will be greater than later in the process.

### National systems
None of the national system platform components (Repeat Caller Service, Intelligent Data Tool) are directly impacted by the decoupling or personalisation changes.

## Framework Process
### Overview
The framework process for tranche 1 is primarily intended for CDSS suppliers, and will be managed in alignment with the creation of a purchasing framework for CDSS suppliers and UEC service providers.

NHS Digital will specify the functional modules which suppliers and providers can use.  Different modules may have different criteria to meet.

The key areas that will be addressed during the process are outlined below.

### Technical Assurance
Technical assurance, performed by NHS Digital, will test that a system is conformant with the specification as published.  Each specification will include the necessary assurance process.

### Clinical Assurance
There are two main areas for clinical assurance. The first relates to assurance of the clinical content of the CDSS and its use in practice and the second relates to compliance with the relevant regulations and standards e.g. <a href="https://www.gov.uk/guidance/medical-devices-eu-regulations-for-mdr-and-ivdr">Medical Device Regulations</a> and <a href="https://digital.nhs.uk/data-and-information/information-standards/information-standards-and-data-collections-including-extractions/publications-and-notifications/standards-and-collections/dcb0129-clinical-risk-management-its-application-in-the-manufacture-of-health-it-systems">DCB0129 Clinical Risk Management: its Application in the Manufacture of Health IT Systems</a>.

The clinical assurance process will be agreed by the Digital Urgent and Emergency Care (DUEC) board.

### IG Assurance
Information Governance assurance covers the information security and standards for the system components.  IG assurance will be aligned with the <a href="https://digital.nhs.uk/data-and-information/looking-after-information/data-security-and-information-governance/data-security-and-protection-toolkit">NHS Data Security & Protection Toolkit</a>, and must also be compliant with relevant legislation – including GDPR, and patient consent to share.

### Commercial assurance
In order to be listed on the framework, the supplier will need to undergo appropriate commercial assurance.  This is being led by the CTP team, and will be aligned with existing commercial assurance processes used within the NHS.

## Implementation
As systems are accepted onto the framework, they will become available for implementation by service providers.  NHS Digital will have a purchasing framework for CDSS.  This will enable service providers to choose from the marketplace of CDSS suppliers with confidence.

EMS applications will not be added to the framework by NHS Digital in the same way as CDSS.  However, providers will need an EMS which conforms to the published specification to use conformant CDSS to their greatest benefit.

The CTP programme will support any service providers with their implementation of CTP compliant components.  For first of type, and early adoption providers, this assistance will be greater than later in the process.

## Appendix A.	Enterprise & Organisation landscape
It is important to note that the implementation of the Clinical Triage Platform is in a landscape which has a number of independent enterprises.  This necessarily informs much of this document, so a short overview is provided below:
### Overview
The business architecture presented is for the Urgent & Emergency Care setting within the NHS.  The organisations are subject to change, particularly with reference to the NHS England Integrated Urgent Care Service Specification.  Full details for the operating models for 111 call handling and the Clinical Assessment Service (CAS) are in the NHS England service specification.
### Patients
Patients access Urgent & Emergency Care when a health issue causes an immediate health need.  This results in the patient (or a third-party representative) contacting an appropriate UEC service.  Most of these contacts are through the 111 services.  The other channels include 999, walk-in to ED, walk-in to Urgent Treatment Centres, or walk-in to Minor Injury Units.  Patients may have their health need satisfied by the service that they first contacted, or they may be transferred to another service (which has agreed to accept transfers).

Patients have a choice of which service provider they initially contact.  Although this can be influenced through various factors (advertising, nudges, etc.), a patient can choose any service which accepts direct contact (111, 999, ED, UTC, MIU etc.)
### Providers
Within the UEC landscape, provider organisations can deliver triage assessments, or clinical assessments, or both.  Any provider which accepts direct contact (without clinical referral) from the public will typically do some form of triage assessment.

The Integrated Urgent Care model moves providers to a single organisational model which provides both triage assessment, and clinical assessment (the target being 50% of contacts have a clinical assessment in the initial service).

Providers are awarded contracts by commissioners to deliver services.  Providers include NHS organisations, social care enterprises and may include commercial organisations where this is covered by the Any Qualified Provider (AQP) initiative.

Providers are the primary users (and hence buyers) of ICT systems in the UEC landscape.  Providers will hold the commercial relationship with local system suppliers.

Providers are in the process of moving from either being triage providers (111, 999) or clinical consultation providers (ED, UTC, OoH GPs) to being both.

### Commissioners
Service commissioners will commission providers for services in an area; monitor the delivery of that service, through management information reporting; and define where it is appropriate to transfer patients between different service providers.

Commissioners can include local requirements, but must follow central guidance issued by NHS England.

Commissioners can also contract with system suppliers (normally through Commissioning Support Units (CSU)) where a regional contract makes sense.  However, this is uncommon in UEC.

### NHS England
NHS England publish the service specifications which commissioners then contract providers to supply.  NHS England are the primary commercial entity (budget holders) and money is funnelled to commissioners.  NHS England hold a regulatory responsibility to monitor how commissioners are contracting providers of services.

NHS England can also contract with system suppliers for national (England) systems – this will typically be with NHS Digital (though can be with commercial suppliers).

### System Suppliers
System suppliers can be contracted to provide IT systems by any of the enterprises in the UEC landscape.  System suppliers are mostly engaged at the local (provider) level.  Suppliers are typically involved in release management, and service management, though this can be contracted to separate organisations.

NHS Digital are a system supplier (and also perform service management & release management functions) for national systems, including PDS, RCS and Pathways Outcome Reporting.

## Appendix B.	Interoperability Standards
### NHS Digital Interoperability and Architecture programme
NHS Digital deliver technical standards and capabilities to enable health and care professionals to share and access patient information across all care settings.
<ul>
	<li>
		<a href="https://digital.nhs.uk/about-nhs-digital/our-work/transforming-health-and-care-through-technology/integrated-care-domain-d/interoperability-and-architecture">https://digital.nhs.uk/about-nhs-digital/our-work/transforming-health-and-care-through-technology/integrated-care-domain-d/interoperability-and-architecture</a>
	</li>
</ul>
### INTEROpen community
An OPEN collaboration of individuals, industry, standards organisations and health and care providers, who have agreed to work together to accelerate the development of open standards for interoperability in the health and social care sector.
<ul>
	<li>
		<a href="http://www.interopen.org/standards-development-overview/">http://www.interopen.org/standards-development-overview/</a>
	</li>
</ul>

### NHS England interoperability strategy
The NHS England Interoperability Handbook is one of a number of resources being published by NHS England to support the Interoperability Strategy. It includes criteria by which procured and commissioned solutions should be assessed, including openness.
<ul>
	<li>
		<a href="https://www.england.nhs.uk/wp-content/uploads/2017/03/interoperabilty-handbk.pdf">https://www.england.nhs.uk/wp-content/uploads/2017/03/interoperabilty-handbk.pdf</a>
	</li>
	<li>
		<a href="https://www.england.nhs.uk/digitaltechnology/info-revolution/health-and-care-data/interoperability/">https://www.england.nhs.uk/digitaltechnology/info-revolution/health-and-care-data/interoperability/</a>
	</li>
</ul>
### GOV.UK
A cabinet office policy paper published in April 2018 explains how the government selects open standards for software interoperability, data and document formats in government IT. It also guides departments on how to implement open standards.
<ul>
<li>
	<a href="https://www.gov.uk/government/publications/open-standards-principles/open-standards-principles">https://www.gov.uk/government/publications/open-standards-principles/open-standards-principles</a>
</li>
</ul>
### The open group
The Open Group use collaborative working groups to develop open, vendor-neutral, technology standards. Their processes for developing standards is open and published:
<ul>
	<li>
		<a href="https://www.opengroup.org/standardsprocess/">https://www.opengroup.org/standardsprocess/</a>
	</li>
</ul>

### The European Commission ISA<sup>2</sup> programme
ISA<sup>2</sup> the European Commission programme supporting the development of Interoperability Solutions. To coordinate interoperability activity at the EU level, it makes freely available a number of resources. Though one of the objectives of the programme is to create cross-border interoperability solutions, which is not of direct relevance to the work within UEC and CTP, the resources it produces are of value and applicable for reference:
<ul>
	<li>
		The European Interoperability Framework (EIF)<br>
		Provides specific guidance on how to set up interoperable digital public services, including recommendations on improving governance of interoperability services, establish cross-organisational relationships, and streamline processes supporting end-to-end digital services.<br>
		<a href="https://ec.europa.eu/isa2/eif_en">https://ec.europa.eu/isa2/eif_en</a>
		<br><a href="https://ec.europa.eu/isa2/sites/isa/files/eif_brochure_final.pdf">https://ec.europa.eu/isa2/sites/isa/files/eif_brochure_final.pdf</a>
	</li>

<li>
	The European Interoperability Reference Architecture (EIRA)<br>
	A tool for classifying and organising building blocks relevant to interoperability, which are used in the delivery of digital public services. The goal is to facilitate interoperability and reuse when developing public services. The latest version of EIRA was released in July 2017.<br>
	<a href="https://ec.europa.eu/isa2/solutions/eira_en">https://ec.europa.eu/isa2/solutions/eira_en</a>
</li>
</ul>

## Appendix C.	General Process
The following process steps cover the generic solution approach, which is followed for each workstream, in each tranche.  The rest of the document covers the detailed activities in each step for CTP tranche 1.  The process is illustrated in Figure 8:

<p style="text-align:center;"><a href="images/ctp_tranche_1_solution_approach_tranche_1_solution_approach_process.png"><img src="images/ctp_tranche_1_solution_approach_tranche_1_solution_approach_process.png" alt="Figure 8: Solution Approach Process" title="Figure 8: Solution Approach Process" style="width:75%"></a>
<br>Figure 8: Solution Approach Process
</p>


### Define Scope
The CTP programme will define the scope of the tranche of delivery.  This will be done using the industry standard approach aligned to The Open Group Architecture Framework (TOGAF).  In general terms, the scope will be defined based on a logical progression towards the final state of the solution, with a feasible delivery approach, meeting appropriate requirements to deliver benefits.

Given the scope of the delivery tranche, the programme will also define which platform components and workstreams are in scope.  A platform component is typically a single system or application, but may sometimes be just part of a system if the system is very large.

### Create Specifications
For each platform component in scope, the CTP programme will develop a set of specifications which can be used by system suppliers to develop the components needed by the platform.  The process of developing specifications may vary depending on the component in scope.  There will typically be multiple groups involved in the development of specifications, including the CTP programme, system suppliers, service providers and standards groups such as InterOPEN and PRSB.

The specifications will be published to the market following the normal process – typically this will be on the developer.nhs.uk website.

### Develop Platform components
Following the publication of the specifications, suppliers will develop platform components based on the specifications.  Suppliers will also develop to other requirements, as defined in their own market engagement processes.

The CTP programme will be available to support suppliers in their development to the new specifications.

In some cases (Pathways, Repeat Caller Service) the supplier may be NHS Digital.  Although many of the specifications are designed for components where there will be multiple suppliers (e.g. CDSS, EMS), there may be some where only a single component is required for the platform (e.g. Repeat Caller Service).

### Validation
Following development and release of a supplier platform component, there will be a process of validation.  The validation may differ by tranche and component, but will typically include a level of technical assurance that the component conforms to the specification, as well as wider processes that apply across the NHS, such as clinical safety assurance, and information governance (IG) assurance.

### Deploy
Finally, the components will be deployed into production.  This will normally be through a process of service providers purchasing validated system components directly from suppliers.  In some cases, the deployment may be of a single instance which is licensed centrally.

### Constraining Principles
The approach is defined and will be adapted to each tranche based on the following principles:

<table style="width:90%">
	<thead>
		<tr>
			<th>
				Transparency
			</th>
		</tr>
	</thead>
	<tr>
		<td>
			Statement
				<ul>
					<li>
						Fair and transparent approaches must be used when selecting open standards or agreeing exemptions from Open Standards Principles
					</li>
				</ul>

			Rational
			<ul>
				<li>
					Maintain accountability
				</li>
			</ul>

			Implications
			<ul>
				<li>
					All parties helping to specify or implement an open standard or API must maintain fair and transparent processes
				</li>
			</ul>
			Source
			<ul>
				<li>
					<a href="https://www.gov.uk/government/publications/open-standards-principles/open-standards-principles">https://www.gov.uk/government/publications/open-standards-principles/open-standards-principles</a>
				</li>
			</ul>
		</td>
	</tr>
</table>
<br>


<table style="width:90%">
	<thead>
		<tr>
			<th>
				Consensus
			</th>
		</tr>
	</thead>
	<tr>
		<td>
			Statement
			<ul>

			<li>
				Standards and APIs are based on the consensus of the parties involved
			</li>
		</ul>

			Rational
			<ul>

			<li>Industry consensus is critical to the adoption of standards</li>
			<li>The objective is to reach stable decisions</li>
		</ul>

			Implications
			<ul>

			<li>Standards are supported by consensus rather than unanimity</li>
			<li>Significant objections are taken into account and responded to</li>
			<li>Decisions do not remain strongly opposed by a sufficient subset of members</li>
		</ul>

			Source
			<ul>

			<li><a href="http://www.opengroup.org/standardsprocess/main.html">http://www.opengroup.org/standardsprocess/main.html</a></li>
		</ul>
		</td>
	</tr>
</table>
<br>


<table style="width:90%">
	<thead>
		<tr>
			<th>
				Confidentiality
			</th>
		</tr>
	</thead>
	<tr>
		<td>
			Statement
			<ul>

			<li>Material is kept confidential whilst in progress, until published by consensus</li>
		</ul>

			Rational
			<ul>

			<li>To protect submissions from parties</li>
			<li>To promote open discussions</li>
		</ul>

			Implications
			<ul>

			<li>Participants must be under obligations of confidentiality</li>
			<li>Obligations apply to all individuals of member companies</li>
			<li>All documents in progress should be clearly marked</li>
		</ul>

			Source
			<ul>

			<li><a href="http://www.opengroup.org/standardsprocess/main.html">http://www.opengroup.org/standardsprocess/main.html</a></li>
		</ul>
		</td>
	</tr>
</table>
<br>

<table style="width:90%">
	<thead>
		<tr>
			<th>
				Reusability
			</th>
		</tr>
	</thead>
	<tr>
		<td>
			Statement
			<ul>

			<li>Existing resources are reused and shared across programmes, tranches and workstreams</li>
		</ul>

			Rational
			<ul>

			<li>Improves quality by operational use of solutions with proven value</li>
			<li>Saves money and time</li>
		</ul>

			Implications
			<ul>

			<li>Parties should be open to sharing solutions, concepts, frameworks, specifications, tools and components with others</li>
		</ul>

			Source
			<ul>

			<li><a href="https://ec.europa.eu/isa2/sites/isa/files/eif_brochure_final.pdf">https://ec.europa.eu/isa2/sites/isa/files/eif_brochure_final.pdf</a></li>
		</ul>
		</td>
	</tr>
</table>
<br>


<table style="width:90%">
	<thead>
		<tr>
			<th>
				Timely and deterministic
			</th>
		</tr>
	</thead>
	<tr>
		<td>
			Statement
			<ul>

			<li>Standards are developed using a deterministic process that delivers standards in a predictable and timely manner</li>
		</ul>

			Rational
			<ul>

			<li>Consensus standards cannot be produced as rapidly as those of a single vendor, they do have to be produced at an acceptable pace</li>
		</ul>

			Implications
			<ul>

			<li>Prepare for an activity to be stopped or re-constituted if it does not reach consensus in a timely manner</li>
		</ul>

			Source
			<ul>

			<li><a href="http://www.opengroup.org/standardsprocess/main.html">http://www.opengroup.org/standardsprocess/main.html</a></li>
		</ul>
		</td>
	</tr>
</table>



## Appendix D.	Glossary

<table>
  <thead>
  <tr>
    <th>Abbreviation</th>
    <th>Definition</th>
  </tr>
  </thead>
  <tr>
    <td>A2R</td>
    <td>Access to Records</td>
  </tr>
  <tr>
    <td>A2SI</td>
    <td>Access to Service Information</td>
  </tr>
  <tr>
    <td>A&amp;E</td>
    <td>Accident &amp; Emergency</td>
  </tr>
  <tr>
    <td>API</td>
    <td>Application Programming Interface</td>
  </tr>
  <tr>
    <td>CAS</td>
    <td>Clinical Assessment Service</td>
  </tr>
  <tr>
    <td>CDSS</td>
    <td>Clinical Decision Support System</td>
  </tr>
  <tr>
    <td>CCG</td>
    <td>Clinical Commissioning Group</td>
  </tr>
  <tr>
    <td>CP-IS</td>
    <td>Child Protection Information System</td>
  </tr>
  <tr>
    <td>CSU</td>
    <td>Commissioning Support Unit</td>
  </tr>
  <tr>
    <td>CTI</td>
    <td>Computer Telephony Integration</td>
  </tr>
  <tr>
    <td>CTP</td>
    <td>Clinical Triage Platform</td>
  </tr>
  <tr>
    <td>DH</td>
    <td>Department of Health</td>
  </tr>
  <tr>
    <td>DoS</td>
    <td>Directory of Services</td>
  </tr>
  <tr>
    <td>DUEC</td>
    <td>Digital Urgent &amp; Emergency Care</td>
  </tr>
  <tr>
    <td>EAB</td>
    <td>Enterprise Architecture Board</td>
  </tr>
  <tr>
    <td>ED</td>
    <td>Emergency Department</td>
  </tr>
  <tr>
    <td>EMS</td>
    <td>Encounter Management System</td>
  </tr>
  <tr>
    <td>FHIR</td>
    <td>Fast Healthcare Interoperability Resources</td>
  </tr>
  <tr>
    <td>GDPR</td>
    <td>General Data Protection Regulations</td>
  </tr>
  <tr>
    <td>GP</td>
    <td>General Practice</td>
  </tr>
  <tr>
    <td>HES</td>
    <td>Hospital Episode Statistics</td>
  </tr>
  <tr>
    <td>HL7</td>
    <td>Health Layer Seven</td>
  </tr>
  <tr>
    <td>IDT</td>
    <td>Intelligent Data Toolkit</td>
  </tr>
  <tr>
    <td>IG</td>
    <td>Information Governance</td>
  </tr>
  <tr>
    <td>IT</td>
    <td>Information Technology</td>
  </tr>
  <tr>
    <td>IUC</td>
    <td>Integrated Urgent Care</td>
  </tr>
  <tr>
    <td>MH</td>
    <td>Mental Health</td>
  </tr>
  <tr>
    <td>MHRA</td>
    <td>Medicines and Healthcare products Regulatory Agency</td>
  </tr>
  <tr>
    <td>MIG</td>
    <td>Medical Interoperability Gateway</td>
  </tr>
  <tr>
    <td>MIU</td>
    <td>Minor Injury Unit</td>
  </tr>
  <tr>
    <td>NHS</td>
    <td>National Health Service</td>
  </tr>
  <tr>
    <td>NHSD</td>
    <td>NHS Digital</td>
  </tr>
  <tr>
    <td>NHSE</td>
    <td>NHS England</td>
  </tr>
  <tr>
    <td>NIB</td>
    <td>National Informatics Board</td>
  </tr>
  <tr>
    <td>NLP</td>
    <td>Natural Language Processing</td>
  </tr>
  <tr>
    <td>OoH</td>
    <td>Out of Hours</td>
  </tr>
  <tr>
    <td>PDS</td>
    <td>Personal Demographics Service</td>
  </tr>
  <tr>
    <td>PEM</td>
    <td>Post-Event Message</td>
  </tr>
  <tr>
    <td>PoC</td>
    <td>Proof of Concept</td>
  </tr>
  <tr>
    <td>PMPR</td>
    <td>Personalised Modelling of Patient Risk</td>
  </tr>
  <tr>
    <td>PRSB</td>
    <td>Professional Record Standards Body</td>
  </tr>
  <tr>
    <td>RCS</td>
    <td>Repeat Caller Service</td>
  </tr>
  <tr>
    <td>RFI</td>
    <td>Request For Information</td>
  </tr>
  <tr>
    <td>SaaS</td>
    <td>Software as a Service</td>
  </tr>
  <tr>
    <td>SCCI</td>
    <td>Standardisation Committee for Care Information</td>
  </tr>
  <tr>
    <td>SCR</td>
    <td>Summary Care Record</td>
  </tr>
  <tr>
    <td>TOGAF</td>
    <td>The Open Group Architecture Framework</td>
  </tr>
  <tr>
    <td>UEC</td>
    <td>Urgent &amp; Emergency Care</td>
  </tr>
  <tr>
    <td>UTC</td>
    <td>Urgent Treatment Centre</td>
  </tr>
</table>
Table 2: Glossary of Terms
