# Report Data Elements

Different [submission methods](data_submission.md) can be used to create or [update](data_submission.md#updating-reports) quality assurance report records in DEQAR. Deletion of existing records can be requested through the API or manually through the admin interface, but final deletion can only be performed by the EQAR Secretariat.

Below we provide a full list of the data elements that can make up a report record. It is important to note that the below list is exhaustive, including all possible elements. Required data elements are listed in **bold** with a \* , conditionally required data elements in **bold** with a (\*).

There are several possible one-to-many relations within a report record: e.g. one report might cover several providers (e.g. in case of a joint programme), or several programmes of one institution, or can have several associated files, etc.. In JSON for API submission, these cases can be naturally represented as arrays of objects; in a CSV file, these relations are difficult to represent due to the flat/one-dimensional structure.

In the CSV template, such columns or groups of columns can thus be duplicated and indexed with an integer in square brackets, e.g. `institution[1].deqar_id`, `institution[2].deqar_id`, … The structure and field names of the elements below directly reflect the CSV template, with repeatable columns indicated by `[n]` part of the column name.

To see how these elements are arrayed in JSON for API submission, see our JSON definition at:

<https://backend.deqar.eu/submissionapi/v2/swagger/>

Please note that new records for providers not currently represented in DEQAR should be submitted separately beforehand. Please use the dedicated [CSV templates described above](institution_data.md#how-to-provide-data).

|ELEMENT NAME |REQUIRED |ONE/MANY |EXAMPLE |
|:--------------------------------------------|:------------|:---------|:-----------------------|
|**Agency** |yes |one |*AAQ*<br>*33* |
|Contributing Agencies | no | many | *MusiQuE*<br>*34* |
|DEQAR Report ID |no |one |*786* |
|Local Report Identifier |no |one |*QAA1153-March15* |
|**Activity** |conditionally|one |*institutional audit*<br>*programme evaluation*<br>*2*<br>*8*|
|**Activity Local Identifier** |conditionally|one |*inst_aud* |
|**Status** |yes |one |*1 - part of obligatory EQA system*<br>*2 - voluntary*|
|**Decision** |yes |one |*1 - positive*<br>*2 - positive with conditions or restrictions*<br>*3 - negative*<br>*4 - not applicable*|
|Summary |no |one | |
|**Valid from** |yes |one |*2015-01-15* |
|Valid to |no |one |*2020-01-15* |
|**Date Format** |yes |one |*%Y-%m-%d* |
|Link |no |one |*http://srv.aneca.es/ListadoTitulos/node/1182321350*|
|Comment |no |one |*Evaluation undertaken with Musique.*<br>*Programme group reports are created for programmes with a similar profile across the entire sector on a 7-year rotating basis.*|

## Agency

A single creating agency must be clearly identified for each report. The creating agency is often, though not always, the same as the submitting agency (see [Agency Identifiers](architecture_data_model.md#agency-identifiers)).

> When a report is co-created by several EQAR-registered agencies, one of the agencies needs to take responsibility for uploading the report to DEQAR and keeping it up-to-date. This one should be specified as (main) Agency, the other ones as Contributing Agencies.

- **Agency\*** (<code>agency</code>; required; string)  
  The (main) agency which created the report must be provided for each report as an agency acronym or as a DEQAR agency ID. This allows the report to be linked to an existing agency record and makes it possible to validate and transform the submitted data in accordance with the agency's profile.

    *e.g. AAQ*  
    *e.g. 33*

- Contributing Agencies (<code>contributing_agencies[n]</code>; not required; string)  
  Additional EQAR-registered agencies that were involved in the external QA procedure and the production of the report. Contributing agencies can only be recorded if they were registered in EQAR at the time of issuing of the report (<code>valid_from</code> date). Otherwise, all validation and flagging rules follow the main agency. The report will also be shown under the contributing agencies’ profiles in DEQAR.

    *e.g. MusiQuE*  
    *e.g. 34*


## Report Identifier

Each uploaded report is assigned a unique DEQAR report ID. The identifiers of new reports uploaded are shown in the DEQAR admin interface. When using the Submission API, the identifiers are also included in the response object and automatically sent back to the agency via the email tied to the username.

Each report can be identified using an agency's local identifiers or through DEQAR report IDs. It is recommended that agencies submit a local report identifier for every report (see [Report Identifiers](architecture_data_model.md#report-identifiers)).

* DEQAR Report ID (<code>report_id</code>; not required; string)  
  A report identifier must be used when submitting updates to an existing report in CSV or JSON. This may be used to submit updates to existing reports or to promote synchronisation with an agency's local system.

    *e.g. 000786*

* Local Report Identifier (<code>local_identifier</code>; not required; string)  
  The report identifier used in the agency's local system should be provided for each report. This may be used to submit updates to existing reports or to promote synchronisation with the agency's local system; the local report identifier is particularly useful in the identification of invalid submission objects.

    The format and semantics of the local identifier are at the agency's discretion. Please note that local identifiers must be **stable** and **unique** (within your agency): if you submit a report with the same local identifier as an existing report of your agency, you will overwrite the existing record.

    Local identifiers are always linked to a specific agency. Hence, there is no need to include your agency acronym as part of your identifier.

    *e.g. QAA1153-March15*

## Activity

A single activity must be assigned to each report. Activities are selected from the agency's pre-defined list of activities and should be provided as a DEQAR value (as either a string value or a DEQAR activity ID).

> If you do not find the activity enlisted on DEQAR, please inform EQAR about the new activity through submitting a Substantive Change Report via [this form](https://www.eqar.eu/register/substantive-change-report/).

Optionally an agency may choose to provide local identifiers for its own activities; before these can be used for submission, these identifiers should be assigned through the agency record in the administrative interface (see [Role of Standards and Identifiers: Other Identifiers](architecture_data_model.md#other-identifiers). If both elements are submitted for a single report, then the DEQAR value will be used by the system.

* **Activity(\*)** (<code>activity</code>; conditionally required; string)  
A DEQAR activity value may be provided as an activity name or DEQAR activity ID for each report. The activity is used to validate the structure of submitted report data.

    *e.g. institutional audit*  
    *e.g. programme evaluation*  
    *e.g. 2*  
    *e.g. 8*  

* **Activity Local Identifier(\*)** (<code>activity_local_identifier</code>; conditionally required; string)  
  A local activity identifier may optionally be provided in place of a DEQAR activity value for each report. The local activity identifier may be used to validate the structure of submitted report data. (Note: local activity identifiers need to be assigned through the administrative interface before they can be used in submission.)

    *e.g. inst_aud*

Each activity is classified as one of four activity types (<code>activity_type</code>). These classifications determine the structure of the report record:

|Type                    |Provider(s)            |Programme(s)           |
|:-----------------------|:----------------------|:----------------------|
|institutional           |at least one provider  |no programme           |
|institutional/programme |only one provider      |at least one programme |
|programme               |only one provider      |at least one programme |
|joint programme         |at least two providers |at least one programme |

## Details

Each report must be assigned a single status and a single decision value. Together these elements signal the role, status and nature of the report. Status and decision values may be provided as either string values or DEQAR IDs.

* **Status\*** (<code>status</code>; required; string)  
  The status must be provided as either a DEQAR status name or a DEQAR status id for each report. The status specifies whether the report is part of the obligatory EQA system in the country of the institution or whether the institution has undertaken it voluntarily:

    |ID |name |description |
    |:--|:-----------------------------|:-----------|
    |1 |part of obligatory EQA system |A review is of obligatory nature if the QA process/the report/the decision has any kind of official status in the higher education system where the institution is based/established, e.g. further serves for accreditation or licencing of the higher education institution, fulfils a legal obligation to undergo a regular evaluation or audit, etc. |
    |2 |voluntary | Any other review is of a voluntary nature, e.g. if it is requested at the provider's own initiative and serves enhancement purposes only (i.e. does not lead to a nationally-recognised accreditation or certification of the provider). |

    > Where an institution can choose different types of external QA arrangements (e.g. applying for institutional is optional, but might replace all or some programme accreditation obligations), also the optional/voluntarily chosen external QA report should be classified as "part of obligatory EQA system" if it has a status within the higher education system's official QA framework.

    The status "part of obligatory EQA system" may only be used for reports that cover at least one higher education institution based in the EHEA. **For reports that cover only higher education institutions beyond the EHEA or only other providers, the status must always be "voluntary".**

    | Type of provider | Part of obligatory system | Voluntary |
    |:-----------------|:--------------------------|:----------|
    | Higher education institution in the EHEA | Yes | Yes     |
    | Higher education institution beyond the EHEA | Only if the report also covers at least one institution based in the EHEA | Yes |
    | Other provider   | Only if the report also covers at least one institution based in the EHEA | Yes |


    > The status determines whether a QA report is exported to the accreditation database for European Digital Credentials for Learning (EDC): only reports classified as "part of obligatory EQA system" are automatically exported and can be used as accreditations in EDC. See [Integrations: EDC](europass.md) for details.

* **Decision\*** (<code>decision</code>; required; string)  
  The decision must be provided as either a DEQAR decision name or a DEQAR decision id for each report. The decision records the final result of the QA procedure/report.

    The decision should be final. Only in cases when the decision is “positive with conditions”, the decision can be changed to “positive”. In such cases, a second report file that confirms the upgraded decision should be added to the record without deleting the initial report file.

    |ID |name |
    |:--|:---------------------------------------|
    |1 |positive |
    |2 |positive with conditions or restrictions|
    |3 |negative |
    |4 |not applicable |

* Summary (<code>summary</code>; not required; string)  
  A textual summary of the key findings of the report/decision that allows users to understand the outcomes without reading the full report. Strongly recommended, the summary should be in English.

* Comment (<code>other_comment</code>; not required; string)  
  The optional comment can contain important information on the report that cannot be represented in the structured data, e.g. involvement of other partner agencies or any specific notes about the QA procedure.

    *e.g. Evaluation undertaken in cooperation with MusiQuE.*  
    *e.g. Programme group reports are created for programmes with a similar profile across the entire sector on a 7-year rotating basis.*

## Validity

Each report must have a date defining the start of its validity. Agencies should also provide a date defining the end of the report's validity. In case the end date is left open, the report will be treated as valid for six years from the start of its validity. DEQAR uses a special notation to denote the date format. This allows each agency to signal the date format it uses; this must be provided for each report.

* **Valid from\*** (<code>valid_from</code>; required; date)  
  A valid from date marking the starting date of the report's validity must be provided for each report. This date is used to generate an archiving date when no valid to date is provided.

    *e.g. 2015-01-15*

* Valid to (<code>valid_to</code>; not required; date)  
  A valid to date marking the ending date of the report's validity should be provided for each report. This date determines when report data will be archived in DEQAR. If no valid to date is assigned, then the report will be treated as valid for six years after the valid from date.

    *e.g. 2020-01-15*

* **Date Format\*** (<code>date_format</code>; required; string)  
  A date format must be provided for each report. Dates may be submitted in any standard format; the format should be represented as a combination of the following characters:

    |symbol(s)| meaning |example |
    |:--------|:--------------------------------------|:----------------------------|
    |%d |day as expressed in two digits |02 |
    |%-d |day as expressed in one or two digits |2 |
    |%m |month as expressed in two digits |05 for May |
    |%-m |month as expressed in one or two digits|5 for May and 12 for December|
    |%Y |year as expressed in four digits |2014 |
    |%y |year as expressed in two digits |14 |
    |%d-%m-%Y | |04-01-2014 |
    |%d/%m/%y | |04/01/14 |
    |%Y-%m-%d | |2015-01-15 |

## Files

DEQAR requires PDF versions of quality assurance reports for every submission object. Agencies can choose either to make files available for harvest or to upload files. In order to make files available for harvest, agencies must provide the URL for files already available on a public server. Alternatively, files may be submitted using the API or uploaded through the administrative interface. All reports must be submitted with data on the language(s) used in the report. A file display name can be provided as well.

|ELEMENT NAME |REQUIRED |ONE/MANY |EXAMPLE |
|:--------------------------------------------|:------------|:---------|:-----------------------|
|**File Original Location** |conditionally|many |*http://estudis.aqu.cat/MAD2014_UPC_es.pdf*|
|File Display Name |no |one (per) |*Report*<br>*Evaluation*<br>*MAD2014_UPC_es.pdf*|
|**Report Language** |yes |many (per)|*es*<br>*spa* |

* **File Original Location(\*)** (<code>file[n].original_location</code>; conditionally required; string)  
  At least one PDF file should be provided with each submitted report in the form of a URL. Optionally, PDF files can be uploaded through the API or user interface.

    *e.g. http://estudis.aqu.cat/MAD2014_UPC_es.pdf*

    > The URL *should* return the [HTTP content-type header](https://developer.mozilla.org/de/docs/Web/HTTP/Headers/Content-Type) `application/pdf` upon a *HEAD* request. The URL *must* return `application/pdf` upon a *GET* request. If another content-type is reported, the file will not be downloaded and saved.
    >
    >  The maximum file size is 10MB.

* File Display Name (<code>file[n].display_name</code>; not required; string)  
  A single file display name may be provided for each PDF report file, used for the file link in DEQAR. If no display name is provided, then the file name will be used for display instead.

    *e.g. Report*  
    *e.g. Evaluation*

    > This should be a short and generic term (such as “Report and Decision”, “Evaluation Report”, “Accreditation Decision”, “Summary report”, ...). The display name should *not* repeat the name of the provider or programme addressed in the report.

* **Report Language\*** (<code>file[n].report_language[n]</code>; required; string)  
  One or more languages must be provided for each file in the form of an ISO 639 1 (two-digit) or ISO 639 2 (three digit) language code (see [ISO 639-1 or ISO 639-2/B format](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)).

    *e.g. es*  
    *e.g. spa*

## Link

One or more links may be provided to alternative views of the report data on the agency's own website or other webpage(s) in order to provide more context.

If one link is provided, it will be displayed with the text "View record on agency's website".

If several links are provided, display names must be provided for each link. These texts will be displayed on DEQAR in order to distinguish the different links.

* Link (<code>link[n]</code>, not required, string)  
  One or more URL links may be provided for each report to the same report presented on other sites in order to provide more context to the report.

    *e.g. http://srv.aneca.es/ListadoTitulos/node/1182321350*

* Link Display Name (<code>link_display_name[n]</code>, conditionally required, string)  
  A short text describing where the link points to; required and used only when several links are provided.

    *e.g. report in national qualifications database*  
    *e.g. decision on ministry's website*

## Provider(s)

Each report must be associated with at least one provider. The record(s) for the provider(s) need(s) to already exist in DEQAR, see [the previous section on adding missing providers to DEQAR](institution_data.md).

Preferably, the DEQARINST ID should be provided to identify the provider(s). In addition, the ETER ID can be used for higher education institutions listed in ETER/OrgReg.

Alternatively, an agency may choose to use local or other identifiers for the provider(s). Before these can be used for submission, the local identifiers should be provided in bulk to the EQAR secretariat.

Only one identifier should be submitted for each provider in the submission object (see [Provider Identifiers](architecture_data_model.md#provider-identifiers)). If more than one identifier is submitted, then the DEQARINST ID will be used to establish internal linkage, followed by the ETER ID (for higher education institutions), followed by the local or other identifier.

|ELEMENT NAME                 |REQUIRED FOR HEI |REQUIRED FOR AP |ONE/MANY  |EXAMPLE                          |
|:----------------------------|:----------------|:---------------|:---------|:--------------------------------|
|**DEQARINST ID**             |conditionally    |conditionally   |one (per) |*DEQARINST0034*                  |
|**ETER ID**                  |conditionally    |not applicable  |one (per) |*BG0001*                         |
|**Institutional Identifier** |conditionally    |conditionally   |one (per) |*HCERES21*<br>*AT0004*           |
|Identifier Resource          |conditionally    |conditionally   |one (per) |*SI-ETER.BAS.NATID*<br>*Erasmus* |

* **DEQARINST ID(\*)** (<code>institution[n].deqar_id</code>; conditionally required; string)  
  Each provider already described in DEQAR is assigned a DEQARINST ID. The DEQARINST ID may be used to establish a link between submitted report data and an existing provider record.

    *e.g. DEQARINST0034*

* **ETER ID(\*)** (<code>institution[n].eter_id</code>; conditionally required; string)  
  (*Only applicable to reports on higher education institutions*) Each institution described in OrgReg or ETER is assigned an ETER ID (see [Register of Public Sector Organisations - OrgReg](https://www.risis2.eu/registers-orgreg/) or [European Tertiary Education Register - ETER](https://www.eter-project.com/)). The ETER ID may be used to establish a link between submitted report data and an ETER record in DEQAR.

    *e.g. BG0001*

* **Provider Identifier(\*)** (<code>institution[n].identifier[1]</code>; conditionally required; string)  
  A local identifier is any identifier used by the Agency to identify a provider, while other identifiers can be recorded in DEQAR for use by all agencies. These may optionally be used in the place of a DEQARINST ID (or ETER ID for higher education institutions) to establish a link between submitted report data and an existing provider record.

    > Local identifiers need to be assigned in bulk through the EQAR secretariat before they can be used in submission; other identifiers can be consulted in the administrative interface and can be assigned in consultation with the EQAR secretariat; see [Provider Identifiers](architecture_data_model.md#provider-identifiers) for details.)

    *e.g. HCERES21*  
    *e.g. AT0004*

* Identifier Resource(\*) (<code>institution[n].resource[1]</code>; conditionally required; string)  
  If the identifier you use is not a local identifier of your agency, you need to provide its corresponding resource tag. The value for this field can be consulted through the administrative interface.

    *e.g. DE-HRK*  
    *e.g. SI-ETER.BAS.NATID*  
    *e.g. Erasmus*

## Programme Data

Information on one or more programmes is required for all reports with the assigned activity types: **institutional/programme**; **programme**; or **joint programme**. As a rule, programme information must be entered anew for each report, though DEQAR allows agencies to assign local programme identifiers in order to track reports on the same programme.

See the [definitions on programmes and higher education providers](index.md#definitions).

|ELEMENT NAME |REQUIRED FOR PROGRAMMES LEADING TO A FULL DEGREE |REQUIRED FOR PROGRAMMES THAT DO NOT LEAD TO A FULL DEGREE |ONE/MANY |EXAMPLE |
|:------------|:-----------------------------------|:-----------------------------------------------------------|:--------|:-------|
|Local Programme Identifier             |no      |no      |many (per) | *61*<br>*60800* |
|**Primary Programme Name**             |yes     |yes     |one (per)  | *Arts-specialist in opleiding*|
|Programme Qualification                |no      |no      |one (per)  | *Master in de specialistische geneeskunde*|
|Programme Name Alternative             |no      |no      |many (per) | *Medical Natural Sciences*|
|Programme Qualification Alternative    |no      |no      |many (per) | *Master of Medicine* |
|Programme Country                      |no      |no      |many (per) | *BE*<br>*BEL* |
|**Programme Degree Outcome**           |yes(\*) |yes(\*) |one (per)  | *yes*<br>*no* |
|**Programme Qualification Level**      |yes(\*) |yes     |one (per)  | *0 - short cycle*<br>*1 - first cycle*<br>*2 - second cycle*<br>*3 - third cycle*|
|Programme NQF Level                    |no      |no      |one (per)  | *level 6*<br>*level 7* |
|**Workload expressed in ECTS Credits** |no      |yes     |one (per)  | *5*<br>*20* |
|**Assessment and certification**       |no      |yes     |one (per)  | *Attendance certificate*<br>*2* |
|Learning outcomes - ESCO               |no      |no      |many (per) | *http://data.europa.eu/esco/skill/b1115b14-fa16-4c1e-be6c-91fd49a1808b* |
|Learning outcomes description          |no      |no      |one (per)  | *Digitise and scan lasts. Work with files in various CAD systems. Produce 3D models of heels and create 2D computer aided designs. |
|Field of study                         |no      |no      |one (per)  | *032*<br>*http://data.europa.eu/esco/isced-f/0588* |

### Programme Identification

* Local Programme Identifier (<code>programme[n].identifier[1]</code>; not required; string)  
  One local programme identifier may be provided for each programme associated with the submitted report. Once the identifier has been submitted, the agency can identify reports on the same programme in the system.

    *e.g. 61*  
    *e.g. 60800*

### Programme Name and Qualification

Exactly one primary programme name must be provided for each programme associated with the report. The programme name should be accompanied by a qualification title in the same language (information inserted in the Programme qualification field). Agencies may also provide alternative or other language versions of the programme name and/or qualification. The primary name will be used for display.

The Programme Name field should only contain information on the name (further details on the qualification, level etc. should be provided in the other fields as presented below). 

* **Primary Programme Name(\*)** (<code>programme[n].name_primary</code>; conditionally required; string)  
  Exactly one primary name must be provided for each programme associated with the submitted report. It is recommended to provide the primary program name in English.

    *e.g. Medical Natural Sciences*

* Programme Qualification (<code>programme[n].qualification_primary</code>; not required; string)  
  The qualification offered by each programme should be recorded in the same language that is used for primary name.

    *e.g. Master of Medicine*  
    *e.g. Nano degree in C++*

* Programme Name Alternative (<code>programme[n].name_alternative[n]</code>; not required; string)  
  One or more alternative or other language names may be provided for each programme associated with the submitted report, e.g. in the local language.

    *e.g. Arts-specialist in opleiding*

* Programme Qualification Alternative (<code>programme[n].qualification_alternative[n]</code>; not required; string)  
  The qualification offered by each programme may be recorded in the same language that is used for the alternative name version.

    *e.g. Master in de specialistische geneeskunde*  
    *e.g. Micro-credential in basics in CAD*

### Programme Location

Information on the country/ies where each programme is located should be provided **only if different from the provider country**.

* Programme Country (<code>programme[n].country[n]</code>; not required; string)  
  The one or more countries where the programme is located should be provided if different from the provider's country. The country/ies should be provided in the form of an ISO 3166 alpha2 or ISO 3166 alpha3 country code (see [ISO 3166-1 standard](https://en.wikipedia.org/wiki/ISO_3166-1)).

    *e.g. BE*  
    *e.g. BEL*

### Programme Qualification Level

Information on the qualification level of each programme must be provided as a standardised level (based on the QF-EHEA levels); agencies may also choose to indicate the NQF level for each programme.

* **Degree outcome\*** (<code>programme[n].degree_outcome</code>; required \*; string)  
  The field specifies whether the programme leads to a full degree, recognised by the national authorities where the provider is based at.

    When a programme report is uploaded solely for an "other provider", the value of the field must be "No" (= no full degree). If the value is marked as "yes", the report upload will be automatically rejected.

    |ID |value|description               |
    |:--|:----|:-------------------------|
    | 1 |Yes  |Fully recognised degree   |
    | 2 |No   |No fully recognised degree|

    When a report is shown on the public DEQAR website (as well as in the Web API), three programme types are distinguished based on the degree outcome and workload of the programme:

    | Degree outcome | Workload   | Programme type shown             |
    |:---------------|:-----------|:---------------------------------|
    | Yes            | regardless | Full recognised degree programme |
    | No             | < 60 ECTS  | Micro-credential                 |
    | No             | ≥ 60 ECTS  | Other provision                  |

    > \* This field was recently added to the current DEQAR data model. In order to be backwards-compatible and not to break existing implementations, this field is currently not required, but will become required in the next version of DEQAR APIs (expected in September 2024). The current default is "yes" for programmes offered by HEIs, as it is considered as leading to a full degree unless specified otherwise. The current default is "no" for programmes offered by other providers, as micro credentials do not lead to a full degree.

* **Programme Qualification Level\*** (<code>programme[n].qf_ehea_level</code>; required \*; string)  
  A single standardised qualification level must be provided for each programme in the form of either a level name or level ID. These levels are based on the [Framework for Qualifications of the European Higher Education Area (QF-EHEA)](https://www.ehea.info/page-qualification-frameworks), the [European Qualifications Framework (EQF)](https://europa.eu/europass/en/europass-tools/european-qualifications-framework) and the [International Standard Classification of Education (ISCED)](https://uis.unesco.org/en/topic/international-standard-classification-education-isced).

    |ID |name (QF-EHEA) |equivalent to   |
    |:--|:--------------|:---------------|
    |0  |short cycle    | EQF 5, ISCED 5 |
    |1  |first cycle    | EQF 6, ISCED 6 |
    |2  |second cycle   | EQF 7, ISCED 7 |
    |3  |third cycle    | EQF 8, ISCED 8 |

    > \* This field was not required previously. In order to be backwards-compatible and not to break existing implementations, this field is currently not required for programmes leading to a full degree, but only for programmes not leading to a full degree (= micro-credentials). This field will become fully required in the next version of DEQAR APIs.

* Programme NQF Level (<code>programme[n].nqf_level</code>; required, string)  
  A single national qualification framework (NQF) level may be provided for each programme.

    *e.g. level 6*  
    *e.g. level 7*

### Programme Details

* **Workload expressed in ECTS Credits\*** (<code>programme[n].workload_ects</code>; conditionally required; string)  
  The workload as number of ECTS credits for programmes that do not lead to a full degree (i.e. micro credentials) must be provided to indicate the volume of learning. For programmes that do not bear ECTS, the workload could be calculated using the following tool: [ECTS calculator](https://www.germangradecalculator.com/ects-calculator/).

    This field is **required** for programmes not leading to a full degree (e.g. micro-credentials) and optional otherwise.

    *e.g. 15*

* **Assessment and certification\*** (<code>programme[n].assessment_certification</code>; conditionally required; string)  
  A programme that does not lead to a full degree could still have a formal outcome (e.g. a micro-credential).

    The field is **required** for programmes not leading to a full degree (e.g. micro-credentials) and **must be empty** for programmes leading to a full degree.

    The following scenarios are possible:

    |ID |Name                             |Description |
    |:--|:--------------------------------|:-----------|
    |1  |Attendance certificate           |The course does not involve an assessment of the acquired knowledge. Learner's attendance to the classes is considered as sufficient for obtaining a certificate. |
    |2  |Assessment based certificate     |The course involves an assessment of the acquired knowledge, The learner is awarded a certificate based on their achievements in the assessment(s). |
    |3  |No assessment and no certificate |No certificate is awarded |


* Learning outcomes - ESCO (<code>programme[n].learning_outcome[n]</code>; not required; string)  
  DEQAR uses the [European Skills, Competences, Qualifications and Occupations (ESCO)](https://esco.ec.europa.eu/en) classification of skills and competences as the preferred and interoperable way to specify the learning outcomes of a programme.

    A Uniform Resource Identifier (URI) of an ESCO skill may be provided for each learning outcome. For multiple learning outcomes in the CSV file, copy paste the columns and change the number in the brackets for every next value (i.e. n+1), see [above](#).

    > **Validation:** DEQAR expects URIs that are valid in ESCO version 1.1.1. Any URIs submitted are validated by making a request to `https://ec.europa.eu/esco/api/resource/skill?selectedVersion=v1.1.1&uri=[provided URI]` and - if successful - verifying that the object is part of the concept scheme `http://data.europa.eu/esco/concept-scheme/skills`; agencies may use the same steps to perform internal validation.
    >
    > Example of validation logic with http & jq utilities:
    >
    > `http "https://ec.europa.eu/esco/api/resource/skill?selectedVersion=v1.1.1&uri=http://data.europa.eu/esco/skill/b1115b14-fa16-4c1e-be6c-91fd49a1808b" | jq '._links.isInScheme | any(.uri == "http://data.europa.eu/esco/concept-scheme/skills")'`

    At report submission stage, any URI starting with `http://data.europa.eu/esco/skill/` is accepted; full validation is performed asynchronously. Invalid URIs will be discarded from the database and a corresponding note will appear in the report update log (see Record History in the admin interface after opening a report and clicking Show Info).

    *e.g. Using computer aided design and drawing tools: http://data.europa.eu/esco/skill/b1115b14-fa16-4c1e-be6c-91fd49a1808b*

* Learning outcomes description (<code>programme[n].learning_outcome_description</code>; not required; string)  
  Free text field to describe the programme's learning outcomes. This can be complementary to learning outcomes described in terms of ESCO skills, represent a summary of those or be used where the learning outcomes cannot be described in terms of ESCO skills.

    *e.g. Digitise and scan lasts. Work with files in various CAD systems. Produce 3D models of heels and create 2D computer aided designs. Grade and obtain the size series. Prepare technical specifications for manufacturing. Produce 2D and 3D computer aided engineering designs and technical drawings of moulds for vulcanised and injected heels. Export the files of the virtual models to 3D printers, CAM or CNC systems.*

* Field of study (<code>programme[n].field_study</code>; not required, string)  
  DEQAR is using the International Standard Classification of Education (ISCED) framework (2013) for assembling the provider of education programmes and related qualifications by levels and fields of education. ESCO uses ISCED-F to organise/categorise the knowledge pillar of skills.

    A 2-digit (broad field), 3-digit (narrow field) or 4-digit (detailed field) code of the ISCED 2013 classification or a URI from the ESCO taxonomy can be used to indicate the field of study.

    > **Validation**: a numerical ISCED-F code is first transformed into an ESCO URI by simple prefixing of `http://data.europa.eu/esco/isced-f/`. The (submitted or generated) URI is then validated against ESCO version 1.1.1 by making a request to `https://ec.europa.eu/esco/api/resource/skill?selectedVersion=v1.1.1&uri=[provided URI]` and - if successful - verifying that the object is part of the concept scheme `http://data.europa.eu/esco/concept-scheme/isced-f`; agencies may use the same steps to perform internal validation.
    >
    > Example of validation logic with http & jq utilities:
    >
    > `http "https://ec.europa.eu/esco/api/resource/skill?selectedVersion=v1.1.1&uri=http://data.europa.eu/esco/isced-f/0588" | jq '._links.isInScheme | any(.uri == "http://data.europa.eu/esco/concept-scheme/isced-f")'`

    At report submission stage, any 2, 3 or 4-digit numerical code or URI starting with `http://data.europa.eu/esco/isced-f/` is accepted; full validation is performed asynchronously. Invalid URIs will be discarded from the database and a corresponding note will appear in the report update log (see Record History in the admin interface after opening a report and clicking Show Info).

    *e.g. 032*  
    *e.g. 0111*  
    *e.g. http://data.europa.eu/esco/isced-f/0588*

