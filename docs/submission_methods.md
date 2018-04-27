Web Form
--------

The DEQAR administrative interface includes an interactive web form, allowing you to submit single reports. The administrative interface is available at:

<https://admin.deqar.eu/>
    
Your username is your agency's acronym (in lower case), your default password is the acronym followed by `#2018`.

The web form can be found in the menu under *Submit Report* > *[Report Form](https://admin.deqar.eu/report-form)*.

Required fields are marked with a <span style="color: #f00;">\*</span> in the form. Fields marked with a <span style="color: #f00;">(\*)</span> are conditionally required: for example, you need to enter either an URL or select a file for upload when adding a report file. The *Save Record* button becomes active once all required information has been provided.

In several instances (Institutions, Programmes, Report Files) you are able to select/add one or more items. In those cases you will find form fields for one item on the left, followed by an *Add* button. On the right, you will see the item(s) selected/added, with buttons to remove or edit.

**Core Data**

Please note that the *Activity* chosen might influence which information is required.

We strongly recommend that you provide a *Local Report Identifier* which identifies the specific report in your own information system or workflow. This will facilitate later updates should they be necessary.

**Institutions**

A report needs to relate to one or more (e.g. in case of joint programmes) institution(s). You can add institutions using the search box or browse the full list by country.

**Programmes**

The programme tab will only be active if your report belongs to an activity that is not a purely institutional type.

Fill the form with the required information and then click the *Add Programme* button. If the report concerns several programmes (e.g. clustered evaluation) please repeat the step for all programmes concerned.

**Report Files**

Each report may contain one or more report files (for example, the experts' report, a possible summary report and the decision taken might be contained all in one or in separate files).

Files can be provided by link or directly uploaded. For each file, please specify the language(s) of the contents. The display name is optional; the text "Report" will be used as a default otherwise.

CSV Upload
----------

[Comma-separated values](https://en.wikipedia.org/wiki/Comma-separated_values) is a common platform-independent, software-independent data-exchange format. Files can be exported from all usual [spreadsheet software](#preparingexporting-csv-files) and numerous other applications.

The first row of your file should include column names as defined under [Data Preparation](submission_object_fields.md) above. A simple example for institution-level reports could look as follows:

```csv
agency,activity,status,decision,valid_from,valid_to,date_format,file[1].original_location,file[1].report_language[1],institution[1].eter_id
```

The following lines contain one report per row.

While CSV is a one-dimensional format, one report may often include/relate to several items: one or more institution(s), programmes or files (which each might contain several languages). These can be provided/identified in separate columns named `field_name[n]` with `n` = 1, 2, ...

For example, two files (e.g. full report in local language, and summary in both English and local language) can be provided as follows:

```csv
..., file[1].original_location,   file[1].display_name, file[1].report_language[1], file[2].original_location,   file[2].display_name, file[2].report_language[1], file[2].report_language[1], ...
..., "http://some.url/to/report", "Expert report",      "de",                       "http://some.url/to/report", "Summary",            "en",                       "de", ...
```
(Spaces added for readability, these should not appear in an actual file.)

### Template and samples

You can use one of the sample CSV files below as a starting point and adjust it to your needs. Please bear in mind the following:

 - The sample file is provided on Google Docs as well as in Microsoft Excel and Open Document Formats. It needs to be saved in CSV format for upload to DEQAR (see notes below).
 - The first worksheet includes *all* possible column names you could use in a CSV file, with the respective requirement/validation notes as comments. These comments will disappear as you save the file in CSV format.
 - The subsequent worksheets include more condensed examples with sample data, including those columns that will typically be used in reports concerning institutions, programmes or joint programmes.
 - You need to include all columns you might need in at least one of your reports, but they can stay empty in those lines where they are not applicable.
 - You may omit columns from the sample CSV file that are not used in any of the reports.
 
 - [Microsoft Excel format](http://link.to/somewhere/)
 - [Open Document Format (OpenOffice/LibreOffice/NeoOffice)](http://link.to/somewhere/)
 - [Google Docs](http://link.to/somewhere/)
 - CSV format (only examples, without comments): [Institutional reports](http://link.to/somewhere/), [Programme reports](http://link.to/somewhere/), [Joint programme reports](http://link.to/somewhere/)

### Preparing/exporting CSV files

Despite being software-independent, there are some known issues when creating/exporting CSV files from some major office applications. Given that it has the most clean and straight-forward CSV export, we recommend the [LibreOffice package](https://www.libreoffice.org/), an open-source desktop application supported on all major operating systems.

For all software packages, please note that CSV format does not support different sheets, but it will always be only the current work sheet that is saved in CSV format.

#### Microsoft Excel

Despite offering CSV as a target file type in its *Save as* dialogue, Microsoft Excel does not create correct CSV files when certain character sets are used (e.g. Greek or Cyrillic alphabets, or certain Roman characters with diacritics). You can use the following work-around:

 - Select *Save as* from the *File* menu, select your desired folder and choose *Unicode Text (\*.txt)* as type.<br />
   ![Excel save as dialogue](img/csv-excel-fix-0.png)
 
 - Simply press *OK* in response to the following error message:<br />
   ![The selected file type does not support workbooks that contain multiple sheets](img/csv-excel-fix-1.png)

 - Furthermore, confirm with *Yes* also the following warning message:<br />
   ![Some features in your workbook might be lost if you save it as Unicode Text](img/csv-excel-fix-2.png)

 - Close Microsoft Excel and navigate to the folder containing your file in the file manager. Right-click on your file and choose *Rename*.
 
 - Now change the file extension from `.txt` into `.csv`. You will encounter the following message: *If you change file name extension, the file may become unusable. You still want to change them, you should press ‘Yes’...* Confirm the warning by clicking Yes.
 
 - This CSV file is now suitable for upload.
 
#### LibreOffice/OpenOffice/NeoOffice

Exporting CSV files is straight-forward in LibreOffice, OpenOffice and NeoOffice:

 - Choose *Text CSV (\*.csv)* as file type in the *Save As ...* or *Save a Copy ...* dialogue:<br />
   ![LibreOffice save file dialogue](img/csv-libreoffice-0.png)

 - Ensure the export settings are set as follows in the next dialogue. Please pay particular attention character set and delimiters:<br />
   ![CSV export settings](img/csv-libreoffice-0.png)

 - The CSV file is now suitable for upload.
 
#### Google Sheets

In Google Sheets, choose *Comma-separated values* from the *File* > *Download as...* menu.

### Uploading CSV files

The CSV upload module is part of the DEQAR admin interface:

<https://admin.deqar.eu/upload-csv>

The username is the agency’s acronym (in lower case, see reference list). For the testing period, the password is the username followed by `#2018`.

 - Select *Submit Report* > *Upload CSV* from the menu.
 
 - Choose your file under *Select CSV file* and click *Upload*.
 
 - You can now review your data one more time under *Uploaded CSV Data*, and make changes if necessary.

 - Afterwards, click on *Ingest* under the table. The uploaded CSV file now passes the same validation and flagging pipeline as information submitted through any other method.

 - After ingest, you will see all rows highlighted in green if they were succesfully injected, or in red if they could not be ingested due to validation errors. Click on one row to see details about errors or flags in the top-right corner.
 
 - If you experienced errors, you can correct the respective lines and click on *Ingest* again.
 
 - Please note that the green rows will be re-ingested, but overwrite the existing report based on the DEQAR Report ID. Any changes you make to green rows will therefore be recorded on further ingest.

Submission API
--------------

REST API is a convenient way for software developers to communicate with web
services via HTTP, the protocol used by the internet. Together with JSON it
provides an easy, straightforward and flexible means of exchanging data between
systems. With the possibility of sending complex request and response objects,
we can accept structured data and give immediate feedbacks (e.g. error checks,
warnings) about the submitted data as well as metadata enhancements (e.g. ETER
IDs on HEIs, when applicable; links to new records on the EQAR public interface,
etc.).

### Authentication

Requests for submission to DEQAR are only accepted from registered users and
must therefore be identified. DEQAR API endpoints manage authentication using
API Tokens (through the so-called Bearer Authentication method). Upon
registration, an API Token (which is basically a hash) is created for each user.
Sending this token in the Authorization header will authenticate the user in
place of a regular username and password.

To get your authentication token you can send a `POST` request to the following URL:

`https://backend.deqar.eu/accounts/get_token/`

An example of obtaining a token using curl in command line:

```
curl -s -H "Content-Type: application/json" -XPOST https://backend.deqar.eu/accounts/get_token/ --data '{"username":"testuser","password":"testpassword"}'
```

The username is the agency’s acronym (in lower case). For the testing period, the password is the username followed by #2018.

Or for those who prefer to use the more user friendly httpie3 client:

```
http POST https://eqar-backend.herokuapp.com/accounts/get_token/ 'username=testuser' 'password=testpassword'
```

### Report Submission Endpoint

The address of the submission endpoint is:

`https://backend.deqar.eu/submissionapi/v1/submit/report`

This is the URL that you can use to make a `POST` request including the Submission
Request Object as JSON object, or many objects as JSON array of objects in the
request body.

#### Submission Request Object

The Submission Request Object is the JSON object (or array of objects) which is
the manifestation of a report or set of reports an agency wants to submit.
Fields names and accepted types are as described in [Data Preparation](submission_object_fields.md).

The full definition of request and response objects can be find in OpenAPI format under:

[https://app.swaggerhub.com/apis/EQAR/SubmissionAPI/1.0.0](https://app.swaggerhub.com/apis/EQAR/SubmissionAPI/1.0.0)

### Report File Submission Endpoint

Files (PDF versions of reports) can be submitted in two separate ways:

 - URLs submitted with a Submission Request Object will be harvested asynchronously upon successful submission.
 - Files can be submitted directly to a dedicated endpoint as part of a `PUT` request:
   `https://backend.deqar.eu/submissionapi/v1/submit/reportfile/<report_file_id>/<filename>`

   `report_file_id`: The id number of the Report File object available in the
response after successful submission. The `report_file_id` is contained in the response object of the successful report submission.
   `filename`: The name of the file that you will submit in this request.

### Examples

The examples below show how a JSON Submission Request Object might look for different types of reports:

- [Institutional report](https://raw.githubusercontent.com/EQAR/eqar_backend/master/submissionapi/examples/institutional.json)
- [Programme report](https://raw.githubusercontent.com/EQAR/eqar_backend/master/submissionapi/examples/programme.json)
- [Institutional/Programme report](https://raw.githubusercontent.com/EQAR/eqar_backend/master/submissionapi/examples/institutional_programme.json)
- [Joint Programme report](https://raw.githubusercontent.com/EQAR/eqar_backend/master/submissionapi/examples/joint_programme.json)
