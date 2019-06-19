---
title: Clinical Decision Support API Demo Implementation
sidebar: overview_sidebar
permalink: cds-api-demo-implementation.html
toc: true
folder: emerging
---

For suppliers interested in understanding more about the CDS-API, working demos of an Encounter Management System (EMS) and a Clinical Decision Support System (CDSS) compliant to the [CDS-API specification](https://developer.nhs.uk/apis/cds-api/) are available as Git repositories for running in a self hosted environment.

## Encounter Management System Test Harness

The EMS is responsible for invoking the decision support process on the CDSS. The EMS will typically also manage elements like user authentication, workflow and user interactions.

The EMS Test Harness application aims to provide the minimum functionality required be compliant to the CDS API specification. The EMS MUST be able to:

* Initiate the selection of a `ServiceDefinition`
* Initiate the evaluation of a `ServiceDefinition`
* Read appropriate resources from the CDSS (e.g. `Questionnaire`)
* Write appropriate resources (e.g. `QuestionnaireResponse`)
The Encounter Management System MAY:

* Write resources which are not core (e.g. `Condition`)

The EMS test harness repository is available at [https://gitlab.com/ems-test-harness/cdss-ems](https://gitlab.com/ems-test-harness/cdss-ems).

This repository is in active development. To access the version compliant to 1.0.0 of the CDS-API [please use the repository 1.0.0 tag](https://gitlab.com/ems-test-harness/cdss-ems/tree/1.0.0).

### EMS Test Harness - setup and build instructions

#### Pre-requsities

Install nodejs and npm if they are not already on your machine.

#### Frontend setup

Navigate to the EMS-UI folder `cd .\EMS-UI\`

Install angular CLI `npm install -g @angular/cli`

Install dependencies `npm install`

To run the application `ng serve --open`. This will open the app on port `4200`.

The applications configuration can be found in `EMS-UI/src/environments`

To generate a new component `ng generate component <component-name>`

#### Backend setup

Create a MySql database and run the sql scripts under `src/main/resources/sql`

Update the `src/main/resources/application.properties` file to point to the database.


#### Credentials to access the EMS solution

- Username: admin
- Password: password

Logging in as admin will provide access to an Admin menu with extra test harness configuration options such as user management, CDSS Supplier management, environment settings and audit logs.


### Using the EMS test harness application

Once logged in, the home page will be displayed

<p style="text-align:center;"><a href="images/ems-demo-homepage.png"><img src="images/ems-demo-homepage.png" alt="The EMS Test Harness home page" title="The EMS Test Harness home page" style="max-width:100%"></a></p>

This gives a selection of patients and CDSS suppliers. The list of suppliers can be changed by going to Admin > Manage CDSS Suppliers. New suppliers can be added, removed or altered (using the Edit button). New scenarios can be added when editing a supplier but please note that new scenarios will not work unless the scenario is also added into the supplier stub database.

To run through a scenario you must
- Begin on the Home page
- Select a patient by clicking on one of their names
- Select a test stub
- Once a stub is selected the user is given a list of service definitions
- Select the service definition you wish to run and click the Launch button.

When running through a scenario you will be presented with a series of questions. Answer the questions and click Continue until the scenario ends. Previous answers may be amended using the Back button. When the scenario ends the user is shown a suggested action or care plan. Start over by clicking on the Home link at the top of the page and selecting a new patient and supplier.


## CDSS (Clinical Decision Support System) Stub

The CDSS is responsible for making clinical decisions, and communicating these to the EMS.

Together the EMS and one or more CDSS's are responsible for providing clinical and non-clinical UEC personnel undertaking triage or consultation with clinical support.

The CDSS Stub application aims to provide the minimum functionality required to be compliant to the CDS API specification. The CDSS MUST be able to:

- Respond to filtered searches for `ServiceDefinition`
- Respond to evaluation of a `ServiceDefinition`
- Read appropriate resources from the EMS (e.g. `QuestionnaireResponse`)
- Write appropriate resources (e.g. `Questionnaire`, `Observation`)

The CDSS Stub repository is available at [https://gitlab.com/ems-test-harness/cdss-supplier-stub](https://gitlab.com/ems-test-harness/cdss-supplier-stub).

This repository is in active development. To access the version compliant to 1.0.0 of the CDS-API [please use the repository 1.0.0 tag](https://gitlab.com/ems-test-harness/cdss-supplier-stub/tree/1.0.0)


### CDSS Supplier Stub - setup and build instructions

#### Running with Docker

To run this locally just run:
`$ docker-compose up`

This will obtain the mySQL image, initialize the `cdss-supplier` database and run the `populate_data.sql` script which creates the tables and populates with the mock data.

It will also download and run the cdss-supplier-stub image from the docker registry in gitlab.com.

Within the `docker-compose.yml` file. The mySQL host can be changed from `cdss-mysql` to `localhost` if the mysql server is being hosted on the local machine instead of the docker container.

Have a look at [Docker documentation](https://docs.docker.com/) for more information.

#### Running without Docker

Create a MySql database and run the sql scripts under `src/main/resources/sql`

Update the `src/main/resources/application.properties` file within the EMS Test Harness to point to the database.

