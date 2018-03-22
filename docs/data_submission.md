Introduction
============

The following documentation describes the methods available to agencies for the
submission of external quality assurance reports to DEQAR. As was mentioned in
the Data Submission Plan1, we have come up with three different submission
methods to meet the various needs of agencies. The decision to use a particular
method or a combination of methods is highly dependent on the technical
resources available to a particular agency; to provide guidance in this, we have
included a few recommendations for each. All three methods will be fully
interoperable. That is, agencies may switch between different methods at any
time, and data submitted via one method may be updated/altered via another
method.

For the testing period two of the three submission methods will be available:

 - Submission API endpoints
 - CSV upload

The agencies are asked to test the use of these methods to ingest reports into DEQAR.

The web form will be available in mid-March 2018.

> Note: The content of this document reflects the state of the development as of
> the *Last Modified At* date listed in the header. Until the final
> release of DEQAR, the submission guidelines may be extended and/or updated
> with minor changes. Nevertheless, the API endpoints and CSV upload methods may
> already be considered proper specifications to be used as the basis of local
> implementations and testing.

No matter how thorough our internal testing, bugs and errors may still occur. If
you encounter any problem submitting data and/or files, please share these with
us:

 - Either through the [DEQAR Trello
   board](https://trello.com/b/cogOpUeh/deqar-board) under Questions and Answer
   list, where you can add your questions/issue as a new card, or comment on an
   existing card if somebody else already raised the same question.

   Please use one of the predefined labels for new cards: technical CSV,
   technical API, or technical web interface. Please also add to your card the CSV
   file/JSON data that caused the problem, so that the EQAR secretariat and
   developers can reproduce the error.

 - Or by giving feedback in person at the DEQAR workshop on 19/20 March.

In case you are interested contributing to the codebase or you would like to
share your thoughts and ideas, we welcome you to do so through the project's
[GitHub page](https://github.com/EQAR/eqar_backend)

The following sections contain important information on the data format and
essentially apply to all submission methods.

Submission Template
===================

The Submission Template shows which data elements on each report can be
submitted and in which form. While the Submission Template is primarily designed
for creating CSV files for upload, the specifications in it apply also to the
other submission methods accordingly.

It provides an indication of the cardinality (minimum and maximum number of
values required in this field) and conditions for each element as well as a
basic description of the content of each element with an example value.

Please note that the Submission Template must not be read as a list of required
data elements. Instead, it should be read as a set of options from which an
agency can choose, allowing each agency to tailor the submission object to data
currently stored in its local system. Beyond the minimum required elements, the
Submission Template also includes several non-required elements which may be
stored and displayed by DEQAR but which are not necessary for the creation of a
basic record. In several cases, the Submission Template also presents options
for submitting the same information in various forms.

The template is divided into three main areas: the main (or “report”)
area; the institution area; and the programme area. Both the institution and
programme areas may be repeated in the case of a report treating multiple
institutions and/or programmes. This is indicated by the formulation
“institution[n]” and “programme[n]”.

The columns in the Submission Template can be understood as follows:

 - Record Area: clusters of data elements that are grouped according to content
   type; this indicates groups of elements that function together or serve the
   same role.
 - Field Name: the 39 separate data elements that may be submitted to DEQAR.
 - Data Format: the base format in which the data for a particular element can
   be delivered--string, text, date, float. In some cases, the string type
   includes a character length indicator as well--e.g. “string (255char)”
   means a string value of maximum 255 characters. For the DEQAR Submission
   Template, identifiers, even those stored in integer form, are accepted as string
   values.
 - Cardinality: the minimum and maximum number of values that may be submitted
   for a particular element OR the minimum and maximum number of groups of
   values that may be submitted for a cluster of elements. The cardinality of any
   element or cluster can extend from .... (i.e. multiple) values. 

   Key to Cardinality:

   0, 1 = not obligatory, and maximum one value may be entered
   1, 1 = one and only one value must be entered
   0, * = not obligatory and multiple values may be entered
   1, * = one value must be entered but multiple values possible.
 - Condition: a description in text form of the cardinality and dependencies of
   a single element or cluster of elements. A particular terminology is used to
   signal DEQAR requirements and recommendations.
   We use:
	- **Must** to signal that the element or cluster of elements has to be there; otherwise the record will be rejected.
        - **Should** to signal that we highly recommend that the element or cluster of elements be provided, unless providing it would cause undue effort.
        - **May** to signal that the element or cluster of elements can be provided if applicable and/or if the agency feels it might be useful.
 - Note: a description of the data required and in some cases also its use in
   later processes.
 - Sample Data: one or more sample values. In the case that a fixed set of
   values is provided by DEQAR, then all values and related IDs are listed.

The Submission Template is accompanied by a second sheet with six sample
submission objects in CSV (in this case as an .xlsx file). The six samples show
data on the four different report types: Institutional, Programme,
Institutional/Programme and Joint Programme.

Take particular note of the treatment of multiple institutions and programmes
and also of multi-value elements, e.g. QF-EHEA levels. Also note that in the
case that a data set is submitted as an .xls sheet, each different element must
be represented as a column, even if the element is only used for a single record
in the set. This is demonstrated in the sample data.

Submission Template (Google Sheets, download possible in Excel, OpenDocument or
PDF format)

Reference Values
================

On the DEQAR Values spreadsheets you can find important reference values:

 1. Higher education institutions with DEQAR IDs and ETER IDs
 2. Registered agencies with acronyms and DEQAR IDs
 3. List of ESG Activities with IDs

If information regarding your agency requires correction, please contact the
EQAR Secretariat. In the future, you will be able to access this information and
ask for modifications through the admin web interface.

DEQAR Values (Google Sheets)

Data Flow
=========

In general, irrespective of the submission method, all data inserted into DEQAR
is handled following these steps:

 1. The Submission Request Object (submitted through the API or a CSV upload) goes through the first level of validation;
 2. If the data format is invalid or the submitted identifiers can’t be resolved (see detailed Validation Criteria below), the record is rejected;
 3. Valid report data is populated in the appropriate tables;
 4. Sanity checks are run against pre-defined flagging criteria (see detailed Flagging Criteria below), reports which contain conflicts are flagged;
 5. A Response Object (or array of objects) is sent back to the agency, containing:
	- detailed error descriptions for reports that were rejected;
	- identifiers of records that were created or identified (in the case of Institutions);
	- identifiers of newly created records (Reports, Report Files);
	- information on records where sanity checks found errors. 

Validation criteria
===================

In order for records making up a Submission Request Object to clear the first
level of validation, they must meet the following criteria:

  1. The agency that created the report (which may or may not be the agency submitting the records) must be clearly identified. The agency may be identified using an agreed upon acronym or a DEQAR agency ID which has been provided by the EQAR secretariat.
  2. All required data must be present for each report. Required data for all records includes:
	1. ESG activity performed: provided as activity name, ID given by EQAR or as a local identifier. (see reference values)		
	2. Status of report: “part of obligatory EQA system” (1) or “voluntary” (2). This can be provided as text or as an ID.	
	3. Decision: “positive” (1), “positive with conditions or restrictions” (2), “negative” (3) or “not applicable” (4). This can be provided as text or as an ID.
	4. Report valid from date: This must be provided as a full date, but can be provided in any common day-month-year format. The date format used by the agency must also be included with the data.
	5. Language(s) of the report: At least one language for each report should be provided as a two- or three-digit ISO 639 code. Ideally language information is provided along with the link to the location of the PDF file. 
	6. Institution Data:
		1. Either DEQAR ID: the identifier under which the Institution is listed in DEQAR. This will be provided to the agency as part of the Response Object for each submission.
		1. or ETER ID: the identifier under which the Institution is listed in ETER. This will also be included as part of the Response Object for each submission.
		1. or Agency Local Identifier: the identifier under which the Institution is listed in the agency’s local system. This can only be used if the identifier has already been provided to DEQAR as part of a previous submission.
		1. or minimum Institution record elements:
			- Official Name of Institution (in original language),
			- Country of Location for the Institution (as ISO 3166-1 alpha-2 or alpha-3 country code) 
			- Website Link for the Institution.
	7. Additional data required for reports on programmes:
		1. Programme Name: in whatever language it is stored by the Agency.
 3. At this point, dependencies between elements will be checked as well as any limits on the cardinality of each element. More information can be found in the Submission Template.
 4. Submitted data must be of the correct type, form and value range/options. More information can be found in the Submission Template.
 5. Submitted data must align with Agency Profile information, specifically report validation date should fall after Agency EQAR registration dates and activities should match defined ESG activities for the Agency.
 6. Submitted data must meet basic data integrity rules for the system, i.e. there should be one and only one creating agency and at least one institution covered by each report.
 7. Submitted report data must meet the structural requirements determined by the listed ESG activity. Each report will be categorised as activity type Institutional, Programme, Institutional/Programme or Joint Programme, and the record structure must reflect this typology. In other words:
	- Report records with Activity Type “Institutional”: 
		- contain required institution data on at least one institution
		- contain no programme data
	- Report records with Activity Type “Programme” or “Institutional/Programme”:
		- contain data on one and only one institution 
		- contain data on at least one programme
	- Report records with Activity Type “Joint Programme”:
		- contain data on more than one institution 
		- contain data on at least one programme

Records not meeting all of the above criteria will be rejected. The system will
return a Response Object that clearly identifies rejected records, including
information on the source of the problem. Importantly, the rejection of one or
more records does not imply the failure of the whole Submission Request Object.

Flagging criteria
=================

Once the records making up the Submission Request Object clear the first level
of validation, they are officially ingested into the system. DEQAR records are
populated with valid data and final sanity checks are run on the records.
(Please note, if an institution record already exists in DEQAR, this data takes
precedence over any newly submitted data on the institution. Updates to existing
institution records can be made through the EQAR secretariat.)

DEQAR records failing sanity checks may receive either a “low-level
flag” or a “high-level flag”. In the first case, records will appear
online with submitted data while they await checks and confirmation by the EQAR
secretariat. In the second case, records will not be published until they have
been checked and confirmed by the EQAR secretariat.

Sanity checks may result in high-level flags for the following reasons:

 - Report Status 	is listed as “part of obligatory EQA system” in a country where the Agency does not have official status.
 - Defined QF-EHEA levels of an institution and one or more of its programmes do not match.

Sanity checks may result in low-level flags for the following reasons:

 - Report is on an institution in a country in which the agency has not previously been active.
 - Validity From date of a report is more than one year before the submission date. (This will be suspended during the uploading of legacy data from each agency.)
 - Country of the Institution does not match the country of one or more of its programmes. 
 - Report on an Institution in the EHEA is submitted without the QF-EHEA levels provided.

Note: any record awaiting harvest or upload of the PDF version of the related
report will automatically receive a low-level flag until the report is
successfully harvested/uploaded.

