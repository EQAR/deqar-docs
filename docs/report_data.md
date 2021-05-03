# Report Data Elements

Agencies are asked to prepare data on quality assurance reports for submission to DEQAR. A submission object is data related to a single report and is used during ingest to populate report records and to establish linkages inside the system. Submission objects can be packaged together for batch submission.

Though they are used mostly to introduce new report records into DEQAR, submission objects can also be used to [update information on existing records](data_submission.md#updating-reports) through batch submission. Deletion of existing records can be requested, but final deletion can only be performed by DEQAR administrators.

Below we provide a full list of the data elements that can make up a submission object. It is important to note that the below list is exhaustive, including all possible elements. Required data elements are listed in **bold** with a \* , conditionally required data elements in **bold** with a (\*). We use the terminology:

* "must" to denote that an element is required or required in certain situations
* "should" to denote that an element is highly recommended
* "may" to denote that an element is optional

(See [RFC 2119 Best Current Practice](https://tools.ietf.org/html/rfc2119).)

The structure of the elements below best reflects our CSV template. To see how these elements are arrayed in JSON for API submission, see our JSON definition at:

<https://backend.deqar.eu/submissionapi/v1/swagger/>

Please note that new records for institutions not currently represented in DEQAR should be submitted separately beforehand. Please use the dedicated [CSV template described above](institution_data.md#how-to-provide-data).

|ELEMENT NAME |REQUIRED |ONE/MANY |EXAMPLE |
|:--------------------------------------------|:------------|:---------|:-----------------------|
|**Agency\*** |yes |one |*AAQ*<br>*33* |
|DEQAR Report ID |no |one |*000786* | |Local Report Identifier |no |one |*QAA1153-March15* |
|**Activity(\*)** |conditionally|one |*institutional audit*<br>*programme evaluation*<br>*2*<br>*8*|
|**Activity Local Identifier(\*)** |conditionally|one |*inst_aud* |
|**Status\*** |yes |one |*1 - part of obligatory EQA system*<br>*2 - voluntary*|
|**Decision\*** |yes |one |*1 - positive*<br>*2 - positive with conditions or restrictions*<br>*3 - negative*<br>*4 - not applicable*|
|**Valid from\*** |yes |one |*2015-01-15* |
|Valid to |no |one |*2020-01-15* |
|**Date Format\*** |yes |one |*%d/%m/%y* |
|Link |no |one |*http://srv.aneca.es/ListadoTitulos/node/1182321350*|
|Comment |no |one |*Evaluation undertaken with Musique.*<br>*Programme group reports are created for programmes with a similar profile across the entire sector on a 7-year rotating basis.*|

## Agency

A single creating agency must be clearly identified for each report. The creating agency is often, though not always, the same as the submitting agency (see [Agency Identifiers](architecture_data_model.md#agency-identifiers)).

- **Agency\*** (<code>agency</code>; required; string)  
  The agency which created the report must be provided for each report as an agency acronym or as a DEQAR agency ID. This allows the report to be linked to an existing agency record and makes it possible to validate and transform the submitted data in accordance with the agency's profile.  
  *e.g. AAQ*  
  *e.g. 33*

## Report Identifier

A report identifier must be used when submitting updates to an existing report in CSV or JSON. Each report can be identified using an agency's local identifiers or through DEQAR report IDs, which are assigned at upload. It is recommended that agencies submit local report identifiers with every submission object (see [Report and Programme Identifiers](architecture_data_model.md#report-and-programme-identifiers)).

* DEQAR Report ID (<code>report_id</code>; not required; string)  
  Each uploaded report is assigned a unique DEQAR report ID. This may be used to submit updates to existing reports or to promote synchronisation with an agency's local system.  
  *e.g. 000786*

* Local Report Identifier (<code>local_identifier</code>; not required; string)  
  The report identifier used in the agency's local system should be provided for each report. This may be used to submit updates to existing reports or to promote synchronisation with the agency's local system; the local report identifier is particularly useful in the identification of invalid submission objects.  
  *e.g. QAA1153-March15*

## Activity

A single activity must be assigned to each report. Activities are selected from the agency's pre-defined list of activities and should be provided as a DEQAR value (as either a string value or a DEQAR activity ID). Optionally an agency may choose to provide local identifiers for its own activities; before these can be used for submission, these identifiers should be assigned through the agency record in the administrative interface (see [Role of Standards and Identifiers: Other Identifiers](architecture_data_model.md#other-identifiers). If both elements are submitted for a single report, then the DEQAR value will be used by the system.

* **Activity(\*)** (<code>activity</code>; conditionally required; string)  
  A DEQAR activity value may be provided as an activity name or DEQAR activity ID for each report. The activity is used to validate the structure of submitted report data.  
  *e.g. institutional audit*  
  *e.g. programme evaluation*  
  *e.g. 2*  
  *e.g. 8*  

* **Activity Local Identifier(\*)** (<code>activity_local_identifier</code>; conditionally required; string)  
  A local activity identifier may optionally be provided in place of a DEQAR activity value for each report. The local activity identifier may be used to validate the structure of submitted report data. (Note: local activity identifiers need to be assigned through the administrative interface before they can be used in submission.)  
  *e.g. inst_aud*  

Each activity is classified as one of four activity types (<code>activity_type</code>). These classifications determine the structure of the report record.

|Type |Report record structure |
|:----------------------|:------------------------------|
|institutional |at least one institution<br>no programme|
|institutional/programme|one and only one institution<br>at least one programme|
|programme |one and only one institution<br>at least one programme|
|joint programme |at least two institutions<br>at least one programme|

## Details

Each report must be assigned a single status and a single decision value. Together these elements signal the role, status and nature of the report. Status and decision values may be provided as either string values or DEQAR IDs.

* **Status\*** (<code>status</code>; required; string)  
  The status must be provided as either a DEQAR status name or a DEQAR status id for each report. The status specifies whether the report is part of the obligatory EQA system in the country of the institution or whether the institution has undertaken it voluntarily.  
  **NB** The status "part of obligatory EQA system" may only be used in the EHEA.

|ID |name |
|:--|:-----------------------------|
|1 |part of obligatory EQA system |
|2 |voluntary |

* **Decision\*** (<code>decision</code>; required; string)  
  The decision must be provided as either a DEQAR decision name or a DEQAR decision id for each report. The decision records the final result of the QA procedure/report.

|ID |name |
|:--|:---------------------------------------|
|1 |positive |
|2 |positive with conditions or restrictions|
|3 |negative |
|4 |not applicable |

* Comment (<code>other_comment</code>; not required; string)  
  The optional comment can contain important information on the report that cannot be represented in the structured data, e.g. involvement of other partner agencies or any specific notes about the QA procedure.  
  *e.g. Evaluation undertaken in cooperation with MusiQuE.*  
  *e.g. Programme group reports are created for programmes with a similar profile across the entire sector on a 7-year rotating basis.*

## Validity

Each report must have an associated date defining the start of its validity. A date defining the end of the report's validity should also be provided. In the cases that the end date is left open, the report will be treated as valid for six years from the start of its validity, after which it will be archived. DEQAR uses a special notation to denote the date format. This allows each agency to signal the date format it uses; this must be provided for each report.

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
|**File Original Location(\*)** |conditionally|many |*http://estudis.aqu.cat/MAD2014_UPC_es.pdf*|
|File Display Name |no |one (per) |*Report*<br>*Evaluation*<br>*MAD2014_UPC_es.pdf*|
|**Report Language\*** |yes |many (per)|*es*<br>*spa* |

* **File Original Location(\*)** (<code>file[n].original_location</code>; conditionally required; string)  
  At least one PDF file should be provided with each submitted report in the form of a URL. Optionally, PDF files can be uploaded through the API or user interface.  
  *e.g. http://estudis.aqu.cat/MAD2014_UPC_es.pdf*

    > The URL *SHOULD* return the [HTTP content-type header](https://developer.mozilla.org/de/docs/Web/HTTP/Headers/Content-Type) `application/pdf` upon a *HEAD* request. The URL *MUST* return `application/pdf` upon a *GET* request. If another content-type is reported, the file will not be downloaded and saved.
    >
    >  The maximum filesize is 10MB.

* File Display Name (<code>file[n].display_name</code>; not required; string)  
  A single file display name may be provided for each PDF report file, used for the file link in DEQAR. If no display name is provided, then the file name will be used for display instead.  
  *e.g. Report*  
  *e.g. Evaluation*  
  *e.g. MAD2014_UPC_es.pdf*

    > This should be a short and generic term (such as “Report and Decision”, “Evaluation Report”, “Accreditation Decision”, “Summary report”, ...). The display name should *not* repeat the name of the institution or programme addressed in the report.

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

## Institution(s)

Each report must be associated with at least one institution. The record(s) for the institution(s) need(s) to already exists in DEQAR, see [the previous section on adding missing insitutions to DEQAR](institution_data.md).

Preferably, the DEQARINST ID or the ETER ID should be provided to identify the institution(s).

Optionally, an agency may choose to use local or national identifiers for institutions. Before these can be used for submission, local identifiers should be assigned to existing institution records through the administrative interface or provided in bulk to the EQAR secretariat.

Only one institution identifier should be submitted for each institution in the submission object (see [Institution Identifiers](architecture_data_model.md#institutional-identifiers)). If more than one identifying element is submitted, then the DEQARINST ID will be used to establish internal linkage, followed by the ETER ID, followed by the local identifier.

|ELEMENT NAME |REQUIRED |ONE/MANY |EXAMPLE |
|:--------------------------------------------|:------------|:---------|:-----------------------|
|**DEQARINST ID(\*)** |conditionally|one (per) |*DEQARINST0034* |
|**ETER ID(\*)** |conditionally|one (per) |*BG0001* |
|**Institutional Identifier(\*)** |conditionally|one (per) |*HCERES21*<br>*AT0004* |
|Identifier Resource|conditionally|one (per) |*SI-ETER.BAS.NATID*<br>*Erasmus* |

* **DEQARINST ID(\*)** (<code>institution[n].deqar_id</code>; conditionally required; string)  
  Each institution already described in DEQAR is assigned a DEQARINST ID. The DEQARINST ID may be used to establish a link between submitted report data and an existing institution record.  
  *e.g. DEQARINST0034*

* **ETER ID(\*)** (<code>institution[n].eter_id</code>; conditionally required; string)  
  Each institution described in OrgReg or ETER is assigned an ETER ID (see [Research infrastructure for research and innovation policy studies - RISIS](http://datasets.risis.eu/) or [European Tertiary Education Register - ETER](https://www.eter-project.com/)). The ETER ID may be used to establish a link between submitted report data and an ETER record in DEQAR.  
  *e.g. BG0001*

* **Institutional Identifier(\*)** (<code>institution[n].identifier[1]</code>; conditionally required; string)  
  A local identifier is any identifier used by the Agency to identify an institution, while other identifiers can be recorded in DEQAR for use by all agencies. These may optionally be used in the place of a DEQARINST ID or ETER ID to establish a link between submitted report data and an existing institution record. (Note: local institution identifiers need to be assigned through the administrative interface or in bulk through the EQAR secretariat before they can be used in submission; other identifiers can be consulted in the administrative interface and can be assigned in consultation with the EQAR secretariat.)  
  *e.g. HCERES21*  
  *e.g. AT0004*

* Identifier Resource (<code>institution[n].resource[1]</code>; conditionally required; string)  
  If the identifier you use is not a local identifier of your agency, you need to provide its corresponding resource tag. The value for this field can be consulted through the administrative interface.  
  *e.g. DE-HRK*  
  *e.g. SI-ETER.BAS.NATID*  
  *e.g. Erasmus*

## Programme Data

Information on one or more programmes is required for all reports with the assigned activity types: **institutional/programme**; **programme**; or **joint programme**. As a rule, programme information must be entered anew for each report, though DEQAR allows agencies to assign local programme identifiers in order to track reports on the same programme or to reuse programme information in later reports.

A local identifier may be submitted along with the report data in CSV or JSON; additional local identifiers can also be assigned through the administrative interface. (Note, if no existing identifier is used, then **as a minimum the programme name must be provided** for programme data to be valid.)

|ELEMENT NAME |REQUIRED |ONE/MANY |EXAMPLE |
|:--------------------------------------------|:------------|:---------|:-----------------------|
|Local Programme Identifier |no |many (per)|*61*<br>*60800* |
|**Primary Programme Name(\*)** |conditionally|one (per) |*Arts-specialist in opleiding*|
|Programme Qualification |no |one (per) |*Master in de specialistische geneeskunde*|
|Programme Name Alternative |no |many (per)|*Medical Natural Sciences*|
|Programme Qualification Alternative |no |many (per)|*Master of Medicine* |
|Programme Country |no |many (per)|*BE*<br>*BEL* |
|Programme NQF Level |no |one (per) |*level 6*<br>*level 7* |
|Programme QF-EHEA Level |no |one (per) |*0 - short cycle*<br>*1 - first cycle*<br>*2 - second cycle*<br>*3 - third cycle*|

### Programme Identification

An identifier may be submitted with programme information to allow the agency to identify reports on the same programme or to reuse the same programme information in a later record (see [Report and Programme Identifiers](architecture_data_model.md#report-and-programme-identifiers)). (Note: if an existing identifier is submitted with new programme information, the previous data will be used in place of the new.)

* Local Programme Identifier (<code>programme[n].identifier[1]</code>; not required; string)  
  One local programme identifier may be provided for each programme associated with the submitted report. Once the identifier has been submitted, the agency can identify reports on the same programme in the system and may reference it in later reports to reuse the same programme data.  
  *e.g. 61*  
  *e.g. 60800*

### Programme Name and Qualification

One and only one primary programme name must be provided for each programme associated with the report. The programme name should be accompanied by a qualification title in the same language. Agencies may also provide alternative or other language versions of the programme name and/or qualification. The primary name will be used for display.

* **Primary Programme Name(\*)** (<code>programme[n].name_primary</code>; conditionally required; string)  
  One and only one primary name must be provided for each programme associated with the submitted report. It is recommended to provide the primary program name in English.  
  *e.g. Medical Natural Sciences*

* Programme Qualification (<code>programme[n].qualification_primary</code>; not required; string)  
  The qualification offered by each programme should be recorded in the same language that is used for primary name.  
  *e.g. Master of Medicine*

* Programme Name Alternative (<code>programme[n].name_alternative[n]</code>; not required; string)  
  One or more alternative or other language names may be provided for each programme associated with the submitted report, e.g. in the local language.  
  *e.g. Arts-specialist in opleiding*

* Programme Qualification Alternative (<code>programme[n].qualification_alternative[n]</code>; not required; string)  
  The qualification offered by each programme may be recorded in the same language that is used for the alternative name version.  
  *e.g. Master in de specialistische geneeskunde*

### Programme Location

Information on the country/ies where each programme is located should be provided if different from the host institution country.

* Programme Country (<code>programme[n].country[n]</code>; not required; string)  
  The one or more countries where the programme is located should be provided if different from the institution country. The country/ies should be provided in the form of an ISO 3166 alpha2 or ISO 3166 alpha3 country code (see [ISO 3166-1 standard](https://en.wikipedia.org/wiki/ISO_3166-1)).  
  *e.g. BE*  
  *e.g. BEL*

### Programme Qualification Level

Information on the qualification framework level of each programme can be provided as a QF-EHEA level; agencies may also choose to provide the NQF level for each programme.

* Programme NQF Level (<code>programme[n].nqf_level</code>; not required, string)  
  A single national qualification framework (NQF) level may be provided for each programme.  
  *e.g. level 6*  
  *e.g. level 7*

* Programme QF-EHEA Level (<code>programme[n].qf_ehea_level</code>; not required; string)  
  A single QF-EHEA level should be provided for each programme in the form of either a QF-EHEA level name or QF-EHEA level id (see [Framework for Qualifications of the European Higher Education Area](http://ecahe.eu/w/index.php/Framework_for_Qualifications_of_the_European_Higher_Education_Area).

  |ID |name |
  |:--|:-----------|
  |0 |short cycle |
  |1 |first cycle |
  |2 |second cycle|
  |3 |third cycle |

