## Data Preparation

Agencies are asked to prepare data on quality assurance reports for submission to DEQAR.  Each agency has the choice to manually submit records one by one through the DEQAR administrative interface or to submit larger batches of data in CSV or JSON format. In the latter cases, the agency must prepare Submission Objects before uploading to DEQAR. A submission object is data related to a single report and is used during ingest to populate report records and to establish linkages inside the system. (Note: a submission object cannot be considered as a report record per se because it may include data stored in other entities as well.) 

Submission objects can be packaged together for batch submission. Though they are used mostly to introduce new report records into DEQAR, submission objects can also be used to update information on existing records through batch submission. Deletion of existing records can only be performed through the administrative interface. 

Below we provide a full list of the data elements that can make up a submission object. It is important to note that the below list is exhaustive, including all possible elements. Required data elements are listed in **bold** with a \* , conditionally required data elements in **bold** with a (\*).  We use the terminology:

 - "must" to denote that an element is required or required in certain situations
 - "should" to denote that an element is highly recommended
 - "may" to denote that an element is optional

### Report Data Elements  

#### Report Creation

A single creating agency must be clearly identified for each report. The creating agency is often, though not always, the same as the submitting agency.  

- **Agency\*** (<code>agency</code> or <code>agency_id</code>; required; string)  
The agency which created the report must be provided for each report as an agency acronym or as a DEQAR agency ID. This allows the report to be linked to an existing agency record and makes it possible to validate and transform the submitted data in accordance with the agency's profile.  
*e.g. AAQ*  
*e.g. 33*  

#### Report Identification 

A report identifier must be used when submitting updates to an existing report in CSV or JSON. Each report can be identified using an agency's local identifiers or through DEQAR report IDs, which are assigned at upload. It is recommended that agencies submit local report identifiers with every submission object.  

- DEQAR Report ID (<code>deqar_id</code>; not required; string)  
Each uploaded report is assigned a unique DEQAR report ID. This may be used to submit updates to existing reports or to promote synchronisation with an agency's local system.  
*e.g. 000786* 

- Local Identifier (<code>local_identifier</code>; not required; string)  
The report identifier used in the agency's local system should be provided for each report. This may be used to submit updates to existing reports or to promote synchronisation with the agency's local system; the local report identifier is particularly useful in the identification of invalid submission objects.  
*e.g. QAA1153-March15*

#### Report Activity

A single activity must be assigned to each report. Activities are selected from the agency's pre-defined list of activities and should be provided as a DEQAR value (as either a string value or a DEQAR activity ID). Optionally an agency may choose to provide local identifiers for its own activities; before these can be used for submission, these identifiers should be assigned through the agency record in the administrative interface. If both elements are submitted for a single report, then the DEQAR value will be used by the system.  

- **Activity(\*)** (<code>activity</code> or <code>activity_id</code>; conditionally required; string)  
A DEQAR activity value may be provided as an activity name or DEQAR activity ID for each report. The activity is used to validate the structure of submitted report data.  
*e.g. institutional audit*  
*e.g. programme evaluation*  
*e.g. 2*  
*e.g. 8*  

- **Activity Local Identifier(\*)** (<code>activity_local_identifier</code>; conditionally required; string)  
A local activity identifier may optionally be provided in place of a DEQAR activity value for each report. The local activity identifier may be used to validate the structure of submitted report data. (Note: local activity identifiers need to be assigned through the administrative interface before they can be used in submission.)  
*e.g. inst_aud*  

Each activity is classified as one of four activity types (<code>activity_type</code>). These classifications determine the structure of the report record.  

|Type                   |Report record structure        |               
|:----------------------|:------------------------------| 
|institutional          |at least one institution<br>no programme|
|institutional/programme|one and only one institution<br>at least one programme|
|programme              |one and only one institution<br>at least one programme|
|joint programme        |at least two institutions<br>at least one programme|  

    	
#### Report Details

Each report must be assigned a single status and a single decision value. Together these elements signal the role, status and nature of the report.  Status and decision values may be provided as either string values or DEQAR IDs.  

