# Report Submission

Each agency should follow three steps to submit their report data:

1. Choose a particular [submission method](#choosing-a-submission-method).
2. Prepare your data with guidance on the [Report Data Elements](report_data.md) above.
3. Submit data using your chosen submission method and review the response after your data has passed through validation and flagging as described in [Data Pipeline](#data-pipeline) below.

## Choosing a Submission Method

Considering the various needs of the agencies, DEQAR supports three different submission methods. Their use is highly dependent on the technical resources available to a particular agency. Important: all three methods are fully interoperable. That is, agencies may switch between different methods at any time, and data submitted via one method may be updated/altered via another method.

[**Webform**](#webform): Those agencies needing a simple means of submitting report data to DEQAR can enter data directly in the webform present in the administrative interface. This method is fully manual; agencies can simply login and create new report records or modify existing ones. Flags and validation errors will be returned immediately upon submission. Data already submitted using CSV or JSON/API will also be accessible through the administrative interface.

We recommend this method for agencies:

* without IT developers;
* with a closed system architecture from which data export is not straightforward;
* who would like to submit small amounts of data occasionally;
* who would like to interact with their DEQAR data directly.

[**CSV Upload**](#csv-upload): In order to submit batches of documents, agencies may prefer to work with well-established formats like Excel. [Comma Separated Values (CSV)](https://en.wikipedia.org/wiki/Comma-separated_values) is a flat file format which can be produced and presented directly through Excel, LibreOffce and many other software packages. This termed a semi-automatic data submission method. DEQAR has provided a CSV template which can be complemented with the detailed explanation of the [Report Data Elements](report_data.md) above.

Using CSV, transformation of data can be done manually by administrative staff without the help of IT. Staff can then login to the administrative interface and upload the CSV file for import. When uploading, records (i.e. single lines of the file) are validated and information on the status of each record in the uploaded batch are shown on the import interface. Agency staff can then decide to fix failed records ad-hoc or re-upload them later.

We recommend this method for agencies:

* without IT developers;
* with a local system from which they can export data in tables;
* who would like to submit bigger amounts of data in a batch;
* who would like to work manually on their data before submitting to DEQAR.

[**Submission API**](#submission-api): [REST API](https://en.wikipedia.org/wiki/Representational_state_transfer) is a convenient way for software developers to communicate via HTTP, the protocol used by the internet. When used together with the [JSON format](https://www.json.org/) it provides flexible means of exchanging data between systems. With the possibility of sending complex request and response objects, DEQAR can accept structured data and give immediate feedbacks (error checks, warnings) about the submitted data as well as metadata enhancements.

We recommend this method for agencies:

* with IT developers / IT vendors who can develop a method (script/web application) to post data to the API endpoint;
* who would like to submit large amounts of data at once with a single call;
* who would like to submit individual reports immediately upon their creation;
* who would like to keep DEQAR and their local system in sync;
* who plan to submit data periodically and at longer intervals (e.g. weekly or monthly).

## Data Pipeline

In general, irrespective of the submission method, all report data submitted to DEQAR is handled following these steps:

1. The first level of validation concerns the data format, including that all required fields are present and all identifiers used are valid. If the record does not pass the requirements and constraints described in [Validation Criteria](#validation-criteria) below, the record is rejected.
2. Valid report data is saved in the database.
3. Sanity checks are run against pre-defined [Flagging Criteria](#flagging-criteria); reports which meet any of these criteria are flagged. Flagged reports are nevertheless saved in the database and should not be re-submitted.
4. A Response Object (or array of objects) is sent back to the agency, containing:
    * detailed error descriptions for report objects that were rejected;
    * identifiers of report records that were created or identified;
    * information on records where sanity checks found issues.

### Validation criteria

In order for submission objects to clear the first level of validation, they must meet the following criteria:

1. The main **agency** that created the report (which may or may not be the agency submitting the records) must be clearly identified and, if your user is not linked to the agency itself, you must have a proxy to submit reports for the agency.

    Additional, contributing agencies [can be identified](report_data.md#agency), but all validation and flagging criteria relate to the main agency only.

2. Submitted data must **align with the Agency Profile** information, specifically report validity date must be after the Agency's EQAR registration start date and before the registration end date, if applicable.

3. All **required data** must be present for each report. Required data for all records includes:
    * [ESG activity/-ies performed](report_data.md#activity), at least one for each agency involved
    * [Status of report](report_data.md#details)
    * [Decision](report_data.md#details)
    * Report [valid from date, including date format](report_data.md#validity) used by the agency
    * At least one [report file](report_data.md#files) including the language(s) in which it is drafted
    * Organisation: a report must relate to at least one [existing organisation record](report_data.md#organisations) identified by a DEQARINST ID, ETER ID or another known identifier.

3. At this point, **dependencies** between elements will be checked as well as any **limits on the number of values permitted** for each element. In particular:
    * Requirements based on the **type of [ESG activity](report_data.md#activity)**:
        - only institutional activities: no programme data must be provided
        - at least one programme or programme/institution activity: exactly one organisation must be identified, data on one or several programme(s) must be provided
        - at least one joint programme activity: at least two organisations must be identified, data on one or several programme(s) must be provided
    * Data required for **each programme** (i.e. except purely institutional reports):
        - the [programme name](report_data.md#programme-name-and-qualification) (in whichever language it is stored by the Agency)
        - the [degree outcome](report_data.md#programme-qualification-level) indicating whether full degree or not
        - the [qualification level](report_data.md#programme-qualification-level)
    * Data required for **programmes with degree outcome "no"** (= not leading to a full degree):
        - [Workload expressed in ECTS](report_data.md#programme-details)
        - Whether programme includes [assessment or certification](report_data.md#programme-details)
    * Constraints for **reports not covering any higher education institution from the EHEA**, e.g. report on a non-European higher education institution or other provider:
        - [Status](report_data.md##report-details) must be "voluntary"
    * Constraints for **reports on only other providers**, i.e. when none of the organisations identified is a higher education institution:
        - [Degree outcome](report_data.md#programme-qualification-level) must be "no" (= not leading to a full recognised degree)

4. Submitted data must be of the **correct type, form and value range/options** as described above.

Records not meeting all of the above criteria will be rejected and no data on the report will be saved. The system will return a response object that clearly identifies rejected records, including information on the source of the problem. Importantly, the rejection of one or more submission objects does not imply the failure of the whole submission batch.

### Flagging criteria

Once the report data passed the first level of validation, DEQAR report records are created or updated with the submitted data. Now, some final sanity checks are run on the records: records may receive a “low-level flag” or a “high-level flag”.

In the first case, records will appear online with submitted data, while the EQAR Secretariat is informed to take note. In the second case, records will not be published until they have been checked and confirmed by the EQAR Secretariat.

> The purpose of a flag is to bring a report to the EQAR Secretariat's attention. A flag normally does **not** indicate that data should be changed. Therefore, provided that the data you entered/uploaded is correct, please do **not** try to change the data of a report in order to prevent it from being flagged, but simply wait for EQAR Secretariat to have checked the report.

Sanity checks may result in **high-level flags** for the following reason:

* Report Status is listed as *part of obligatory EQA system* and the Agency does not have official status (according to EQAR's information) in any legal seat country of any higher education covered by the report.

    > For reports on both higher education institutions and other providers, the agency must have official status in one of the higher education institutions' countries, the status in the other providers' countries is not relevant to this check.

Sanity checks may result in **low-level flags** for the following reasons:

* The report covers a provider with a legal seat in or a programme delivered in a country in which the agency has not previously been active.
* Country of the programme (if specified) does not match any location country of any provider covered.
* Programme-level report is "voluntary" and the programme's qualification level is not contained in the list of qualification levels of any of the higher education institutions specified
* One or more PDF files of the report could not be downloaded (in case a URL was specified) or was not yet uploaded (using the specific API endpoint)

In addition, the following data on agencies or institutions will automatically be complemented at flagging stage:

* If the report covers a provider with a legal seat in or a programme delivered in a country in which the agency has not previously been active, this **country is added to the agency's profile**.
* The **programme qualification level** is added to a higher education institution's qualification levels if the report is "part of the obligatory EQA system".
* The programme qualification level is always added to an other provider's qualification levels.

## Webform

The DEQAR administrative interface includes an interactive webform, allowing you to submit single reports. The administrative interface is available at:

location: <{{ deqar.admin }}/>  
username: [agency's acronym (in lower case)]  
password: [your personal password]

If you do not remember your password or did not change the default password, please go to <{{ deqar.admin }}/forgot-password> in order to reset your password. You need to enter your email address and will receive by email a special link that allows you to set a new password.

The email address linked to your login is the same email address to which submission report emails are sent. If you do not remember which email address is linked to your agency's login, please contact the EQAR Secretariat.

The webform can be found in the menu under *Submit Report* > *[Report Form]({{ deqar.admin }}/submit-report)*.

Required fields are marked with a <span style="color: #f00;">\*</span> in the form; fields marked with a <span style="color: #f00;">(\*)</span> are conditionally required. Please note that the [Activity](#report-activity) chosen might influence which information is required (see [Report Data Elements](report_data.md) above). The *Save Record* button becomes active once all required information has been provided.

We strongly recommend that you provide a [Local Report Identifier](#report-identification) that identifies the specific report in your own information system or workflow, even when you use the webform. This will facilitate later updates should they be necessary, and can be useful if your agency changes to CSV upload or the Submission API later on.

You can select institutions using the search box. If you are uploading a report on an institution that has no DEQAR record yet, see [Institution Data](institution_data.md) on how to add it before uploading reports.

Data on programmes will only be needed if your report results from a programme-level activity. Fill the form with the required information and then click the *Add Programme* button. If the report concerns several programmes (e.g. clustered evaluation) please repeat the step for all programmes concerned. (See [Programme Data Elements](#programme-data-elements) above.)

Each report may contain one or more report files (for example, the experts' report, a possible summary report and the decision taken might be contained all in one or in separate files). The report file fields are conditionally required. At least one must be present, but agencies can either provide a URL or upload a file directly (in either case, only PDF files are accepted). For each file, please specify the language(s) of its contents. The display name is optional; the text "Report" will be used as a default otherwise. (See [QA Report Files](#qa-report-files) above.)

## CSV Upload

[Comma-separated values (CSV)](https://en.wikipedia.org/wiki/Comma-separated_values) is a common and interoperable data-exchange format. Files can be imported and exported from all usual [spreadsheet software](#preparingexporting-csv-files) (e.g. Excel, LibreOffice, ...) and numerous other applications.

The first row of your file is a header which should include column names as defined under [Report Data Elements](report_data.md) above. The following lines contain one report per row. A simple example of a CSV first-fow header for institution-level reports could look as follows:

```
agency, activities[1].activity, status, decision, valid_from, valid_to, date_format, file[1].original_location, file[1].report_language[1], institution[1].eter_id
```

(Spaces added for readability, these should not appear in an actual file.)

One report may often include/relate to several items, such as one or more provider(s), programmes or one or more files--some in several languages. In those cases you will find field names of the type `field_name[n]` (See [Report Data Elements](report_data.md) above). You should create as many columns as you need and replace `n` by 1, 2, ...

For example, two files (e.g. full report in local language, and summary in both English and local language) can be provided as follows:

```
..., file[1].original_location,   file[1].display_name, file[1].report_language[1], file[2].original_location,   file[2].display_name, file[2].report_language[1], file[2].report_language[2], ...
..., "http://some.url/to/report", "Expert report",      "de",                       "http://some.url/to/report", "Summary",            "en",                       "de", ...
```

(Spaces added for readability, these should not appear in an actual file.)

You can use one of the sample CSV files below as a starting point and adjust it to your needs. Please bear in mind the following:

* The template file is provided in Microsoft Excel and Open Document Formats, as well as viewable on-line. **It needs to be saved in CSV format for upload to DEQAR** (see notes below).
* The first worksheet includes *all* possible column names you could use in a CSV file, with the respective requirement/validation notes as comments. These comments will disappear as you save the file in CSV format.
* The subsequent worksheets include more condensed examples with sample data, including those columns that will typically be used in reports concerning institutions, programmes or joint programmes.
* You need to include all columns you might need in at least one of your reports, but they can stay empty in those lines where they are not applicable.
* You may omit columns from the sample CSV file that are not used in any of the reports.
* CSV files should be saved in UTF-8 encoding.

### Template and samples

* [Microsoft Excel format](files/SubmissionTemplate.xlsx)
* [Open Document Format (OpenOffice/LibreOffice/NeoOffice)](files/SubmissionTemplate.ods)

### Preparing/exporting CSV files

Despite being software-independent, there are some known issues when creating/exporting CSV files from some major office applications. Given that it has the most clean and straight-forward CSV export, we recommend the [LibreOffice package](https://www.libreoffice.org/), a free and open-source desktop application supported on all major operating systems.

For all software packages, please note that the CSV format does not support multiple sheets, but it will always be only the current work sheet that is saved in CSV format.

#### Microsoft Excel

Despite offering CSV as a target file type in its *Save as* dialogue, Microsoft Excel does not create correct CSV files when certain character sets are used (e.g. Greek or Cyrillic alphabets, or certain Roman characters with diacritics). You can use the following work-around:

* Select *Save as* from the *File* menu, select your desired folder and choose *Unicode Text (\*.txt)* as type.<br /> ![Excel save as dialogue](img/csv-excel-fix-0.png)
* Simply press *OK* in response to the following error message:<br /> ![The selected file type does not support workbooks that contain multiple sheets](img/csv-excel-fix-1.png)
* Furthermore, confirm with *Yes* also the following warning message:<br /> ![Some features in your workbook might be lost if you save it as Unicode Text](img/csv-excel-fix-2.png)
* Close Microsoft Excel and navigate to the folder containing your file in the file manager. Right-click on your file and choose *Rename*.
* Now change the file extension from `.txt` into `.csv`. You will encounter the following message: *If you change file name extension, the file may become unusable. You still want to change them, you should press ‘Yes’...* Confirm the warning by clicking Yes.
* This CSV file is now suitable for upload.

#### LibreOffice/OpenOffice/NeoOffice

Exporting CSV files is straight-forward in LibreOffice, OpenOffice and NeoOffice:

* Choose *Text CSV (\*.csv)* as file type in the *Save As ...* or *Save a Copy ...* dialogue:<br /> ![LibreOffice save file dialogue](img/csv-libreoffice-0.png)
* Ensure the export settings are set as follows in the next dialogue. Please pay particular attention character set and delimiters:<br /> ![CSV export settings](img/csv-libreoffice-1.png)
* The CSV file is now suitable for upload.

#### Google Sheets

In Google Sheets, choose *Comma-separated values* from the *File* > *Download as...* menu.

### Uploading CSV files

The CSV upload module is part of the DEQAR admin interface:

location: <{{ deqar.admin }}/upload-csv>  
username: [agency's acronym (in lower case)]  
password: [your personal password] (see [above](#webform) how to reset your password)

* Select *Submit Report* > *Upload CSV* from the menu.
* Choose your file under *Select CSV file* and click *Upload*.
* You can now review your data one more time under *Uploaded CSV Data*, and make changes if necessary.
* Afterwards, click on *Ingest* under the table. The uploaded CSV file now passes the same [validation](#validation-criteria) pipeline as information submitted through any other method.
* After ingest, you will see all rows highlighted in green if they were successfully saved, or in red if they could not be ingested due to validation errors. Click on a row to see details about the errors.
* If you experienced errors, you can correct the respective lines and click on *Ingest* again.
* Please note that the green rows will be re-ingested, but overwrite the existing report based on the DEQAR Report ID. Any changes you make to green rows will therefore be recorded on a further ingest, too.

## Submission API

REST API is a convenient way for software developers to communicate with web services via HTTP, the protocol used by the internet. Together with JSON it provides an easy, straightforward and flexible means of exchanging data between systems. With the possibility of sending complex request and response objects, we can accept structured data and give immediate feedbacks (e.g. error checks, warnings) about the submitted data as well as metadata enhancements (e.g. ETER IDs on HEIs, when applicable; links to new records on the EQAR public interface, etc.).

### Authentication

Requests for submission to DEQAR are only accepted from registered users and must therefore be identified. DEQAR API endpoints manage authentication using API Tokens (through the so-called Bearer Authentication method). Upon registration, an API Token (which is basically a hash) is created for each user. Sending this token in the Authorization header (with type/scheme Bearer) will authenticate the user in place of a regular username and password.

To get your authentication token you can send a `POST` request to the following URL:

`{{ deqar.root }}/accounts/get_token/`

An example of obtaining a token using curl in command line:

```sh
curl -s -H "Content-Type: application/json" -XPOST {{ deqar.root }}/accounts/get_token/ --data '{"username":"testuser","password":"testpassword"}'
```

The username is the agency’s acronym (in lower case). Please see [above](#webform) how to reset your password.

Or for those who prefer to use the more user friendly [HTTPie](https://httpie.io/) client:

```sh
http POST {{ deqar.root }}/accounts/get_token/ 'username=testuser' 'password=testpassword'
```

You should send this token, preceded by the word `Bearer`, in the Authorization header with every further request. An example of a submission using curl or HTTPie:

```sh
curl -s -H "Content-type: application/json" -H "Authorization: Bearer $DEQAR_TOKEN" -XPOST {{ deqar.root }}/submissionapi/v2/submit/report --data-binary @$DEQAR_FILE

http -v POST {{ deqar.root }}/submissionapi/v2/submit/report "Authorization: Bearer $DEQAR_TOKEN" "Content-type: application/json" < $DEQAR_FILE
```

### Endpoints

The Submission API offers the following endpoints to manage the whole lifecycle of reports:

| Method | Path                                                       | Function                                                                      |
| ------ | ---------------------------------------------------------- | ------------------------------------------------------------------------------|
| POST   | `{{ deqar.root }}/submissionapi/v2/submit/report`          | Submit a new report that is not yet recorded in DEQAR                         |
| PUT    | `{{ deqar.root }}/submissionapi/v2/submit/report`          | Update data on an existing report in DEQAR                                    |
| GET    | `{{ deqar.root }}/submissionapi/v2/check/local-identifier` | Check for the existance of a local identifier                                 |
| POST   | `{{ deqar.root }}/submissionapi/v2/manage/report-file`     | Upload an additional file to an existing report                               |
| PUT    | `{{ deqar.root }}/submissionapi/v2/manage/report-file`     | Replace a file belonging to a report                                          |
| DELETE | `{{ deqar.root }}/submissionapi/v2/manage/report-file`     | Remove a file from a report                                                   |
| DELETE | `{{ deqar.root }}/submissionapi/v2/delete/report/{id}/`    | Request deletion of a report from DEQAR (exceptional cases only)              |

The semantic of the various fields and accepted types are described in [Report Data Elements](report_data.md) above. The technical description of request and response objects can be find in OpenAPI format under:

<{{ deqar.root }}/submissionapi/v2/swagger/>

### Report Lifecycle

Please note that version 2 of the Submission API requires you distinguish clearly between the upload/creation of a new report (`POST`) or the update of an existing one (using `PUT` or `PATCH`). For example, a `POST` request with an existing local identifier will be rejected.

We strongly recommend that you (a) submit a unique code or identifier of a report in your own system as `local_identifier` and (b) track in your system whether a report was already succssfully submitted to DEQAR. To that end, the response of the report creation endpoints includes the new DEQAR ID of the report; you can use that in subsequent `PUT` or `PATCH` requests.

If you cannot track submission status in your system, you might need to make an additional request to the `/check/local-identifier` endpoint first in order to determine whether this report was already submitted to DEQAR earlier.

In general, reports should never be deleted from DEQAR, as the system intends to keep a full historic record. The `DELETE` endpoint is therefore for exceptional circumstances only, e.g. to fix accidental duplications. It can only mark reports for deletion and deletion has to be then confirmed by EQAR staff case by case. You also need to provide a reason for every deletion request. This also means: deletion of reports should never be part of your regular, every-day workflow.

### Report Files

Each report needs to have at least one file (PDF versions of reports). These can be submitted in two separate ways:

* URL reference: these files will be harvested asynchronously upon successful submission.
* Directly: files can be Base64-encoded and submitted directly in requests

Files can be managed as follows, each allowing either option:

* At least one file needs to be submitted whenever creating a report. You can specify a URL or include the Base64-encoded file in your request.
* When updating reports via `PUT`, all files need to be submitted again.
* When updating reports via `PATCH`, ... **to be defined**
* You can use the dedicated report file endpoints to add, update or delete individual files without touching the report record otherwise. Please note that you cannot delete the last file of a report as each report needs to have at least one file attached.

Files submitted by URL reference are downloaded asynchronously after submission. DEQAR makes a `HEAD` request first, followed by a `GET` request. At least the latter needs to return a content-type header of `application/pdf`. If another content type is reported the download will fill. The maximum file size for download is 100MB.

When the download fails, the corresponding report record receives a low-level flag for information.

Downloads are only retried if the report or the specific files are updated through the mentioned endpoints (or via CSV or admin interface). Existing report files are only uploaded/replaced if the new download succeeded and the downloaded file differs from the existing one. Otherwise the existing file is kept.

DEQAR only accepts PDF files. Each file – whether downloaded from a URL or submitted directly – will be opened with the [pypdf](https://pypi.org/project/pypdf/) library (version 4.2.0). Files not readable by the library are rejected.

### Examples

The examples below show how a JSON Submission Request Object might look for different types of reports:

#### Institutional report

```json
{
  "agency": "MusiQuE",
  "local_identifier": "CRDB-October14",
  "activities": [
    {
      "id": "183"
    }
  ],
  "status": "part of obligatory EQA system",
  "decision": "positive",
  "valid_from": "2016-10-28",
  "valid_to": "2018-01-15",
  "date_format": "%Y-%m-%d",
  "report_files": [
    {
      "original_location": "http://www.musique-qe.eu/userfiles/File/2014-10-bruxelles-website.pdf",
      "display_name": "Evaluation report",
      "report_language": [
        "fr"
      ]
    }
  ],
  "institutions": [
    {
      "eter_id": "BE0035"
    }
  ]
}
```

#### Another institutional report with two agencies

```json
{
  "agency": "MusiQuE",
  "contributing_agencies": [
    "AAQ"
  ],
  "local_identifier": "ENH-4711",
  "activities": [
    {
      "id": "97"
    },
    {
      "local_identifier": "DE-SYS-2018",
      "agency": "AAQ"
    }
  ],
  "status": "2",
  "decision": "4",
  "valid_from": "2021-01-15",
  "date_format": "%Y-%m-%d",
  "report_files": [
    {
      "original_location": "http://www.musique-qe.eu/userfiles/File/2015-06-25-hamu-review-reportfinal.pdf",
      "display_name": "Institutional Review",
      "report_language": [
        "eng"
      ]
    },
    {
      "original_location": "https://zenodo.org/record/4516653/files/Database_of_External_QA_Results_Report%2BModel_2016.pdf?download=1",
      "display_name": "Addendum to the report",
      "report_language": [
        "ger"
      ]
    },
    {
      "file": "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",
      "file_name": "3rd-report.pdf",
      "display_name": "Further addendum",
      "report_language": [
        "eng"
      ]
    }
  ],
  "institutions": [
    {
      "deqar_id": "DEQARINST0390"
    },
    {
      "eter_id": "AT0006"
    }
  ]
}
```

#### Programme report

```json
{
  "agency": "MusiQuE",
  "local_identifier": "SHM-April09",
  "activities": [
    {
      "id": "181"
    }
  ],
  "status": "2",
  "decision": "1",
  "valid_from": "2017-04-09",
  "valid_to": "2022-02-15",
  "date_format": "%Y-%m-%d",
  "report_files": [
    {
      "original_location": "http://www.musique-qe.eu/userfiles/File/2009-06-report-trossingen-website.pdf",
      "display_name": "Review report",
      "report_language": [
        "ger"
      ]
    }
  ],
  "institutions": [
    {
      "eter_id": "DE0140"
    }
  ],
  "programmes": [
    {
      "identifiers": [
        {
          "identifier": "16"
        }
      ],
      "name_primary": "Organ Expert",
      "qualification_primary": "Master of Arts",
      "nqf_level": "level 7",
      "degree_outcome": "1",
      "qf_ehea_level": "second cycle"
    }
  ]
}
```

#### Joint Programme report with additional label awarded by contributing agency

```json
{
  "agency": "MusiQuE",
  "contributing_agencies": [
    "ASIIN"
  ],
  "local_identifier": "EAMT-September13",
  "activities": [
    {
      "id": "182"
    },
    {
      "group": 5
    }
  ],
  "status": "voluntary",
  "decision": "positive",
  "valid_from": "15.01.2020",
  "valid_to": "15.01.2025",
  "date_format": "%d.%m.%Y",
  "report_files": [
    {
      "original_location": "http://www.musique-qe.eu/userfiles/File/final-reportaec-programme-reviewcopeco.pdf",
      "display_name": "Review report",
      "report_language": [
        "eng"
      ]
    }
  ],
  "institutions": [
    {
      "eter_id": "EE0022"
    },
    {
      "eter_id": "SE0037"
    },
    {
      "identifier": "F  LYON24",
      "resource": "Erasmus"
    },
    {
      "deqar_id": "DEQARINST0460"
    }
  ],
  "programmes": [
    {
      "identifiers": [
        {
          "identifier": "18"
        }
      ],
      "name_primary": "CoPeCo – Contemporary Performance and Composition",
      "qualification_primary": "Master (no joint degree)",
      "nqf_level": "level 6",
      "degree_outcome": "1",
      "qf_ehea_level": "second cycle"
    }
  ]
}
```

#### Micro-credential provided by a higher education institution on a platform

```json
{
  "agency": "AAQ",
  "local_identifier": "230830/4711/01",
  "activities": [
    {
      "id": "386"
    }
  ],
  "status": "part of obligatory EQA system",
  "decision": "positive",
  "valid_from": "2022-11-11",
  "valid_to": "2033-03-03",
  "date_format": "%Y-%m-%d",
  "institutions": [
    {
      "deqar_id": "DEQARINST0006"
    }
  ],
  "platforms": [
    {
      "deqar_id": "DEQARINST8785"
    }
  ],
  "report_files": [
    {
      "display_name": "report",
      "original_location": "https://www.eqar.eu/assets/uploads/2021/06/RC_10_1_ComplaintsPolicy_v3_0.pdf",
      "report_language": [
        "EN"
      ]
    }
  ],
  "programmes": [
    {
      "name_primary": "Micro master in IT",
      "qf_ehea_level": "2",
      "degree_outcome": "no",
      "workload_ects": "25",
      "assessment_certification": "1",
      "field_study": "0288",
      "learning_outcomes": [
        "http://data.europa.eu/esco/skill/7c4fc5e4-10cc-4457-9038-77907fee1290",
        "http://data.europa.eu/esco/skill/390bd026-943b-44a5-b871-def0248e26b8",
        "http://data.europa.eu/esco/skill/57231a22-4da7-49c8-97b8-75672feadf1e"
      ]
    }
  ],
  "summary": "We evaluated this micro-credential positively."
}
```

#### Audit of an other provider

```json
{
  "agency": "AAQ",
  "local_identifier": "240117/4711/009",
  "activities": [
    {
      "id": "231"
    }
  ],
  "status": "voluntary",
  "decision": "2",
  "valid_from": "2022-11-11",
  "valid_to": "2033-03-03",
  "date_format": "%Y-%m-%d",
  "institutions": [
    {
      "deqar_id": "DEQARINST7773"
    }
  ],
  "report_files": [
    {
      "display_name": "report",
      "original_location": "https://www.eqar.eu/assets/uploads/2021/06/RC_10_1_ComplaintsPolicy_v3_0.pdf",
      "report_language": [
        "EN"
      ]
    }
  ],
  "summary": "Experts were very satisfied with the academy's internal QA system."
}
```

#### Accreditation of a micro-credential provided by an other provider

```json
{
  "agency": "AAQ",
  "local_identifier": "230830/4711/02",
  "activities": [
    {
      "id": "386"
    }
  ],
  "status": "voluntary",
  "decision": "positive",
  "valid_from": "2022-11-11",
  "valid_to": "2033-03-03",
  "date_format": "%Y-%m-%d",
  "institutions": [
    {
      "deqar_id": "DEQARINST7773"
    }
  ],
  "report_files": [
    {
      "display_name": "report",
      "original_location": "https://www.eqar.eu/assets/uploads/2021/06/RC_10_1_ComplaintsPolicy_v3_0.pdf",
      "report_language": [
        "EN"
      ]
    }
  ],
  "programmes": [
    {
      "name_primary": "Using Pandas and Python for survey analysis",
      "qf_ehea_level": "2",
      "degree_outcome": "2",
      "workload_ects": "5",
      "assessment_certification": "1",
      "field_study": "0288",
      "learning_outcomes": [
        "http://data.europa.eu/esco/skill/7c4fc5e4-10cc-4457-9038-77907fee1290",
        "http://data.europa.eu/esco/skill/390bd026-943b-44a5-b871-def0248e26b8",
        "http://data.europa.eu/esco/skill/57231a22-4da7-49c8-97b8-75672feadf1e"
      ]
    }
  ],
  "summary": "This micro-credential offers valuable skills to students. It is offered by a company."
}
```

## Updating Reports

Normally, once a QA report has been published it will not change. Changing or updating reports in DEQAR should therefore be the exception, rather than regular practice.

Reports can, however, be changed if needed as follows:

 1. **Manually via admin interface**

    Please find the report that you want to change in the admin interface, under under Reference data > Reports. To narrow down the search, use filters and search by report number, name, year, agency, country, activity type and flag. Once you find the report, open the record and click on Edit Report. When submitting, please leave a short note to explain the changes you made.

 2. **Submission API or CSV Upload**

    Please use the same method/template as for initially uploading reports.

    Use either the DEQAR Report ID (`report_id`) or the same [Local Report Identifier](report_data.md#report-identifier) (`local_identifier`) that you provided to DEQAR with your earlier/initial upload of the report. Lacking an ID prevents the system from recognising the report that needs to be updated, and will lead to creation of new (duplicate) record in the database, not overwriting.

    As the system replaces the entire record, you must provide the full submission object once again, including all fields and not just the altered ones.

    Failing to provide information in required fields will lead to rejection of the change, and the old record will remain. Failing to provide information in optional fields will empty those fields, even if they were filled before, and will thus cause deletion of the information.

## Sandbox

The DEQAR Sandbox, like any sandbox, is intended for you to “play”, enabling you to trial particular submission methods, data structures, formats and syntax. More specifically, it is a space where we encourage (even urge) you to test your submissions before putting them into the live system.

The Sandbox is reached through separate links:

* To test the manual and CSV submission, go to the Sandbox Administrative Interface at: <{{ deqar.sandbox.admin }}/>
* To test API submission, go to the Sandbox Submission API at: <{{ deqar.sandbox.backend }}/submissionapi/v2/submit/report>
* To see what your records will eventually look like on the public site, go to the Sandbox Public Interface at: <{{ deqar.sandbox.frontend }}/>

The Sandbox is an identical copy of the live system. The entire data of the live site is copied over to the Sandbox every night. Thus, your login and password are the same as in your DEQAR account—unless you have made changes within the last 24 hours. You can also reset or change your password in the Sandbox, but it will be overwritten by the next day.

