---
title: Clinical Decision Support API Patient Journey
sidebar: overview_sidebar
permalink: cds-api-patient-journey.html
toc: true
summary: This page is intended for UEC supplier product specialists to understand the business context when adopting the CDS API standard, through an attempt to describe how CDS API FHIR resources and interactions could be used to support a simple patient journey.
folder: business_capabilities
---

## Clinical Scenario
This scenario describes the triage journey of a patient, who contacts NHS 111 after injuring her leg.

**Patient Persona** 

Karen is in her mid-thirties and works part time at the local post office.

**Staff Persona**

Claire is a Health Advisor for an NHS 111 Service Provider and has worked there for almost a year. She finds the job interesting and whilst it is challenging at times, she likes having the ability to help people in need and has a high level of job satisfaction.

## Simple patient journey using the CDS API

<table>
    <colgroup>
        <col width="40%" />
        <col width="60%" />
    </colgroup>
    <thead>
      <tr>
        <th>Business view</th>
        <th>System view</th>
    </tr>
</thead>
<tr>
  <td>
    <p>Whilst rushing to work, Karen tripped and injured her leg, which is still painful despite taking over the counter painkillers. She is not sure if it is bad enough to go to the Emergency Department, so she calls 111.</p>

    <p>Health Advisor, Claire, answers the call. She establishes Karen's identity and records that a leg injury is the reason for the contact. She enters this information into her organisation's Encounter Management System (EMS) whilst speaking to the patient.</p>
  </td>
    <td><p>The EMS creates the encounter and captures the patient's details including demographic information and the presenting complaint.</p></td>
</tr>
</table>

<div class="alert alert-info" role="alert">
    <i class="fa fa-info-circle"></i> 
    <b>Info:</b> Capturing the presenting complaint is managed by the EMS and does not form part of the CDS API interaction. However, a presenting complaint in a coded format, conformant with CDS API data requirements, may be required by the CDSS to drive triage initiation.
</div>


### 1. Find appropriate Clinical Decision Support to enable triage of the presenting complaint

<table class="table">
    <colgroup>
        <col width="40%" />
        <col width="60%" />
    </colgroup>
    <thead>
        <tr>
            <th>Business view</th>
            <th>System view</th>
        </tr>
    </thead>
    <tr>
        <td>
          <p>Claire requests clinical decision support to assist her in the triage of Karen's leg injury</p>
      </td>
      <td>        
          <p>The EMS must first select an appropriate <code>ServiceDefinition</code> from a Clinical Decision Support System (CDSS).</p> 
          
          <p>The EMS searches for a <code>ServiceDefinition</code> using a $search operation to search for a <code>ServiceDefinition</code> which corresponds to selected search criteria known to the EMS (e.g. patient gender, patient age group, user role). The EMS selects the appropriate <code>ServiceDefinition</code> and invokes the CDSS <code>ServiceDefinition</code>.</p>

          <p>The key interactions for the CDS API are represented in diagram format on the <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/solution_interactions.html">Solution Interactions section of the CDS API implementation guide</a>. </p>
      </td>
  </tr>
</table>

### 2. Initiate and run triage questionnaire with selected ServiceDefinition

