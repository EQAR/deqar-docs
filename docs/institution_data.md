# Institution Data

Each report must be associated with at least one institution. If a record already exists in DEQAR, the institutions needs to be identified; otherwise, the institution must be created **before** a report can be submitted.

DEQAR has records on a large number of higher education institutions (over 4000 institutions from 42 European countries) harvested from the ETER/OrgReg databases (available through [Research infrastructure for research and innovation policy studies - RISIS](http://datasets.risis.eu/) or [European Tertiary Education Register - ETER](https://www.eter-project.com/). More than 2000 additional institutions are already recorded in DEQAR based on other official sources (e.g. lists by national ministries) or have already been added by other agencies.

## Finding Existing Institutions

Existing institutions need to be identified by their DEQARINST ID, ETER ID or a local or national identifier (if available).

### Admin Interface

All [institution identifiers](architecture_data_model.md#institution-identifiers) can be found through the [administrative interface](https://admin.deqar.eu/reference/institutions).

**Important:** The public [DEQAR website](https://www.deqar.eu/) does *not* show all institutions, but only those institutions for which at least one report is available. It is therefore important that you **always search for institutions in the [administrative interface](https://admin.deqar.eu/reference/institutions)**, as DEQAR contains records on several hundreds of institutions for which no reports have been submitted yet.

Reports on existing institutions can be submitted directly, providing identifiers in CSV or JSON objects as described under [Submission Object Data Elements: Institution(s)](report_data.md#institutions) or by selecting the institution in the web form.

### Download CSV File

The full list of higher education institutions can also be downloaded as a CSV file from:

<https://www.eqar.eu/qa-results/download-data-sets/>

### Connect API

The full institution list can be accessed and searched using the Connect API. EQAR-registered agencies have access to the Connect API using the same credentials as for the DEQAR administrative interface, the Submission API and the Web API.

Please refer to the [explanations on authentication for the Submission API](data_submission.md#authentication) for information on how to obtain and use a token.

The base URL for the Connect API is:

`https://backend.deqar.eu/connectapi/v1`

The endpoint <https://backend.deqar.eu/connectapi/v1/institutions/> allows to query the full list of higher education institutions, with or without reports.

The full definitions of the endpoint, the search parameters and the response object is available as [OpenAPI Specification 3.0](https://en.wikipedia.org/wiki/OpenAPI_Specification) at:

<https://backend.deqar.eu/connectapi/v1/swagger/>

To retrieve the details on a single institution, please use the [Web API endpoint](web_api_endpoints.md#institutions).

## Defining Institutions

Before suggesting to add a new institution, please consider the following notes:

 1. DEQAR mainly follows European Tertiary Education Register's (ETER) [data model and coverage](https://eter-project.com/#/info/coverage).

 2. The primary unit of registration is the university/higher education institution, i.e. an institution of higher learning that awards academic degrees in diverse disciplines, is organised as central unit and consists of separate functional units (i.e. faculties, institutes, schools, departments).

 3. Functional units (i.e. faculties, institutes, schools, departments) themselves are not registered in DEQAR as separate entity. Reports on functional units are uploaded/recorded/shown under the central unit's record.

 4. Reports on consortia consisting of several universities will be showcased in the record of each university separately. Consortia themselves will not be presented as a central unit.

    Only in exceptional cases, when the consortium has a long-term tradition of organising education and is recognised by stakeholders as an institution itself, will it be registered as a separate institution in DEQAR.

 5. Reports on institutions' branches and campuses, home and abroad, will be showcased in the record of the central institution (i.e. the university). Only in exceptional cases, where the branch/campus has a proven long-term tradition of organising education and is recognised by stakeholders as a semi-independent institution, will it be registered in DEQAR.

 6. In cases when the status of the entity is not clearly determined by the aforementioned cases or the status is debatable, EQAR and the agency will discuss the nature of it taking into account five main indicators:

    - legal status
    - organisational independence
    - financial independence
    - stakeholders’ perceptions
    - local context and approaches to higher education

## Institution Data Elements

If a record for an **institution does not already exist in DEQAR** it should be described with the elements below; required elements are marked by **(\*)**. Before a new record is created, data will be checked against institution data already in DEQAR. If a DEQAR institution record is identified as a match, the existing record will take precedence over submitted data.

|ELEMENT NAME |REQUIRED |ONE/MANY |EXAMPLE |
|:--------------------------------------------|:------------|:---------|:-----------------------|
|**Official Institution Name (\*)** |yes |one |*Graz University of Technology*<br>*Югозападен университет "Неофит Рилски"*<br>*Πληροφορίες για τους αλλοδαπούς φοιτητές: Είσοδος και προγράμματα*|
|Official Institution Name, transliterated |no |one |*Yugo-zapaden universitet "Neofit Rilski”*<br>*Plirophoríes yia tous allodapoús phitités: Ísodos kai prográmmata*|
|English Institution Name |no |one |*South-West University "Neofit Rilski", Blagoevgrad*|
|Institution Acronym |no |one |*SWU* |
|**Institution Country (\*)** |yes |many (per)|*BG*<br>*BGR* |
|Institution City |no |many (per)|*Sofia* |
|Institution Latitude<br>Institution Longitude|no |many (per)|*48,208,356; 1,636,776* |
|Institution QF-EHEA Level |no |many (per)|*0 - short cycle*<br>*1 - first cycle*<br>*2 - second cycle*<br>*3 - third cycle*|
|**Institutional Website (\*)** |yes |one |*http://www.swu.bg* |

### Name(s)

One and only one official institution name must be provided for each new institution record. Each official institution name that is in a non-Latin script should be accompanied by a transliterated version to support search and discovery. It is also recommended that agencies provide an English institution name for each new institution record. If provided, the English name will be used for display. An institution acronym may also be provided. (Note: alternative or other language institution names can be provided through the administrative interface.)

* **Official Institution Name (\*)** (<code>name_official</code>; required; string)  
  The official name of each institution in the original alphabet must be provided for every new institution record. The official name will be indexed for search and may be used as the primary institution name in the search interface if no English institution name is assigned.  
  *e.g. Graz University of Technology*  
  *e.g. Югозападен университет "Неофит Рилски"*  
  *e.g. Πληροφορίες για τους αλλοδαπούς φοιτητές: Είσοδος και προγράμματα*

* Official Institution Name, transliterated (<code>name_official_transliterated</code>; not required; string)  
  A romanised transliteration should be provided if the official institution name is in non-Latin script. If no romanised form is stored locally, then [ISO romanisation standards](https://en.wikipedia.org/wiki/List_of_ISO_romanizations) can be used to created romanised forms. If transliteration is not provided, access to the institution record through the search interface will be more limited. For those languages included in the [Python transliterate package](https://pypi.org/project/transliterate/) transliterations can be generated automatically when [supplying institution data in bulk](#bulk-upload).
  *e.g. Yugo-zapaden universitet "Neofit Rilski”*  
  *e.g. Plirophoríes yia tous allodapoús phitités: Ísodos kai prográmmata*

* English Institution Name (<code>name_english</code>; recommended; string)  
  A single English institution name may be provided for any institution without an English official name. If provided, the English institution name will be used as the primary institution name in the search interface. While not required, providing an English name is strongly recommended to enhance the user experience.  
  *e.g. South-West University "Neofit Rilski", Blagoevgrad*

* Institution Acronym (<code>acronym</code>; not required; string)  
  The official acronym for each institution may be provided. This will be indexed for search.  
  *e.g. SWU*

### Location

One or more countries must be provided for each new institution record. One city may be provided to correspond with each country along with an optional latitude and longitude. In the case that the institution is located in more than one city in the same country, then this would require a separate country/city entry for each city.

* **Institution Country (\*)** (<code>country_id</code>; conditionally required; string)  
  The country/ies where each institution is located must be provided for every new institution record. Each country must be provided using either an ISO 3166 alpha2 or ISO 3166 alpha3 country code (see [ISO 3166-1 standard](https://en.wikipedia.org/wiki/ISO_3166-1)), or using the DEQAR numerical ID. Institution countries will be indexed for search.  
  *e.g. BG*  
  *e.g. BGR*

* Institution City (<code>city</code>; recommended; string)  
  The city name, preferably in English, where the institution is located in each country may be provided for each institution record. If an institution is located in more than one city, then a separate country/city pairing should be entered for each city. Institution cities will be indexed for search.
  *e.g. Sofia*

* Institution Latitude (<code>latitude</code>; not required; float)
* Institution Longitude (<code>longitude</code>; not required; float)  
  The exact latitude and longitude of the institution site or the general latitude and longitude of the city of the institution may also be provided for each institution record.  
  *e.g. 48,208,356; 1,636,776*

### Qualification Level

The institution QF-EHEA levels may be provided for each institution. If QF-EHEA levels are provided, then *ALL* levels covered by the institution should be recorded. QF-EHEA levels may be provided as either string values or DEQAR IDs.

* Institution QF-EHEA Level (<code>qf_ehea_levels</code>; required; string)  
  One or more institution QF-EHEA levels may be provided as either a DEQAR QF-EHEA level name or a DEQAR QF-EHEA level id for each institution record (see [Framework for Qualifications of the European Higher Education Area](http://ecahe.eu/w/index.php/Framework_for_Qualifications_of_the_European_Higher_Education_Area). These are the qualification framework levels at which each institution may award degrees. (Note: if QF-EHEA levels are provided, then all levels covered by the institution should be provided at the same time.)

|ID |name |
|:--|:-----------|
|0 |short cycle |
|1 |first cycle |
|2 |second cycle|
|3 |third cycle |

### Website

One and only one website link must be provided for each new institution record. When possible, the root domain name of the institution website should be provided without language or other qualifiers.

* **Institutional Website (\*)** (<code>website_link</code>; required; string)  
  The URL to the primary institution website or home page should be provided for every new institution record. The root domain name of the site should be used when possible.  
  *e.g. http://www.swu.bg*

### Identifier

You may provide a local or other identifier for the institution, which can later be used to identify this institution in report submission objects. Local identifier are for use by your agency only, whereas other identifiers can be used also by others.

* Institutional Identifier (<code>identifier</code>; not required; string)  
  The identifier for this institution. Please note that identifiers must be unique within your agency or within the resource provided.  
  *e.g. HCERES21*

* Identifier Resource (<code>identifier_resource</code>; not required; string)  
  If the identifier is not a local identifier of your agency, please provide a short label designating the resource in order to distinguish it from other identifiers. As the resource tag needs to be used consistently, and the combination of identifier and resource tag needs to be globally unique in DEQAR, it should be agreed with the EQAR secretariat.  
  *e.g. DE-HRK*

### Dates

Founding and closing years or dates can be provided if known.

* Founding date (<code>founding_date</code>; not required; date)
* Closing date (<code>closing_date</code>; not required; date)  
  Dates should be formated as *YYYY-MM-DD* and years should be given in four digits (*YYYY*).
  *e.g. 2020-07-01*

### Hierarchical Relationship

* Parent institution (<code>parent_id</code>; not required; string)  
  If the institution is a faculty or independent unit of another institution, or is part of a grouping of institutions that is also recorded in DEQAR, ETER or OrgReg, you should specify the parent institution. The parent institution can be specified by its DEQARINST ID, optionally in numerical form without the prefix *DEQARINST*.
  *e.g. DEQARINST4711*

## How to Provide Data

If you identify that institutions are missing, please send us a spreadsheet with the required data.

Before sending data on a new institution, please check carefully that the institution is not yet listed in the [reference list of institutions](https://admin.deqar.eu/reference/institutions). It is important to use the administrative interface to do so, as there are many institutions already recorded in DEQAR for which no reports have been uploaded yet. These are visible in the administrative interface, but not in the public interface.

Please supply the institution data using the template available in two formats:

* [Open Document Format](files/Template_HEI_lists.ods) (OpenOffice, LibreOffice, NeoOffice)
* [Microsoft Excel format](files/Template_HEI_lists.xlsx)
* [View on-line](https://cloud.eqar.eu/s/f9xo8yXYoH8ZFrA)

You may save the spreadsheet in either format or as a CSV file. Send the filled spreadsheet to [deqar@eqar.eu](mailto:deqar@eqar.eu); we will check the list shortly and return your original file with the newly generated DEQARINST IDs added.

