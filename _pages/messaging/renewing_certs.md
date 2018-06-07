---
title: Renewing TLS MA Certificates for ITK Messaging
sidebar: overview_sidebar
keywords: ITK, certificates, security
permalink: renewing_certs.html
toc: false
folder: messaging
---
ITK certificates provide the security and identification element of existing Integrated Urgent Care interoperability. They are used to provide Mutual Authentication between two communicating parties. Live services operate using spine certificates issued to endpoints on the oneoneone.nhs.uk NHS sub-domain.

These certificates are issued centrally by NHS Digital. New certificates can be obtained by contacting the Deployment Issue Resolution team on <mailto:dir@hscic.gov.uk>

### Expiry of certificates
When you are issued with ITK certificates, they are automatically issued with an expiry date. This expiry date is the last point in time at which that certificate will be valid.

Once a certificate expires it can no longer be used to make a secure connection - this would result in interoperability failing.

In order to ensure that your service is not interrupted by an expiring certificate, you must make sure you **renew your certificate** before the expiry date.


### Renewing certificates
Certificates can be renewed at any point - you do not have to wait until the the expiry date is close or passed.

If a certificate is issued with an expiry date that is 2 years away, it is advisable that you aim to renew that certificate 6 months before it expires. This gives you plenty of time to go through the renewal process and deal with any issues that may arise.


### Monitoring certificates
Monitoring certificates is the responsibility of the organisation to which the certificate has been issued - certificate expiries are not monitored centrally and so you will not receive an alert when your certificate is about to expire.

Many system vendors will have their own processes in place for monitoring certificates and will be able to cover this as part of their service provision.