- **Status\*** (<code>status</code> or <code>status_id</code>; required; string)  
The status must be provided as either a DEQAR status name or a DEQAR status id for each report. The status specifies whether the report is part of the obligatory EQA system in the country of the institution or whether the institution has undertaken it voluntarily.  

   |ID |name                          |
   |:--|:-----------------------------|
   |1  |part of obligatory EQA system | 
   |2  |voluntary                     |  
   		
- **Decision\*** (<code>decision</code> or <code>decision_id</code>; required; string)  
The decision must be provided as either a DEQAR decision name or a DEQAR decision id for each report. The decision records the final result of the QA procedure/report.  

   |ID |name                                    |
   |:--|:---------------------------------------|
   |1  |positive                                | 
   |2  |positive with conditions or restrictions|
   |3  |negative                                |
   |4  |not applicable                          |  

#### Report Validity

Each report must have an associated date defining the start of its validity. A date defining the end of the report's validity should also be provided. In the cases that the end date is left open, the report will be treated as valid for six years from the start of its validity, after which it will be archived. DEQAR uses a special notation to denote the date format. This allows each agency to signal the date format it uses; this must be provided for each report.
		
- **Valid from\*** (<code>valid_from</code>; required; date)  
A valid from date marking the starting date of the report's validity must be provided for each report. This date is used to generate an archiving date when no valid to date is provided.  
*e.g. 2015-01-15*
		
- Valid to (<code>valid_to</code>; not required; date)  
A valid to date marking the ending date of the report's validity should be provided for each report. This date determines when report data will be archived in DEQAR. If no valid to date is assigned, then the report will be treated as valid for six years after the valid from date.  
*e.g. 2020-01-15*
		
- **Date Format\*** (<code>date_format</code>; required; string)  
A date format  must be provided for each report. Dates may be submitted in any standard format; the format should be represented as a combination of the following characters:  

   |symbol(s)| meaning                               |example                      |      
   |:--------|:--------------------------------------|:----------------------------|
   |%d       |day as expressed in two digits         |02                           | 
   |%-d      |day as expressed in one or two digits  |2                            |
   |%m       |month as expressed in two digits       |05 for May                   |
   |%-m      |month as expressed in one or two digits|5 for May and 12 for December|
   |%Y       |year as expressed in four digits       |2014                         |
   |%y       |year as expressed in two digits        |14                           |
   |d-%m-%Y  |                                       |04-01-2014                   |
   |%d/%m/%y |                                       |04/01/14                     |
   |%Y-%m-%d |                                       |2015-01-15                   |  

#### Report Link

One or more URL links may be provided to alternative views of the report data on the agency's website or other webpage(s) in order to provide more context. A display name may be provided for each URL link. The linked text will display on DEQAR under the display name label provided or, if no name is provided, under generic text provided by DEQAR. 

- Link (<code>link</code>, not required, string)  
One or more URL links may be provided for each report to the same report presented on other sites in order to provide more context to the report.  
*e.g. http://srv.aneca.es/ListadoTitulos/node/1182321350*
		
- Link Display Name (<code>link_display_name</code>, not required, string)  
A display name may optionally be provided for each link to the report on other sites. If no display name is provided, then EQAR will supply generic text.  
*e.g. General information on this programme.*

### Institution Identification (linking to existing record)  

