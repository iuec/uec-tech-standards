---
title: PEM Suppression
sidebar: overview_sidebar
keywords: ITK, pem, discharge
permalink: pem_suppression.html
toc: true
folder: messaging
---
At the end of an patient journey within Integrated Urgent Care (IUC), a patient's GP practice should be notified, messages should only be sent when an encounter with the IUC service has concluded and no call backs or further care is going to be provided by the service.

This is to ensure the volume of messages a GP receives is kept to a minimum and the GP isn't receiving duplicate information.


## Never Send List

For the purposes of Post Event Messaging (PEM) to a GP the following dispositions are categorized as “Never Send”.

This means that upon completion of a NHS Pathways assessment, reaching any of these disposition messages do not need to be transferred to inform the patients GP.

| Dx Code | Description                              |
| ------- | ---------------------------------------- |
| DX 28   | Contact Pharmacist                       |
| DX 52   | Refer to Police                          |
| DX 60   | Contact Optician next routine appointment within 72 hours |
| DX 22   | To be seen by Dental Practice within 3 working days |
| DX 23   | Contact Orthodontist next working day    |
| DX 45   | Provide Service Location Information     |
| DX 46   | Refer to Health Information              |
| DX 63   | Refer to Fluline                         |
