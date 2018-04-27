Agencies are asked to prepare data on quality assurance reports for submission to DEQAR.  Each agency has the choice to manually submit records one by one through the DEQAR administrative interface or to submit larger batches of data in CSV or JSON format. In the latter cases, the agency must prepare Submission Objects before uploading to DEQAR. A submission object is data related to a single report and is used during ingest to populate report records and to establish linkages inside the system. (Note: a submission object cannot be considered as a report record per se because it may include data stored in other entities as well.) 

Submission objects can be packaged together for batch submission. Though they are used mostly to introduce new report records into DEQAR, submission objects can also be used to update information on existing records through batch submission. Deletion of existing records can only be performed through the administrative interface. 

Below we provide a full list of the data elements that can make up a submission object. It is important to note that the below list is exhaustive, including all possible elements. Required data elements are listed in **bold** with a \* , conditionally required data elements in **bold** with a (\*).  We use the terminology:

 - "must" to denote that an element is required or required in certain situations
 - "should" to denote that an element is highly recommended
 - "may" to denote that an element is optional

### Report Data Elements

**Report Creation:** A single creating agency must be clearly identified for each report. The creating agency is often, though not always, the same as the submitting agency.

- **Agency\*** (<code>agency</code> or <code>agency_id</code>; required; string)  
The agency which created the report must be provided for each report as an agency acronym or as a DEQAR agency ID. This allows the report to be linked to an existing agency record and makes it possible to validate and transform the submitted data in accordance with the agency's profile.   
*e.g. AAQ*
*e.g. 33*

**Report Identification:** A report identifier must be used when submitting updates to an existing report in CSV or JSON. Each report can be identified using an agency's local identifiers or through DEQAR report IDs, which are assigned at upload. It is recommended that agencies submit local report identifiers with every submission object.

- DEQAR Report ID (<code>deqar_id</code>; not required; string)  
Each uploaded report is assigned a unique DEQAR report ID. This may be used to submit updates to existing reports or to promote synchronisation with an agency's local system.  
*e.g. 000786* 

- Local Identifier (<code>local_identifier</code>; not required; string)  
The report identifier used in the agency's local system should be provided for each report. This may be used to submit updates to existing reports or to promote synchronisation with the agency's local system; the local report identifier is particularly useful in the identification of invalid submission objects.  
*e.g. QAA1153-March15*

**Report Activity:** A single activity must be assigned to each report. Activities are selected from the agency's pre-defined list of activities and should be provided as a DEQAR value (as either a string value or a DEQAR activity ID). Optionally an agency may choose to provide local identifiers for its own activities; these should be assigned through the agency record in the administrative interface before they can be used for submission. If both elements are submitted for a single report, then the DEQAR value will be used by the system.  

- **Activity(\*)** (<code>activity</code> or <code>activity_id</code>; conditionally required; string)  
A DEQAR activity value may be provided as an activity name or DEQAR activity ID for each report. The activity is used to validate the structure of submitted report data.  
*e.g. institutional audit, programme evaluation*
*e.g. 2, 8*				
	
- **Activity Local Identifier(\*)** (<code>activity_local_identifier</code>; conditionally required; string)  
A local activity identifier may optionally be provided in place of a DEQAR activity value for each report. The local activity identifier may be used to validate the structure of submitted report data.  
*e.g. inst_aud*  

Each activity is classified as one of four activity types (<code>activity_type</code>). These classifications determine the structure of the report record.  

|Type                   |Report record structure        |               
|:----------------------|:------------------------------| 
|institutional          |at least one institution<br>no programme|
|institutional/programme|one and only one institution<br>at least one programme|
|programme              |one and only one institution<br>at least one programme|
|joint programme        |at least two institutions<br>at least one programme|  

    	
**Report Details:** Each report must be assigned a single status and a single decision value. Together these elements signal the role, status and nature of the report.  Status and decision values may be provided as either string values or DEQAR IDs.  

- **Status\*** (<code>status</code> or <code>status_id</code>; required; string)  
The status must be provided as either a DEQAR status name or a DEQAR status id for each report. The status specifies > > whether the report is part of the obligatory EQA system in the country of the institution or whether the institution has undertaken it voluntarily.  

   |ID |value                         |
   |:--|:-----------------------------|
   |1  |part of obligatory EQA system | 
   |2  |voluntary                     |  
   		
- **Decision\*** (<code>decision</code> or <code>decision_id</code>; required; string)  
The decision must be provided as either a DEQAR decision name or a DEQAR decision id for each report. The decision records the final result of the QA procedure/report.  

   |ID |value                                   |
   |:--|:---------------------------------------|
   |1  |positive                                | 
   |2  |positive with conditions or restrictions|
   |3  |negative                                |
   |4  |not applicable                          |  

**Report Validity:** Each report must have an associated date defining the start of its validity. A date defining the end of the report's validity should also be provided. In the cases that the end date is left open, the report will be treated as valid for six years from the start of its validity, after which it will be archived.  
DEQAR uses a special notation to denote the date format. This allows each agency to signal the date format it uses; this must be provided for each report.
		
- **Valid from\*** (<code>valid_from</code>; required; date)  
A valid from date marking the starting date of the report's validity must be provided for each report. This date is used to generate an archiving date when no valid to date is provided.  
*e.g. 2015-01-15*
		
- Valid to (<code>valid_to</code>; not required; date)  
A valid to date marking the ending date of the report's validity should be provided for each report. This date determines when report data will be archived in DEQAR. If no valid to date is assigned, then the report will be treated as valid for six years after the valid from date.  
*e.g. 2020-01-15*
		
- **Date Format\*** (<code>date_format</code>; required; string)  
A date format  must be provided for each report. Dates may be submitted in any standard format; the format should be represented as a combination of the following characters:  

   |symbol(s)| value                                 |example                      |      
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

**Report Link:** One or more URL links may be provided to alternative views of the report data on the agency's website or other webpage(s) in order to provide more context. A display name may be provided for each URL link. The linked text will display on DEQAR under the display name label provided or, if no name is provided, under generic text provided by DEQAR. 

- Link (<code>link</code>, not required, string)  
One or more URL links may be provided for each report to the same report presented on other sites in order to provide more context to the report.  
*e.g. http://srv.aneca.es/ListadoTitulos/node/1182321350*
		
- Link Display Name (<code>link_display_name</code>, not required, string)  
A display name may optionally be provided for each link to the report on other sites. If no display name is provided, then EQAR will supply generic text.  
*e.g. General information on this programme.*
