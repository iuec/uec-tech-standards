---
title: Clinical Decision Support API Patient Journey
sidebar: overview_sidebar
permalink: cds-api-patient-journey.html
toc: true
summary: This page is intended for the UEC supplier product specialists to understand the business context when adopting the CDS API standard.
folder: business_capabilities
---

<style>
    code{
        background-color: #f9f2f4;
        border-radius: 4px;
        color: #c7254e;
        white-space: normal;
    }
</style>


## Clinical Scenario
This scenario covers a patient, who contacts NHS 111 after having fallen and hurt their right knee.

**Patient Persona** 

Karen Bloggs is in her mid-thirties, has an 18 year old son living at home and works part time at the local post office.

**Staff Persona**

Claire is a call handler at 111 and has worked there for almost a year now. Claire finds the job interesting but also challenging at times. However, she likes having the ability to help people in need and says she has good job satisfaction.

## Patient journey using the Clinical Decision Support API

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

        <p>Claire, the Call Handler, answers the call. Claire establishes Karen's demographic information and records that Karen has a Leg Injury resulting from Blunt Trauma.</p>

        <p>The information is entered into the EMS by the system user while talking to the patient.</p>
</td>
    <td><p>The EMS records the demographic information and the presenting complaint.</p></td>
</tr>
</table>

<div class="alert alert-warning" role="alert">
    <!-- <i class="fa fa-warning"></i>  -->
    <b>Info:</b> Capturing the presenting complaint should be managed within the EMS and does not form part of the CDS API interaction. However, the presenting complaint in a coded format drives and informs the triage process initiation. 
</div>







### Step 1: Find appropriate Clinical Decision Support to enable Triage of the presenting complaint

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
          Claire enters the presenting complaint obtained in the patient encounter on the EMS, which in turn invokes the Clinical Decision Support and selects an appropriate Service Definition. </p>
      </td>
      <td>        
          <p>The EMS invokes the clinical decision support system through EMS using the <code>$evaluate</code> operation, requesting guidance from the <code>ServiceDefinition</code>.</p>
          <p>The EMS selects from the available CDSS service definitions, which most closely match the current known state of the patient using the <code>select ServiceDefinition</code> interaction.</p>
          <p>
              The CDS API facilitates the selection of a service definition by search and filtering based on query and <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/api_post_service_definition.html#trigger-for-evaluate-servicedefinition-interaction">Trigger for Evaluate ServiceDefinition Interaction</a>
          </p>
      </td>
  </tr>
</table>

### Step 2: Initiate and run triage questionnaire with most appropriate Service Definition available

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
          <p>Illness and injury Clinical decision support gets invoked and the invocation includes known information about the journey.</p>
      </td>
      <td>
        <p>This known information, stored in <code>ServiceDefinition.$evaluate.inputData</code> is 'inspected' by the CDS and is insufficient to render a result. The CDSS creates a <code>Questionnaire</code> resource to elicit more information about the journey.</p> 

        <p>The CDSS references this <code>Questionnaire</code> in a <code>GuidanceResponse</code> resource and returns to the EMS, and thus establishes a question and response interaction sequence.</p>
    </td>
  </tr>

    <tr>
        <td>
            <p>Claire asks for confirmation that Karen is able to walk through question and answers, which she is.</p>
            
            <p>Questions from the CDSS are presented on the EMS screen for Claire to read to Karen and record her responses.</p>
            
        </td>
        <td>
            <p>The responses to the CDSS questions from Karen are then communicated back by the EMS using the <a href="http://hl7.org/fhir/stu3/questionnaireresponse.html"><code>QuestionnaireResponse</code></a>.</p> 

            <p>More information on the EMS-CDSS questionnaire response interaction is available <a href="https://developer.nhs.uk/apis/cds-api-1-0-0/solution_interactions.html#questionnaire--questionnaireresponse-interaction">here</a>.</p>


            <p>The CDSS, in turn, reads the response and creates clinical assertion/s as <a href="http://hl7.org/fhir/stu3/observation.html"><code>Observation</code></a> resource and tags  these to the next set of questions, until there is enough information for it to conclude an outcome. </p>

        </td>
    </tr>
    <tr>
        <td>
            <p>Using the questions available from the CDSS presented on her screen, Claire continues talking to Karen ruling out any blood loss, swelling of limbs, joint pains and deformity as directed by the CDSS question path. She captures Karen's answers in the EMS, including any additional information as necessary, which are conveyed back to the CDSS. </p>
            
        </td>
        <td>
            <p>The EMS requests the CDSS to continue to evaluate while it references the latest <code>QuestionnaireResponse</code> and any previous assertions (Observation resources) for the CDSS.</p>
            <p> The CDSS creates further assertions from the <code>QuestionnaireResponse</code> and determines whether a result can be provided.</p>
        </td>
    </tr>
</table>

### Step 3: CDSS provides a Result against a chief concern, post assessment

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
          The CDSS reaches the stage where enough information is available for the CDSS to arrive at result or a triage outcome, the CDSS conveys this through the Result element within the <code>GuidanceResponse</code> resource. Since Karen's injury is only superficial, the CDSS is able to confirm the triage outcome or result of a Care advise of type "Self Care". 
      </p>
          <p>
            The result element in <code>GuidanceResponse</code> is populated with a <code>RequestGroup</code> resource which will reference a <code>CarePlan</code> as the outcome of the triage journey. The CarePlan is of type "Self Care" Advice, is indicated by the  CareTeam.particpant element of the resource is referenced with only one instance of participant and the participant.role set to "Patient".
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


### Step 4: End of CDS API interactions
The EMS to CDSS interactions are concluded.
