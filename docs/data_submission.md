## Data flow

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

## Validation criteria

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

## Flagging criteria

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
