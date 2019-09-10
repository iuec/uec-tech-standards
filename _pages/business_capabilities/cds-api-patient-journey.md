---
title: Clinical Decision Support API Patient Journey
sidebar: overview_sidebar
permalink: cds-api-patient-journey.html
toc: true
summary: This page is intended for UEC supplier product specialists to understand the business context when adopting the CDS API standard, through an attempt to describe how CDS API FHIR resources and interactions could be used to support a simple patient journey.
folder: business_capabilities
---

## Clinical Scenario
This scenario covers a patient, who contacts NHS 111 after having fallen and hurt their right knee.

**Patient Persona** 

Karen Bloggs is in her mid-thirties, has an 18 year old son living at home and works part time at the local post office.

**Staff Persona**

Claire is a call handler at 111 and has worked there for almost a year now. Claire finds the job interesting but also challenging at times. However, she likes having the ability to help people in need and says she has good job satisfaction.

## Simple patient journey using the CDS API

<table>
    <colgroup>
        <col width="60%" />
        <col width="40%" />
    </colgroup>
    <thead>
      <tr>
        <th>Business view</th>
        <th>System view</th>
    </tr>
</thead>
<tr>
    <td>
        <p>Rushing to the shops this morning Karen tripped and injured her left knee. The fall occurred 30 minutes ago. There is no further bleeding, but Karen's knee is sore, Karen calls 111.</p>

        <p>Claire, the Call Handler, answers the call. Claire establishes Karen's demographic information and records that Karen has a leg injury resulting from blunt trauma.</p>

        <p>The information is entered into the EMS by the system user while talking to the patient.</p>
</td>
    <td><p>The EMS records the demographic information and the presenting complaint.</p></td>
</tr>
</table>

<div class="alert alert-info" role="alert">
    <i class="fa fa-info-circle"></i> 
    <b>Info:</b> Capturing the presenting complaint should be managed within the EMS and does not form part of the CDS API interaction. However, the presenting complaint in a coded format drives and informs the triage process initiation. 
</div>



### 1. Find appropriate Clinical Decision Support to enable triage of the presenting complaint

<table class="table">
    <colgroup>
        <col width="50%" />
        <col width="50%" />
    </colgroup>
    <thead>
        <tr>
            <th>Business view</th>
            <th>System view</th>
        </tr>
    </thead>
    <tr>
        <td>
          <p>
          Claire enters the presenting complaint obtained in the patient encounter on the EMS, which in turn invokes the clinical decision support. </p>
      </td>
      <td>        
          <p>The EMS invokes clinical decision support through the <code>ServiceDefinition.$evaluate</code> operation, requesting a <code>GuidanceResponse</code> resource from the CDSS.</p>
          <p>The EMS selects from the available CDSS service definitions, which most closely match the current known state of the patient using the <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/api_get_service_definition.html">select ServiceDefinition interaction</a>.</p>
          <p>
              The CDS API facilitates the selection of a service definition by search and filtering based on query and <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/api_post_service_definition.html">Trigger for Evaluate ServiceDefinition Interaction</a>.
          </p>
          <p>The key interactions for the CDS API are represented in diagram format on the <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/solution_interactions.html">Solution Interactions section of the CDS API implementation guide</a>. </p>
      </td>
  </tr>
</table>

### 2. Initiate and run triage questionnaire with most appropriate ServiceDefinition available

<table class="table">
    <colgroup>
        <col width="50%" />
        <col width="50%" />
    </colgroup>
    <thead>
        <tr>
            <th>Business view</th>
            <th>System view</th>
        </tr>
    </thead>
    <tr>
        <td>
          <p>Illness and injury clinical decision support gets invoked and the invocation includes known information about the journey.</p>
      </td>
      <td>
        <p>This known information, stored in <code>ServiceDefinition.$evaluate.inputData</code> is 'inspected' by the CDSS and is insufficient to render a result. The CDSS creates a <code>Questionnaire</code> resource to elicit more information about the journey.</p> 

        <p>The CDSS references this <code>Questionnaire</code> in a <code>GuidanceResponse</code> resource returned to the EMS, and thus establishes a <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/api_get_questionnaire.html">Questionnaire and Response interaction</a> sequence.</p>
    </td>
  </tr>

    <tr>
        <td>
            <p>Claire asks for confirmation that Karen is able to walk through some questions, which she is.</p>
            
            <p>Questions from the CDSS are presented on the EMS screen for Claire to read to Karen and record her responses.</p>
            
        </td>
        <td>
            <p>The responses to the CDSS questions from Karen are then communicated back by the EMS using the <code>QuestionnaireResponse</code>.</p> 

            <p>The CDSS, in turn, reads the response and creates a clinical assertion as an <code>Observation</code> resource, and tags these to the next set of questions until there is enough information for it to conclude an outcome. </p>
        </td>
    </tr>
    <tr>
        <td>
            <p>Using the questions available from the CDSS presented on her screen, Claire continues talking to Karen ruling out any blood loss, swelling of limbs, joint pains and deformity as directed by the CDSS question path.</p>
            <p> She captures Karen's answers in the EMS, including any additional information as necessary, which are conveyed back to the CDSS. </p>
        </td>
        <td>
            <p>The EMS continues invoking the <code>ServiceDefinition.$evaluate</code> operation referencing <code>QuestionnaireResponses</code> and any previous assertions (<code>Observation</code> resources) for the CDSS to evaluate.</p>
            <p> The CDSS creates further assertions from the <code>QuestionnaireResponse</code> and determines whether a result can be provided.</p>
        </td>
    </tr>
</table>

### 3. CDSS provides a Result against a chief concern, post assessment

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
          <p>Claire reaches the end of the blunt trauma question pathway and a triage outcome is displayed on screen.</p>
      </td>
      <td>
          <p>
          The CDSS reaches the stage where enough information is available to arrive at a triage outcome. The CDSS conveys this through the Result element within the <code>GuidanceResponse</code> resource. Since Karen's injury is only superficial, the CDSS is able to confirm the triage outcome or result of a Care advice of type "Self Care". 
      </p>
          <p>
            The result element in <code>GuidanceResponse</code> is populated with a <code>RequestGroup</code> resource which will reference a <code>CarePlan</code> as the outcome of the triage journey. The <code>CarePlan</code> is of type "Self Care" Advice, and is indicated by the CareTeam.particpant element of the resource is referenced with only one instance of participant and the participant.role set to "Patient".
        </p>
    </td> 
</tr>
<tr>
    <td>
        Claire provides self-care advice to Karen, using the information provided by the CDSS. 
    </td>
    <td>
    </td>
</tr>
</table>


### 4. End of CDS API interactions
The EMS to CDSS interactions are concluded.