<table class="table">
    <colgroup>
        <col width="40%" />
        <col width="60%" />
    </colgroup>
    <thead>
        <tr>
            <th>Business view</th>
            <th>System view</th>
        </tr>
    </thead>
    <tr>
        <td>
          <p>Claire is presented with clinical decision support to assist her with the triage of Karen's leg injury.</p>
      </td>
      <td>
        <p>The EMS has patient age and gender details that partially meet the <code>ServiceDefinition.DataRequirements</code> and posts these to the CDSS in the <code>ServiceDefinition.$evaluate.inputData</code> element.</p>

        <p>This information is 'inspected' by the CDSS and is insufficient to render a result as the CDSS needs more information about the nature of Karen's injury. The CDSS identifies an appropriate <code>Questionnaire</code> resource to elicit more information about the patient's injury. The reference to the <code>Questionnaire</code> resource is returned to the EMS as part of the <code>GuidanceResponse</code>.</p>
    </td>
  </tr>

    <tr>
        <td>
            <p>Claire asks Karen the questions displayed by the EMS and records her responses.</p>
        </td>
        <td>
          <p>The EMS displays the question(s) from the CDSS <code>Questionnaire</code> resource and captures the answers from the user.  The EMS creates a <code>QuestionnaireResponse</code> resource and populates this with the answers.</p>

          <p>The EMS posts the captured responses to the CDSS by invoking the same <code>ServiceDefinition.$evaluate</code> operation as in the step above, but now with a reference to the newly created <code>QuestionnaireResponse</code> in the $evaluate.inputData element.</p> 
          <p>The CDSS, in turn, reads the response and creates a clinical assertion as an <code>Observation</code> resource.</p> 
          <p>In line with RESTful behaviour (where each request from client to server must contain all the information necessary to understand the request and cannot take advantage of any stored context on the server) the assertions are referenced in the <code>GuidanceResponse.outputParameters</code>.</p> 
          <p>The <code>GuidanceResponse.status</code> is set to 'data-required' and the reference to the next <code>Questionnaire</code> resource is populated in the <code>GuidanceResponse.dataRequirement</code> element.</p>  
          <p>The next <code>Questionnaire</code> is sent as a request for more information from the EMS. The EMS collects answers from the user and invokes $evaluate again, populating input data with the <code>QuestionnaireResponse</code> and all assertions received in the <code>GuidanceResponse.outputParameters</code>, as per the Restful behaviour described above.</p>
          <p>This loop is repeated until there is enough information for the CDSS to populate the result.</p> 
        </td>
    </tr>
</table>

### 3. The CDSS provides a Result against a chief concern, post assessment

<table class="table">
    <colgroup>
        <col width="40%" />
        <col width="60%" />
    </colgroup>
    <thead>
        <tr>
            <th>Business view</th>
            <th>System view</th>
        </tr>
    </thead>
    <tr>
        <td>
          <p>Claire reaches the end of the questions and a triage outcome, which in this case is to have her leg examined by her GP within 24 hours, is displayed on screen.</p>
      </td>
      <td>

        <p>The CDSS has enough information to arrive at a triage outcome which determined that the patient required a primary care assessment within 24 hours.
        </p> 
        <p>The <code>GuidanceResponse.status</code> is set to 'success'.</p>
        <p>The result element in <code>GuidanceResponse</code> is populated with a <code>RequestGroup</code> resource which references a <code>ReferralRequest</code>.</p>
        <p>The details of the referral carried in the <code>ReferralRequest</code> include:
         <ul>
           <li>reasonReference of 'Injury of Lower Leg'</li>
           <li><code>ProcedureRequest</code> of 'Physical examination of limb by primary care clinician'</li>
           <li>Occurrence of 'within 24 hours'</li>
         </ul>
       </p>
    </td> 
</tr>
<tr>
    <td>
        <p>As it is within Primary Care opening hours, Claire advises Karen to make an appointment with her GP within 24 hours, using the information displayed on the EMS.</p>
    </td>
    <td>
    </td>
</tr>
</table>


### 4. End of CDS API interactions

<p>Because the <code>GuidanceResponse.status</code> has been set as 'success', the EMS knows that the recommended result can be acted on, and that no additional information is needed which would improve the recommendation.</p>

<p>The EMS displays the recommendation to Claire, who has no reason in her judgement to override the recommendation.  As the call happens during GP opening hours, Claire advises Karen to make an appointment with her GP.  Since the EMS is connected to the Personal Demographics Service (PDS), and Karen has been identified in the EMS, Claire can see Karen's registered GP.</p>

<p>The EMS to CDSS interactions are concluded.</p>
