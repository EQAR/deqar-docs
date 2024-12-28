# Quick Start Guide

The purpose of DEQAR is to give wide public access to the reports and decisions on higher education institutions/programmes externally reviewed by EQAR-registered agencies.  We accomplish this through:

- an easily searchable database of institutions where users can find up-to-date QA reports for download;
- the provision of a basic set of standardised data on a range of agency activities;
- linked contextual data on national QA requirements and QA agencies, allowing users to understand the status and nature of QA reports.

[Download Quick Start Guide](files/DEQARStartUpPackage_v2.pdf)

## Getting Started

To get started with DEQAR, it is a good idea to first take measure of your agency’s needs to determine:

### What to Upload?

> **Take stock of the activities you undertake and the past and current reports which are eligible for DEQAR.**
>
> - Only upload those **reports on activities that were confirmed to be within the scope of the ESG** when the reports were created.
>
>     _Note: the list of eligible activities can be found on the register record for the agency ([https://www.eqar.eu/register/agencies/](https://www.eqar.eu/register/agencies/)) and also in the DEQAR administrative interface  accessible after the agency activates its account (see below: [Activate your Account](quick_start_guide.md#activate_your_account))._
>
>     _If a new activity is introduced, then a [formal change report](https://www.eqar.eu/register/guide-for-agencies/reporting-and-renewal/) should be submitted to the EQAR secretariat before the activity is deemed eligible in DEQAR. For other changes to activities, please contact the EQAR secretariat: [info@eqar.eu](mailto:info@eqar.eu)_
>
> - Only upload **reports created since the date of the agency’s registration** on EQAR (i.e. the date of the first external review of your agency against the ESG).
>
>     - Upload **legacy data**, i.e. the backlog of reports published since registration with EQAR.
>
>         _Note: if your agency is newly registered, then you should have little if any legacy data._
>
>     - Upload **current data**, i.e. reports you have recently completed (or will complete in the future).
>
> - It is necessary to meet certain **data requirements** in order for reports to be ingested into the system. Data requirements for reports vary depending on the type of activity described.  Ensure that you have this data available or can generate it as needed.
>
>     _Note: there are a few “soft requirements” for DEQAR which are not necessary for ingestion but which do trigger a red or yellow alert flag in the system._
>
> For details, please see:<br />
> [Report Data Elements](report_data.md)<br />
> [Data Pipeline](data_submission.md#data-pipeline)

### How to Upload?

> **Take stock of the size of your organisation, available staff and technical expertise as well as the volume of activities you undertake.**
>
> Each agency can choose one (or more) methods for submitting data. The DEQAR team has provided three submission methods tailored to different agencies’ needs:
>
> - a manual upload for individual reports;
> - CSV file upload for larger batches of reports; and
> - an API which automatically uploads reports from your local database as they are created, individually or in batches.
>
> _Note: these three methods are interoperable and can be used in different situations by the same agency. You should determine which option or options best suits your agency._
>
> For details, please see:<br />
> [Choosing a Submission Method](data_submission.md#choosing-a-submission-method)<br />

## Finding your Legs in DEQAR

Once you have figured out what you will submit and how, then it is time to enter the system.

### Activate your Account

> **Access the DEQAR account for your agency and confirm existing information.**
>
> - To activate your agency’s account, contact the EQAR secretariat at: [deqar@eqar.eu](mailto:deqar@eqar.eu)
>
>     _Note: unless you wish otherwise, the account information (contact name and email) will be based on the information on the agency already in our system._
>
> - Enter DEQAR’s Administrative User Interface using the following link: [{{ deqar.admin }}]({{ deqar.admin }})
>
> - Visit your agency’s Profile under My Data:
>
>     - to freely update the DEQAR contact information and password as suits your needs.
>
>         _Note: if you change your email address, you will need to use the new address to reset your password in the future._
>
>     - to update publicly available contact data on your agency, such as agency website, contact person, phone number, address and email.
>
>     - to assign local IDs to agency activities.
>
>     _Note: if you would like to change the general “Information on the agency’s work”, listed agency activities or the list of countries where the agency’s activities are officially recognised, you should contact the EQAR secretariat: [info@eqar.eu](mailto:info@eqar.eu)_
>
> - You should also analyse DEQAR’s institutional list to ensure that institutions evaluated/accredited by your agency are already present in the system.  The institution list can be found on the EQAR Admin Interface at: [{{ deqar.admin }}/institutions]({{ deqar.admin }}/institutions)
>
>     _Note: the base institution list is synchronised daily with the [Register of Public Sector Organisations (OrgReg)](https://www.risis2.eu/registers-orgreg/) and the [European Tertiary Education Register (ETER)](https://eter-project.com/), which cover a large number of European countries._
>
>     _If institutions are missing from the list, please contact the EQAR secretariat: [deqar@eqar.eu](mailto:deqar@eqar.eu) to arrange for the data to be imported. For details, see [Institution Data](institution_data.md)._

### Get to Know the System

> **Familiarise yourself with the administrative interface and the Sandbox.**
>
> - Once in the system, you should become familiar with the different modules available to you through the administrative interface:
>
>     - **My Data:** including records on your uploaded reports as well as your agency's profile (see above); information on alerts and flags.
>
>     - **Submit Reports:** giving access to the manual and CSV submission methods (see below for API).
>
>     - **Reference Data:** including records on all agencies, countries, higher education institutions and reports currently in DEQAR.
>
> - If you are planning to use the submission API, you can use API token found in your agency Profile and the following link: [{{ deqar.root }}/submissionapi/v2/submit/report]({{ deqar.root }}/submissionapi/v2/submit/report)
>
> - The Sandbox is reached through a separate link. The DEQAR Sandbox, like any sandbox, is intended for you to “play”, enabling you to trial particular submission methods, data structures, formats and syntax. More specifically, it is a space where we encourage (even urge) you to test your submissions before putting them into the live system:
>
>     - To test the manual and CSV submission, go to the Sandbox Administrative Interface at: [{{ deqar.sandbox.admin }}/]({{ deqar.sandbox.admin }}/)
>
>     - To test API submission, go to the Sandbox Submission API at: [{{ deqar.sandbox.backend }}/submissionapi/v2/submit/report]({{ deqar.sandbox.backend }}/submissionapi/v2/submit/report)
>
>     - To see what your records will eventually look like on the public site, go to the Sandbox Public Interface at: [{{ deqar.sandbox.frontend }}/]({{ deqar.sandbox.frontend }}/)
>
>     _Note: the entire data of the live site is copied over to the Sandbox every night. Thus, your login and password are the same as in your DEQAR account—unless you have made changes within the last 24 hours. You can also reset or change your password in the Sandbox, but it will be overwritten by the next day._

### Perform your First Submission

> - To perform your first submission &ndash; whether through the manual upload, CSV or API &ndash; we strongly encourage every agency to use the test environment, i.e. the [Sandbox]({{ deqar.sandbox.admin }}/).
>
> - Once you do the first test upload through the Sandbox, please check whether the test reports are red flagged by using the filter “Flags” in the section “Reports”. Should that be the case, at the bottom of the page, press “Show info” and read the note on the reasons. Please correct your data if applicable (e.g. the status of the report is marked as "part of the obligatory EQA system" for a higher education institution with a legal seat outside EHEA, in which case it must be "voluntary") or contact the EQAR Secretariat.
>
> - If the system ingests your files and there are no red flagged reports, please proceed with uploading your reports through the real live environment.
>
> - In case of doubt, please contact the EQAR secretariat at: [deqar@eqar.eu](mailto:deqar@eqar.eu). This will allow us to check your proposed data (particularly if submitted as a CSV), walk you through the submission process one last time and double check your results.

## DEQAR in the Longer Term

### Make a Road Map

> **Determine internal priorities and work methods.**
>
> - **Legacy data:** if applicable, determine a timeframe and method for uploading legacy reports, i.e. reports created since registration with EQAR. As a rule, it is a good idea to use a batch upload method (CSV or API) for legacy data.
>
> - **Current data:** set a continuous workflow to ensure that DEQAR is kept up to date with current activities. Determine:
>
>     - at what point in the work process will the reports be uploaded to DEQAR?
>     - will the reports be uploaded one-by-one upon completion or in batches, e.g. every month or every quarter?
>
>   _Note: methods for submitting legacy data — which is generally done in a few large batches — may be quite distinct from methods for continuous submission._

### Stay Connected

> **Stick with your road map and adapt your methods as needed.**
>
> _Remember: **“With great power comes great responsibility.”**_
>
> Once you commit to using DEQAR, it is important that you stay active so that your agency’s presence in the system is as continuous and coherent as possible.  Be sure to load new reports soon after they are ready for publication; otherwise you risk confusing the public, institutions or other agencies. You are encouraged to adapt the method and timing of submissions to best fit your internal work processes.
>
> On our side, we have tried to design DEQAR to be as effortless as possible. We hope that the system will prove a boost rather than a burden to your QA work.
>
> _Note: the DEQAR front end user interface is built using an API. This means that any agency may embed a version of DEQAR (included full search functionality) in its own website to alleviate some of the burden on the local IT team._

[Download Quick Start Guide](files/DEQARStartUpPackage_v2.pdf)