Each report must be associated with at least one institution. If a record for the institution already exists in DEQAR, a DEQARINST ID or an ETER ID should be provided to establish a link to the existing record. Optionally an agency may choose to provide a local or national identifier for an institution; before these can be used for submission, local identifiers should be assigned to existing institution records through the administrative interface or provided in bulk to the EQAR secretariat. Only one institution identifier should be submitted for each institution in the submission object. If more than one identifying element is submitted, then the DEQARINST ID will be used to establish internal linkage, followed by the ETER ID. If no record for the institution exists in DEQAR, a new record can be created by filling in several descriptive elements (see [**Institution Data Elements**](https://docs.deqar.eu/submission_object_fields/#institution-data-elements) below). 
 
- **DEQARINST ID(\*)** (<code>institution.deqar_id</code>; conditionally required; string)  
Each institution already described in DEQAR is assigned a DEQARINST ID.  The DEQARINST ID may be used to establish a link between submitted report data and an existing institution record.  
*e.g. DEQARINST0034*  

- **ETER ID(\*)** (<code>institution.eter_id</code>; conditionally required; string)  
Each institution described in OrgReg or ETER is assigned an ETER ID (see [Research infrastructure for research and innovation policy studies - RISIS](http://datasets.risis.eu/) or [European Tertiary Education Register - ETER](https://www.eter-project.com/)). The ETER ID may be used to establish a link between submitted report data and  an ETER record in DEQAR.  
*e.g. BG0001*  
		
- **Local Institutional Identifier(\*)** (<code>institution.identifier</code>; conditionally required; string)  
A local identifier is any identifier used by the Agency to identify an institution. A local identifier may optionally be used in the place of a DEQARINST ID or ETER ID to establish a link between submitted report data and an existing institution record. (Note: local institution identifiers need to be assigned through the administrative interface or in bulk through the EQAR secretariat before they can be used in submission.)  
*e.g. HCERES21*  
*e.g. AT0004*  

### Institution Data Elements (new institution record) 
 
Each report must be associated with at least one institution. If a record for an institution does not already exist in DEQAR, the institution must be described with the elements below. (Note, **as a minimum the institution name, country and website must be provided** for a new record to be created.) Before a new record is created, data will be checked against institution data already in DEQAR. If a DEQAR institution record is identified as a match, the existing record will take precedence over submitted data.  

#### Institution Name

One and only one official institution name must be provided for each new institution record. Each official institution name that is in a non-Latin script should be accompanied by a transliterated version to support search and discovery. It is also recommended that agencies provide an English institution name for each new institution record. If provided, the English name will be used for display. An institution acronym may also be provided.  (Note: alternative or other language institution names can be provided through the administrative interface.)   

- **Official Institution Name(\*)** (<code>institution.name_official</code>; conditionally required; string)  
The official name of each institution in the original alphabet must be provided for every new institution record. The official name will be indexed for search and may be used as the primary institution name in the search interface if no English institution name is assigned.  
*e.g. Graz University of Technology*  
*e.g. Югозападен университет "Неофит Рилски"*  
*e.g. Πληροφορίες για τους αλλοδαπούς φοιτητές: Είσοδος και προγράμματα*  

- Official Institution Name, transliterated (<code>institution.name_official_transliterated</code>; not required; string)  
A romanised transliteration should be provided if the official institution name is in non-Latin script. If no romanised form is stored locally, then [ISO romanisation standards] (https://en.wikipedia.org/wiki/List_of_ISO_romanizations) can be used to created romanised forms.  If transliteration is not provided, access to the institution record through the search interface will be more limited.  
*e.g. Yugo-zapaden universitet "Neofit Rilski”*  
*e.g. Plirophoríes yia tous allodapoús phitités: Ísodos kai prográmmata*  

- English Institution Name (<code>institution.name_english</code>; not required; string)  
A single English institution name may be provided for each institution.	If provided, the English institution name will be used as the primary institution name in the search interface.  
*e.g. South-West University "Neofit Rilski", Blagoevgrad*  

- Institution Acronym (<code>institution.acronym</code>; not required; string)  
The official acronym for each institution may be provided. This will be indexed for search. 
*e.g. SWU*  
	
#### Location

One or more countries must be provided for each new institution record. One city may be provided to correspond with each country along with an optional latitude and longitude. In the case that the institution is located in more than one city in the same country, then this would require a separate country/city entry for each city.  

- **Institution Country(\*)** (<code>institution.country</code>; conditionally required; string)  
The country/ies where each institution is located must be provided for every new institution record. Each country must be provided using either an ISO 3166 alpha2 or ISO 3166 alpha3 country code (see [ISO 3166-1 standard](https://en.wikipedia.org/wiki/ISO_3166-1)). Institution countries will be indexed for search. 
*e.g. BG*  
*e.g. BGR*  
	
- Institution City (<code>institution.city</code>; not required; string)  
The city name, preferably in English, where the institution is located in each country may be provided for each institution record. If an institution is located in more than one city, then a separate country/city pairing should be entered for each city. Institution cities will be indexed for search.  
*e.g. Sofia*  

- Institution Latitude (<code>institution.latitude</code>; not required; float)  
- Institution Longitude (<code>institution.longitude</code>; not required; float)  
The exact latitude and longitude of the institution site or the general latitude and longitude of the city of the institution may also be provided for each institution record.  
*e.g. 48,208,356; 1,636,776*  

#### Level

The institution QF-EHEA levels may be provided for each institution. If QF-EHEA levels are provided, then *ALL* levels covered by the institution should be recorded. QF-EHEA levels may be provided as either string values or DEQAR IDs.  

- Institution QF-EHEA Level (<code>institution.qf_ehea_level</code>; not required; string)  
One or more institution QF-EHEA levels may be provided as either a DEQAR QF-EHEA level name or a DEQAR QF-EHEA level id for each institution record (see [Framework for Qualifications of the European Higher Education Area](http://ecahe.eu/w/index.php/Framework_for_Qualifications_of_the_European_Higher_Education_Area). These are the qualification framework levels at which each institution may award degrees. (Note: if QF-EHEA levels are provided, then all levels covered by the institution should be provided at the same time.)   

   |ID |name        |  
   |:--|:-----------|  
   |0  |short cycle |  
   |1  |first cycle |  
   |2  |second cycle|  
   |3  |third cycle |  

#### Website

One and only one website link must be provided for each new institution record. When possible, the root domain name of the institution website should be provided without language or other qualifiers.  

- **Institutional Website(\*)** (<code>institution.website_link</code>; conditionally required; string)  
The URL to the primary institution website or home page should be provided for every new institution record. The root domain name of the site should be used when possible.  
*e.g. http://www.swu.bg*  

### Programme Data Elements 
 
Information on one or more programmes is required for all reports with the assigned activity type: **institutional/programme**; **programme**; or **joint programme**. As a rule, programme information must be entered anew for each report, though DEQAR allows agencies to assign local programme identifiers in order to track reports on the same programme or to reuse programme information in later reports. A local identifier may be submitted along with the report data in CSV or JSON; additional local identifiers can also be assigned through the administrative interface. (Note, if no existing identifier is used, then **as a minimum the programme name must be provided** for programme data to be valid.)  

#### Programme Identification

Certain types of reports must include data on at least one associated programme. An identifier may be submitted with programme information to allow the agency to identify reports on the same programme or to reuse the same programme information in a later record. In the case that an existing identifier is later submitted with different programme information, the previous data will be used in place of the new.  

- Local Programme Identifier (<code>programme.identifier</code>; not required; string)  
One local programme identifier may be provided for each programme associated with the submitted report. Once the identifier has been submitted, the agency can identify reports on the same programme in the system and may reference it in later reports to reuse the same programme data.  
*e.g. 61*  
*e.g. 60800*  

#### Programme Name and Qualification

One and only one primary programme name must be provided for each programme associated with the report. The programme name should be accompanied by a qualification title in the same language. Agencies may also provide alternative or other language versions of the programme name and/or qualification. The primary name will be used for display.  

- **Primary Programme Name(\*)** (<code>programme.name_primary</code>; conditionally required; string)  
One and only one primary name must be provided for each programme associated with the submitted report. It is recommended to provide the primary program name in English or in the original language.  
*e.g. Arts-specialist in opleiding*  

- Programme Qualification (<code>programme.qualification_primary</code>; not required; string)  
The qualification offered by each programme should be recorded in the same language that is used for primary name.  
*e.g. Master in de specialistische geneeskunde*  
		
- Programme Name Alternative (<code>programme.name_alternative</code>; not required; string)  
One or more alternative or other language names may be provided for each programme associated with the submitted report.  
*e.g. Medical Natural Sciences*  

- Programme Qualification Alternative (<code>programme.qualification_alternative</code>; not required; string)  
The qualification offered by each programme may be recorded in the same language that is used for the alternative name version.  
*e.g. Master of Medicine*  

#### Programme Location

Information on the country/ies where each programme is located should be provided if different from the host institution country. 

- Programme Country (<code>programme.country</code>; not required; string)  
The one or more countries where the programme is located should be provided if different from the institution country. The country/ies should be provided in the form of an ISO 3166 alpha2 or ISO 3166 alpha3 country code (see [ISO 3166-1 standard](https://en.wikipedia.org/wiki/ISO_3166-1)).  
*e.g. BE*  
*e.g. BEL*  

#### Programme Level

Information on the qualification framework level of each programme can be provided as a QF-EHEA level; agencies may also choose to provide the NQF level for each programme.

- Programme NQF Level (<code>programme.nqf_level</code>; not required, string)  
A single national qualification framework (NQF) level may be provided for each programme.  
*e.g. level 6*  
*e.g. level 7*  

- Programme QF-EHEA Level (<code>programme.qf_ehea_level</code> or <code>programme.qf_ehea_level_id</code>; not required; string)  
A single QF-EHEA level should be provided for each programme in the form of either a QF-EHEA level name or QF-EHEA level id (see [Framework for Qualifications of the European Higher Education Area](http://ecahe.eu/w/index.php/Framework_for_Qualifications_of_the_European_Higher_Education_Area).    

  |ID |name        |  
  |:--|:-----------|  
  |0  |short cycle |  
  |1  |first cycle |  
  |2  |second cycle|  
  |3  |third cycle |  

### Preparing QA Report Files

DEQAR requires PDF versions of quality assurance reports for every submission object. Agencies can choose either to make files available for harvest or to upload files. In order to make files available for harvest, agencies must provide the URL for files already available on a public server. Alternatively, files may be submitted using the API or uploaded through the administrative interface. All reports must be submitted with data on the language(s) used in the report. A file display name can be provided as well.
		
- **File Original Location(\*)** (<code>file.original_location</code>; conditionally required; string)  
At least one PDF file should be provided with each submitted report in the form of a URL. Optionally, PDF files can be uploaded through the API or user interface.  
*e.g. http://estudis.aqu.cat/MAD2014_UPC_es.pdf*  

- File Display Name (<code>file.display_name</code>; not required; string)  
A single file display name may be provided for each PDF report file. This will be used for the file link in DEQAR. If no display name is provided, then the file name will be used for display instead.    
*e.g. Report*  
*e.g. Evaluation*  
*e.g. MAD2014_UPC_es.pdf*  

- **Report Language\*** (<code>file.report_language</code>; required; string)  
One or more languages must be provided for each file in the form of an ISO 639 1 (two-digit) or ISO 639 2 (three digit) language code (see [ISO 639-1 or ISO 639-2/B format](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)).  
*e.g. es*  
*e.g. spa*  

## Data Pipeline

### Data flow

All three submission methods are fully interoperable. That is, agencies may switch between different methods at any time, and data submitted via one method may be updated/altered via another method.

In general, irrespective of the submission method, all data inserted into DEQAR is handled following these steps:

 1. The Submission Request Object goes through the first level of validation;
 2. If the data format is invalid or the submitted identifiers cannot be resolved (see detailed [Validation Criteria](#validation-criteria) below), the record is rejected;
 3. Valid report data is populated in the appropriate tables;
 4. Sanity checks are run against pre-defined flagging criteria (see detailed [Flagging Criteria](#flagging-criteria) below), reports which contain conflicts are flagged;
 5. A Response Object (or array of objects) is sent back to the agency, containing:
	- detailed error descriptions for reports that were rejected;
	- identifiers of records that were created or identified (in the case of Institutions);
	- identifiers of newly created records (Reports, Report Files);
	- information on records where sanity checks found errors. 

### Validation criteria

In order for records making up a Submission Request Object to clear the first level of validation, they must meet the following criteria:

1. The **agency** that created the report (which may or may not be the agency submitting the records) must be clearly identified. The agency may be identified using an agreed upon acronym or a DEQAR agency ID which has been provided by the EQAR secretariat.
2. All **required data** must be present for each report. Required data for all records includes:
    1. ESG activity performed: provided as activity name, ID given by EQAR or as a local identifier. (see reference values)
    2. [Status of report](submission_object_fields.md#status), provided as text or as an ID
    3. [Decision](submission_object_fields.md#decision), provided as text or as an ID.
    4. Report valid from date, incl. [date format](submission_object_fields.md#date-format) used by the agency
    5. Language(s) of the report: At least one language for each report should be provided as a two- or three-digit [ISO 639-1 or 2/B code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). Ideally language information is provided along with the link to the location of the PDF file. 
    6. Institution: a report must relate to at least one institution.
        - Institutions already recorded in DEQAR should be identified by their DEQARINST ID, their ETER ID or an Agency Local Identifier (i.e. the identifier under which the Institution is listed in the agency’s local system; this can only be used if the identifier has previously been provided to DEQAR)
        - A minimum Institution record must be provided in the Insitution is not yet recorded in DEQAR and must contain:
            - Official Name of the Institution (in original language),
            - Country of Location for the Institution (as [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) alpha-2 or alpha-3 country code)
            - Website Link for the Institution.
        The identified/created Institution's DEQARINST and ETER IDs are returned as part of the Response Object for each submission.
    7. For reports on programmes, the Programme Name (in whatever language it is stored by the Agency).
3. At this point, **dependencies** between elements will be checked as well as any **limits on the cardinality** of each element, see [Data Preparation](submission_object_fields.md).
4. Submitted data must be of the **correct type, form and value range/options**, see [Data Preparation](submission_object_fields.md).
5. Submitted data must **align with Agency Profile** information, specifically report validation date should fall after Agency EQAR registration dates and activities should match defined ESG activities for the Agency.
6. Submitted data must **meet basic data integrity rules** for the system, i.e. there should be one and only one creating agency and at least one institution covered by each report.
7. Submitted report data must meet the structural **requirements determined by the listed ESG activity**. Each report is categorised as one of four activity types based on the Activity to which it belongs, and the record structure must reflect this typology:
    - Report records with Activity Type “Institutional”: 
        - contain required institution data on at least one institution
        - contain no programme data
    - Report records with Activity Type “Programme” or “Institutional/Programme”:
        - contain data on one and only one institution 
        - contain data on at least one programme
    - Report records with Activity Type “Joint Programme”:
        - contain data on more than one institution 
        - contain data on at least one programme

Records not meeting all of the above criteria will be rejected. The system will return a Response Object that clearly identifies rejected records, including information on the source of the problem. Importantly, the rejection of one or more records does not imply the failure of the whole Submission Request Object.

### Flagging criteria

Once the records making up the Submission Request Object clear the first level of validation, they are officially ingested into the system. DEQAR records are populated with valid data and final sanity checks are run on the records. (Please note, if an institution record already exists in DEQAR, this data takes precedence over any newly submitted data on the institution. Updates to existing institution records may be made through the EQAR secretariat.)

DEQAR records failing sanity checks may receive either a “low-level flag” or a “high-level flag”. In the first case, records will appear online with submitted data while they await checks and confirmation by the EQAR secretariat. In the second case, records will not be published until they have been checked and confirmed by the EQAR secretariat.

Sanity checks may result in **high-level flags** for the following reasons:

 - **Report Status** is listed as *part of obligatory EQA system* in a country where the Agency does not have official status.
 - Defined **QF-EHEA levels** of an institution and one or more of its programmes do not match.
 
 Sanity checks may result in **low-level flags** for the following reasons:

 - Report is on an institution in a country in which the agency has not previously been active.
 - Validity From date of a report is more than one year before the submission date. (NB: this check is suspended during the uploading of legacy data from each agency.)
 - Country of the Institution does not match the country of one or more of its programmes. 
 - Report on an Institution in the EHEA is submitted without the QF-EHEA levels provided.

Note: any record awaiting harvest or upload of the PDF version of the related report will automatically receive a low-level flag until the report is successfully harvested/uploaded.

