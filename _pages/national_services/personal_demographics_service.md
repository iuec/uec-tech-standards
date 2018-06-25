---
title: Personal Identification
sidebar: overview_sidebar
keywords: ITK
permalink: personal_demographics_service.html
toc: true
folder: national_services
---

## Using the Personal Demographics Service (PDS)
PDS is the national electronic database of NHS patient details such as name, address, date of birth and NHS Number (known as demographic information)<sup>1</sup>. The PDS should be used to identify patients when they present to urgent care services.

In a UEC context, PDS allows the provider to confirm a patient’s demographics including their name, date of birth, sex, the GP surgery at which they are currently registered, and their current home address. This is an essential enabler for interoperability between services and enables providers to send Post Event Messages (PEMs) to the patient’s registered GP surgery<sup>2</sup>.

The NHS England Integrated Urgent Care Service (IUC) Specification<sup>2</sup> sets out how existing and new NHS 111 and Out Of Hours (OOH) service elements should be commissioned, provided and measured which includes expectations around access to and use of PDS.  The NHS England specification<sup>2</sup> details what service providers need to have in place regarding PDS, summarised below:

+ The patient’s NHS number shall be verified using PDS
+ The chosen clinical workflow system has technical integration with PDS and supports the use of Advanced PDS Tracing
+ An Advanced PDS trace shall be performed for all patients during their encounter with IUC and shall be an integrated part of the workflow within the clinical workflow system and available to all users, subject to appropriate access controls. It is not permissible for traces to be performed manually by use of a separate system.
+ For patient referrals/transfers from another service (including online), if it is established that a PDS trace has not been performed by the sending service, the receiving service must perform a PDS trace for that patient at the point of referral.
+ Where a PDS lookup has been performed online, the information must be captured by the provider’s workflow system as part of the referral.
+ For Clinical Assessment Services (CASs), on receipt of patients streamed to a CAS through a NHS 111 telephony or online channel, the CAS must validate the demographics and if necessary run a PDS match before placing the call in the appropriate clinical queue for assessment.


## Developing against PDS
A formal specification of the HL7v3 messaging to Spine required for accessing PDS is available on TRUD as part of the NHS Message Implementation Manual (MiM):

[https://isd.digital.nhs.uk/trud3/user/authenticated/group/0/pack/34/subpack/28/releases](https://isd.digital.nhs.uk/trud3/user/authenticated/group/0/pack/34/subpack/28/releases)

Registration is required for access.

A copy of the MiM specifications is also available here:

[https://data.developer.nhs.uk/dms/mim/4.2.00/Index.htm](https://data.developer.nhs.uk/dms/mim/4.2.00/Index.htm)

## Spine Mini Services (SMS)
Advanced PDS tracing is identified as a requirement in the NHS England Integrated Urgent Care Service (IUC) Specification, however a more restricted form of PDS searching through SMS is available which may be sufficient in simpler use cases.

The SMS PDS offers a read-only interface to PDS, which only returns a single result or nothing at all – sufficient input search criteria must be supplied to differentiate multiple matches and target a single individual.

Information regarding the process for Suppliers and End User organisations who wish to gain access to the PDS via the NHS Digital Spine Mini Service Provider (SMSP) is available at:

[https://developer.nhs.uk/library/systems/nhs-digital-smsp-pds/](https://developer.nhs.uk/library/systems/nhs-digital-smsp-pds/)

 The SMSP allows systems to integrate with Spine more easily. SMSP is a free web service interface, fully supported by NHS Digital as part of the Spine platform allowing health and care organisations to fulfil their duties under the NHS Standards contracts to use the NHS number as a ‘consistent identifier’<sup>4</sup> .  The NHS Digital SMSP application is currently available for PDS data only and enables service providers to connect to the NHS PDS for read only access.

## References
1. [https://digital.nhs.uk/services/demographics](https://digital.nhs.uk/services/demographics)
2. [https://www.england.nhs.uk/wp-content/uploads/2014/06/Integrated-Urgent-Care-Service-Specification.pdf](https://www.england.nhs.uk/wp-content/uploads/2014/06/Integrated-Urgent-Care-Service-Specification.pdf)
3. [https://developer.nhs.uk/library/systems/nhs-digital-smsp-pds/](https://developer.nhs.uk/library/systems/nhs-digital-smsp-pds/)
4. [https://digital.nhs.uk/services/spine/spine-mini-service-simplified-ways-to-connect-to-spine#the-nhs-digital-spine-mini-service-provider-smsp-](https://digital.nhs.uk/services/spine/spine-mini-service-simplified-ways-to-connect-to-spine#the-nhs-digital-spine-mini-service-provider-smsp-)
