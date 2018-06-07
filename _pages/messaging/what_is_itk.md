---
title: What is ITK?
sidebar: overview_sidebar
keywords: ITK, faq
permalink: what_is_itk.html
toc: false
folder: messaging
---

The acronym 'ITK' gets used a lot within the healthcare technology world.

It stands for **Interoperability Toolkit**, and the official NHS Digital page about ITK can be found at (https://digital.nhs.uk/interoperability-toolkit)

## What is ITK?

> The Interoperability Toolkit (ITK) is a set of common specifications, frameworks and implementation guides that support interoperability.

It is essentially an umbrella term / brand name.

## What isn't ITK?

**ITK is not a specific specification or standard. It is not a 'badge' that is issued to system suppliers.**

A system with 'ITK interfaces' or 'ITK support' does not necessarily have the ability to talk to other systems with 'ITK interfaces' - it depends completely on which of the ITK specifications or standards the system provider has implemented.

When system providers have developed their product to support ITK specifications and standards, they can go through an accreditation process to have this formally tested and recognised by NHS Digital.

*If a system provider tells you that the system supports 'ITK' you should ask for precise detail on which elements of ITK they support.*

## What is ITK accreditation?

Also known as 'ITK conformance', a system provider being issued with ITK accreditation means that they have implemented against at least one of the specifications within the ITK collection.

An ITK Conformance certificate is issued to a system provider upon completion of the accreditation process - it means that NHS Digital are satisified that the system meets the requirements in the specification you have chosen to support.

**Note: You do not require ITK accreditation in order to start development - it is issued right at the end of the development process.**

NHS Digital maintains an [online catalogue of suppliers who have been formally accredited as 'ITK Conformant'](https://digital.nhs.uk/interoperability-toolkit/accreditation-catalogue) - if the supplier is not in this list, it means they have not been issued with an ITK accreditation by the NHS Digital ITK team.

You will notice that the catalogue specifically lists the *Catalogue category* and *System type* against which a system provider has been issued accreditation.

**As a purchaser / user of systems this is the most important part of the cataloge - it will tell you exactly which capability a system provider can support.**

For example, a supplier listed under the Catalogue category of "Hospital Admission, Discharge and Transfers" can't necessarily communicate with a system under the category of "NHS 111".

The cataloge also lists the System Version ID against which an accreditation has been issued. This means that in order for you to make use of the ITK functionality, your system will need to be on that minimum version; it is often the case that all versions after the one listed will continue to support the functionality but you should always ask your the system provider about this.

## What is the process for ITK accreditation / conformance?

The ITK team at NHS Digital will guide you through the process, and so you should enage with that team as early in the process as possible. You need to know which of the ITK specifications you would like to develop against, as the requirements can vary significantly, and the exact process may involve different teams and additional business requirements.

You can find more details about initiating contact with the ITK team here: (https://developer.nhs.uk/testcentre/itk-accreditation/)

A a system provider, an overview of the process is:

1. You identify the ITK specifications against which they would like to develop your software.

2. You make contact with ITK Accreditation team at NHS Digital to initiate the process.

3. You download the relevant technical specifications to support the specific technical capability you are building against.

   Most specifications can be found on the TRUD [(Terminology and Reference data Update Distribution)](https://isd.digital.nhs.uk/trud3/user/guest/group/0/home) portal - you will have to sign up for an account, but this is free.

   You will also need to download the development support tools that are provided to help you with the process.

   You should ask the ITK team for guidance on which specifications and tools you need to use if in doubt.

4. Once accepted into the process, the ITK team will issue you with a tailored "requirements catalogue" - it will list all of the documented functional and non-functional requirements you need to meet. It will also detail any tests you need to complete as part of the process.

5. As you develop your product, you should complete the requirements catalogue and try and use the specified tests as a guide for your development. Many leave the compliance parts to the end, and this is guarranteed to be more painful for you!

6. Once all development is complete, you submit your completed requirements cataloge along with all necessary test evidence that is required.

7. When the ITK team are satisfed with your submission, they will confirm conformance and issue you with a certificate. This is the point at which you will be added to the online ITK Accreditiation Catalogue.
