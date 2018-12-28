---
title: Current ITK messaging within Urgent and Emergency Care
sidebar: overview_sidebar
keywords: ITK, transfer_of_care, referrals
permalink: itk_messaging_within_uec.html
toc: true
folder: messaging
---

Messaging across the 111 Domain is defined within the context of ITK2.2.  The following diagram shows in green the interactions that are within the NHS 111 Domain Message Specification:

<!--- check wording of above sentence -->
<!--- Image green highlight not visible -->

<p style="text-align:center;"><img src="images/itk_messaging_within_uec.png" alt="Interactions within the NHS 111 Domain Message Specification.png" style="width:75%"></p>

The message structures are defined on TRUD [https://isd.digital.nhs.uk](https://isd.digital.nhs.uk) (search for 111).

The current version of the structures in use is 2.0.

The message structures are based on HL7 standards, (HL7v3 and CDA).  A set of development requirements for using ITK 2.2 to send and receive CDA documents can be found at:

[https://developer.nhs.uk/wp-content/uploads/2017/10/ITK-CDA-Sender-and-Receiver-Requirements.pdf](https://developer.nhs.uk/wp-content/uploads/2017/10/ITK-CDA-Sender-and-Receiver-Requirements.pdf)

## Conformance levels and compatibility maturity

Integration between different organisations requires common consent around the structures that are used to share information between them. Reaching agreement on how data will be transferred provides a level of technical interoperability between them.

Clinical interoperability is achieved when, in additional to technical interoperability, a common understanding of the content of the messages is agreed. This implies the exchanged information contains some structured content (machine readable) and that a common terminology is used.

The resource above provides a high-level introduction to ITK and also describes the concept of ITK CDA conformance levels and an associated concept of compatibility maturity.

<table>
  <tr>
    <th>Conformance level<br></th>
    <th>Description<br></th>
  </tr>
  <tr>
    <td>Level 1</td>
    <td>CDA header and CDA bodies can be rendered, but are not structured</td>
  </tr>
  <tr>
    <td>Level 2a</td>
    <td>CDA header, structured XML CDA body and simple non-coded text</td>
  </tr>
  <tr>
    <td>Level 2b </td>
    <td>CDA header, structured XML CDA body and advanced coded text sections</td>
  </tr>
  <tr>
    <td>Level 3</td>
    <td>CDA header, structured XML CDA body and simple non-coded text or advanced coded text sections, and SNOMED coded entries </td>
  </tr>
</table>

### Compatibility maturity
Interoperability between systems is impacted by having differing levels of maturity at the ITK CDA Sender and Receiving applications.

<style media="screen">
  .darkgrey{background-color:#777!important;color: white;}
  .lightcyan{background-color:#daeef3;}
  .lightsteelblue{background-color:#b8cce4;}
  .lightskyblue{background-color:#8db3e2;}
  .thistle{background-color:#b2a1c7;}
  .cellwidth100 td{
    width:100px;
  }
  .text-center td{
    text-align:center;
  }
</style>

<table>
<thead>
  <tr>
    <th>Key</th>
    <th>Description</th>
  </tr>
  </thead>
  <tr>
    <!-- <td style="background-color:#daeef3;">VB</td> -->
    <td style="background-color:lightcyan">VB</td>
    <td>View Body – e.g. viewing an embedded PDF</td>
  </tr>
  <tr>
    <!-- <td style="background-color:#b8cce4;">VT</td> -->
    <td style="background-color:lightsteelblue;">VT</td>
    <td>View text</td>
  </tr>
  <tr>
    <td style="background-color:lightskyblue;">PT</td>
    <td>Process text</td>
  </tr>
  <tr>
    <td style="background-color:thistle">VB, PT, PC</td>
    <td>View body, processes coded text sections and process coded entries</td>
  </tr>
</table>




<table class="cellwidth100 text-center" style="">
  <tr class="darkgrey">
    <td></td>
    <td colspan="4">Sender</td>
  </tr>
  <tr class="darkgrey">
    <td>Receiver</td>
    <td>1</td>
    <td>2a</td>
    <td>2b</td>
    <td>3</td>
  </tr>
  <tr>
    <td class="darkgrey">1</td>
    <td class="lightcyan">VB</td>
    <td class="lightcyan">VB</td>
    <td class="lightcyan">VB</td>
    <td class="lightcyan">VB</td>
  </tr>
  <tr>
    <td class="darkgrey">2a</td>
    <td class="lightcyan">VB</td>
    <td class="lightsteelblue">VB, VT</td>
    <td class="lightsteelblue">VB, VT</td>
    <td class="lightsteelblue">VB, VT</td>
  </tr>
  <tr>
    <td class="darkgrey">2b</td>
    <td class="lightcyan">VB</td>
    <td class="lightsteelblue">VB, VT</td>
    <td class="lightskyblue">VB, PT</td>
    <td class="lightskyblue">VB, PT</td>
  </tr>
  <tr>
    <td class="darkgrey">3</td>
    <td class="lightcyan">VB</td>
    <td class="lightsteelblue">VB, VT</td>
    <td class="lightskyblue">VB, PT</td>
    <td class="thistle">VB, PT, PC</td>
  </tr>
</table>

It should be noted that the CDA Levels of either party impact the interoperability of the system has a whole.
