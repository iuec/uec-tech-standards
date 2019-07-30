---
title: Clinical Decision Support API developer guidelines
sidebar: overview_sidebar
permalink: cds-api-developer-guidelines.html
folder: business_capabilities
---

<style type="text/css">
  pre.highlight{
    max-height: 500px;
    overflow: scroll;
  }
</style>

<!-- Restrict table of contents to H2 elements -->

<script>
$( document ).ready(function() {
  // Handler for .ready() called.

$('#toc').toc({ minimumHeaders: 0, listType: 'ul', showSpeed: 0, headers: 'h2' });

/* this offset helps account for the space taken up by the floating toolbar. */
$('#toc').on('click', 'a', function() {
  var target = $(this.getAttribute('href'))
    , scroll_target = target.offset().top

  $(window).scrollTop(scroll_target - 10);
  return false
})

});
</script>

<div id="toc"></div>




## General
### Should I send interim (draft) results?
There can be value in the CDSS providing an early view of the decision, even when more information would help to refine the decision.  This can be done by populating the result element of the `GuidanceResponse`, but marking the status as ‘draft’.  This enables the EMS to advise the system user, who can then act appropriately, according to local process.

### What happens if a patient has multiple presenting conditions?
If a patient has multiple presenting conditions, each of which is managed by a separate `ServiceDefinition`, then the EMS can invoke more than one `ServiceDefinition` evaluation and these can be processed in parallel.  From the CDSS perspective, each is a separate journey, and it is up to the EMS to manage the presentation of information to the user.

### Can I make a referral request while continuing the triage?  For example, dispatching an ambulance?
Yes, this can be done by populating the result, and setting the status of the result to final, while setting the status of the `GuidanceResponse` to dataRequested or dataRequired.  If the referral request is also the end of the triage, then the `GuidanceResponse.status` will be final.

### As the CDSS, can I move the user to a different journey?
Yes.  The CDSS may have constructed internal logic such that a certain set of answers in a journey mean that the current `ServiceDefinition` is no longer appropriate, and that a different `ServiceDefinition` should be used.  For example, a patient may have started on a `ServiceDefinition` based on a presenting complaint of joint pain, but the patient’s answers indicate that the problem is more serious, and that a  `ServiceDefinition` designed for broken bones is more appropriate.  When this happens, the CDSS can direct the EMS to a new `ServiceDefinition` by sending back an `ActivityDefinition` in the `GuidanceResponse`, where the `ActivityDefinition` has the trigger of the new `ServiceDefinition` (which can then be found by the EMS).

## Evaluation

### How do I start the decision support process?
Asking a Clinical Decision Support System (CDSS) for a decision is done by invoking the `$evaluate` operation on a `ServiceDefinition`.  A CDSS will publish at least one `ServiceDefinition`, and can publish many different `ServiceDefinitions` – each of which is appropriate for a different clinical decision.  The CDSS will send back a `GuidanceResponse` as the reply to an `$evaluate` operation.

### How do I know which ServiceDefinition to choose?
When the CDSS publishes a `ServiceDefinition`, the `ServiceDefinition` will have elements which describe how the `ServiceDefinition` can be used.  The description of where in the clinical process a `ServiceDefinition` sits is described in the `ServiceDefinition.trigger`.  This element will hold all the data conditions which need to be satisfied for the `ServiceDefinition` to be chosen.

<!-- ### What if there are multiple ServiceDefinitions that fit the data available?
During a given patient journey, there may be points where there is more than one `ServiceDefinition` available.  Any one CDSS should avoid this situation, but if a provider has more than one CDSS available, there may be situations where more than one CDSS can provide an appropriate `ServiceDefinition`.  In this case, it will be up to local providers on how to choose between the available `ServiceDefinitions`. -->

### What if the CDSS needs more information?
In a typical UEC triage journey, the CDSS will need to get information from the patient by asking questions.  This is provided by putting the next question to be asked in the `GuidanceResponse`, and the Encounter Management System (EMS) providing the patient’s answer in the next `$evaluate` operation.

<!-- 
EMS
How can I capture site safety information?
Flag (need to elaborate?) 
-->

## FHIR Primer
### What are resources?
Fast Healthcare Interoperability Resources (FHIR) is an international standard based around defining Resources.  These are objects which represent things of value to a healthcare environment.  Examples are patient, encounter, medication or diagnosis.  Much of the information transferred during a triage journey is described using resources.

In a message, resources will often be referenced from other resources.  For example, a diagnosis resource will have a reference to the patient that the diagnosis applies to.  The patient will be described in a resource.

### What’s a contained resource?
Referenced resources can be a reference (by id), where if more information from the referenced resource is needed, that resource can be fetched directly (through a GET operation).  Alternatively, the referenced resource can be provided in full in the primary resource.  This is referred to in FHIR as a contained resource.

### Should I use contained resources?
There are advantages and disadvantages of embedding resources as contained resources.  It makes the message bigger and can mean that the same information is sent repeatedly, during the ‘conversation’ of a typical triage journey.  However, using contained resources reduces network traffic, and the overhead of connection and handshaking.

Each system should be able to work with contained and referenced resources, without prejudice.  The choice of whether to use references or contained resources will depend on many factors of the local implementation.



## Elements

### How is the presenting complaint identified?
The presenting complaint is a primary symptom that a patient states as the reason for seeking medical help. The presenting complaint is a subjective statement made by a patient describing the most significant or serious symptoms or signs of illness or dysfunction that caused him or her to seek health care.

The patients’ presenting complaint will be identified by asking the patient directly what the problem is they are calling about. 

The presenting complaint does not have a specific place within the CDS API. Therefore, a `ServiceDefinition` with a 'null trigger' would present a questionnaire to capture this information. This may be a multiple choice question, or as free text providing the system has the ability to parse, consume and act on this information.


