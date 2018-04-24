File format
-----------

[Comma-separated values](https://en.wikipedia.org/wiki/Comma-separated_values) is a common platform-independent, software-independent data-exchange format.

The first row of your file should include column names as defined in [...link to add...](http://www.deqar.eu).

The following lines contain one report per row. Where one report may include/relate to several items (e.g. institutions, programmes, files), these can be provided/identified in separate columns using the `field_name[n]` syntax.

For Example, two files (e.g. full report in local language, and summary in both English and local language) can be provided as follows:

```csv
...,file[1].original_location,file[1].display_name,file[1].report_language[1],file[2].original_location,file[2].display_name,file[2].report_language[1],file[2].report_language[1],...
...,"http://some.url/to/report","Expert report","de","http://some.url/to/report","Summary","en","de",...
```

You can use our sample CSV file as a starting point and adjust it to your needs. Please bear in mind the following:

 - The sample file is provided in Microsoft Excel and Open Document Formats. It needs to be saved in CSV format for upload to DEQAR (see notes below).
 - The first line contains the relevant requirement/validation notes for the column as a comment. These comments will disappear as you save the file in CSV format.
 - You need to include all columns you might need in at least one of your reports.
 - omit columns you don't need
 
Exporting beautiful CSV
=======================

Microsoft Excel
---------------

tricky

Google Sheets
-------------

less tricky

LibreOffice/OpenOffice/NeoOffice
--------------------------------

sound different, but all the same

CSV Upload Test
===============

A testing module is available to try the CSV upload under the following
address:

[https://backend.deqar.eu/csvtest/upload/]

The username is the agency’s acronym (in lower case, see reference list).
For the testing period, the password is the username followed by #2018.

After a successful login on the login page, a simple form is available to upload
the submission CSV files. Please refer to the Submission Template to create your
CSV files.

The uploaded CSV file goes through the same validation and flagging procedure as
the JSON package. Submission results are displayed directly in the browser,
under the submission form.