### What is a chief concern? How is it identified?
The Chief Concern is the most dominant clinical finding/condition or diagnosis the clinician or CDS has concerns about.  

Typically, clinical decision support that is used for triage presents questions that start with the most urgent and life threatening symptoms, seeking to eliminate the most significant concerns and risks to the patient. These systems are typically non diagnostic and are used for remote triage/assessment over the telephone. These triage solutions often lead to a recommended level of care and are accompanied with a timeframe in which to seek that care.

Responses to the questions will drive the recommendations that are generated by the Clinical Decision Support System. The clinician using these recommendations, their own critical thinking skills, experience/knowledge, will formulate a clinical impression which they will endorse by use of the chief concern for onwards communication. 

When a CDSS recommends additional referral/consultation, the clinician receiving the referral will often be helped by seeing the chief concern which has driven the recommendation.
The chief concern is carried in the reasonReference element in the `Referralrequest` resource. The CDSS can also provide other concerns which have not been eliminated, but which are less significant than the chief concern. These secondary concerns are carried in the supportingInfo element in the `Referralrequest` resource.


### What is the diagnostic discriminator? How is it identified?
When the CDSS recommends the patient is referred for further consultation, there may be a specific activity which needs to be performed at the next consultation, so that the chief concern can be ruled in or out. For example, if the chief concern of the CDSS is a fracture, the activity needed is an x-ray. This activity is the diagnostic discriminator.

The diagnostic discriminator can be used when searching for the best service to perform the consultation, where the service must be able to carry out the activity in the diagnostic discriminator. For example, where the diagnostic discriminator is an x-ray of the suspected fracture, the filter for the service can look for services which have x-ray facilities.

The diagnostic discriminator is carried in the ProcedureRequest element in the `ReferralRequest` resource.


## Questionnaire resource
### How do I represent a choice question?
Many of the questions presented during a triage process are ‘closed’ questions, where the patient is asked to choose one of a set of limited options.  There are two ways of representing this in the `Questionnaire` resource.  The first way is to create an item for the question, and then have items for each of the possible choices, associated to the question item.  Since this is quite cumbersome, there is a shortcut, where the question item is marked as a ‘choice’ type item, and the possible options are then listed in the item.option element.

### How do I represent a multiple choice question?
Where the patient can select more than one choice (for example, a question like “Are you taking any of the following medications?”), the options must be listed out as separate items where the item.repeats property of the question is set to true.

### How do I represent a ‘none of the above’ question?
There may be questions where there are multiple options, or the user can choose ‘None of the above’, which can’t be selected if any other options are chosen, and should stop any other options being chosen at the same time.

This can be represented through the Questionnaire extension option-exclusive [https://www.hl7.org/fhir/stu3/extension-questionnaire-optionexclusive.html](https://www.hl7.org/fhir/stu3/extension-questionnaire-optionexclusive.html)

### Is there a value set for Yes|No|Don’t Know?
Yes, there is a standard set for this, which is commonly used in triage – see [https://www.hl7.org/fhir/stu3/questionnaire.html#2.38.5.7](https://www.hl7.org/fhir/stu3/questionnaire.html#2.38.5.7) for full details.

### How do I represent required versus optional?
If a question is optional, and doesn’t need a response, set the `item.required` as false.  If the question must be answered, set this as true.

### How do I represent that the user didn’t answer an optional question?
If the user doesn’t answer an optional question, this element is simply not populated in the `QuestionnaireResponse`.

<!-- ### Are there limits on lengths of question or answer options?
tbc -->

### What type of questions can I ask?
As well as choice type questions, the EMS must be able to support questions which can be answered by text, by numbers (whole or decimal), by date, by a blob (e.g. a picture supplied by the patient of the wound) or as a Boolean (true|false).

### Can I group questions together?
If a set of questions should be displayed together, this can be shown through creating a ‘header’ item, which has the .type of ‘group’

<!-- ### How do I ask a question where the user has to click on an image?

```javascript
    {
     "linkId": "41",
     "text": "Which colour do you prefer: red, blue, green or yellow?",
     "type": "string",
     "required": true,
     "initialAttachment": {
     "url": "data:image/png;base64,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"
      }
    }
```


### Is this the pattern for "image" type questions?
Yes - the image is the attachment, and the EMS sends back the co-ordinate click point as a string (hence the string type) which the CDSS can then 'map' to the image to ascertain the actual 'answer'/selection
 -->
### How do I give contextual information for the question?
Contextual information can be carried as linked extensions, coded as type ‘context’

<script src="https://gist.github.com/IOPS-DEV/45a290a8ac920d031c6465230b834542.js"></script> 


### How do I specify DataRequirements

An example of DataRequirements is given below with notes:

- There is no profile in the first DataRequirement (the QuestionnaireResponse) as we are (currently) using the STU3 profile for QuestionnaireResponse
- The FHIR profiles for the CDS API are to be available in future iterations 
- There is no requirement for the Questionnaire - the CDS doesn't need this, it just needs the QuestionnaireResponse, and we can identify the type of QuestionnaireResponse by saying that it has to be a response to the Questionnaire called "#PRE_STD_AD_DISCLAIMERS"
- The second DataRequirement (for the practice) shows that this must be an Organization, further specified as a CareConnect Organization, where the Organization.identifier must be part of the ValueSet of odsOrganisationCode - that is, that it must be an ODS organisation
- The patient, their age, and their gender are all specified independently
- The valueCode for the gender is the Gender finding - could also be the UK reference set for Gender - 991391000000109

<script src="https://gist.github.com/IOPS-DEV/9870eab47c7d9243a377144df806f61e.js"></script> 

