# Provider Data

Each report must be associated with at least one higher education provider. If a record already exists in DEQAR, the provider needs to be identified; otherwise, the provider must be created **before** a report can be submitted.

## Providers in DEQAR

DEQAR distinguishes two types of providers - higher education institutions and alternative providers. DEQAR only registers providers which provide learning opportunities at the QF-EHEA Levels (equivalent to EQF and ISCED levels 5 to 8). Vocational education and training provisions at EHEA QF level 5 which are not considered as higher education in the national systems are not included.

The main difference between the two types of providers is whether the entity has full degree awarding powers or not. The number of programmes for which the provider has awarding powers, the subject area and the mode of delivery of the programme is not important for the differentiation.

|   | Higher education institution | Alternative provider           |
|:--|:-----------------------------|:-------------------------------|
| QF-EHEA/EQF Levels 5-8 | Yes | Yes |
| Provides short courses (< 90 ECTS) | Yes, optionally | Only short courses |
| Courses lead to full degree (bachelor, master, PhD degree) | Yes | No |
| Courses can lead to other types of certificates (e.g. nano or micro degree, badges etc.) | Yes | Yes|

In case of doubt of the nature of the provider, agencies are advised to consult with the EQAR Secretariat at deqar@eqar.eu. Should this be the case, agencies are encouraged to share materials on the provider, and any other evidence that could help in concluding the status.

## Finding Existing Providers

Existing providers need to be identified by their DEQARINST ID, ETER ID (for higher education institutions), another international identifier, or a local or national identifier (if available).

DEQAR has records on a large number of higher education institutions (over 4000 institutions from 42 European countries) harvested from the ETER/OrgReg databases (available through [Research infrastructure for research and innovation policy studies - RISIS](http://datasets.risis.eu/) or [European Tertiary Education Register - ETER](https://www.eter-project.com/). More than 2000 additional providers are already recorded in DEQAR based on other official sources (e.g. lists by national ministries) or have already been added by other agencies.

### Admin Interface

All [provider identifiers](architecture_data_model.md#provider-identifiers) can be found through the [administrative interface](https://admin.deqar.eu/reference/institutions).

> **Important:** The public [DEQAR website](https://www.deqar.eu/) does *not* show all providers, but only those organsations for which at least one report is available. It is therefore important that you **always search for providers in the [administrative interface](https://admin.deqar.eu/reference/institutions)**, as DEQAR contains records on several hundreds of higher education institutions and some alternative providers for which no reports have been submitted yet.

Reports on existing providers can be submitted directly, providing identifiers in CSV or JSON objects as described under [Submission Object Data Elements: Institution(s)](report_data.md#institutions) or by selecting the provider in the web form.

### Download CSV File

The full list of providers can also be downloaded as a CSV file from:

<https://www.eqar.eu/qa-results/download-data-sets/>

### Connect API

The full providers list can be accessed and searched using the Connect API. EQAR-registered agencies have access to the Connect API using the same credentials as for the DEQAR administrative interface, the Submission API and the Web API.

Please refer to the [explanations on authentication for the Submission API](data_submission.md#authentication) for information on how to obtain and use a token.

The base URL for the Connect API is:

`https://backend.deqar.eu/connectapi/v1`

The endpoint <https://backend.deqar.eu/connectapi/v1/institutions/> allows to query the full list of higher education institutions, with or without reports.

The endpoint <https://backend.deqar.eu/connectapi/v1/providers/> allows to query the full list of all providers, with or without reports. The list can be filtered by type of provider, i.e. higher education instutitons and alternative providers.

The full definitions of the endpoints, the search parameters and the response object is available as [OpenAPI Specification 3.0](https://en.wikipedia.org/wiki/OpenAPI_Specification) at:

<https://backend.deqar.eu/connectapi/v1/swagger/>

To retrieve the details on a single provider, please use the [Web API endpoint](web_api_endpoints.md#institutions).

## Defining Higher Education Institutions

Before suggesting to add a new higher education institution, please consider the following notes:

 1. DEQAR mainly follows European Tertiary Education Register's (ETER) [data model and coverage](https://eter-project.com/#/info/coverage).

 2. The primary unit of registration is the university/higher education institution, i.e. an institution of higher learning that awards full recognised academic degrees in diverse disciplines, is organised as central unit and consists of separate functional units (i.e. faculties, institutes, schools, departments). The degree-awarding powers of the institution are recognised by at least one national authority.

 3. Functional units (i.e. faculties, institutes, schools, departments) themselves are not registered in DEQAR as separate entity. Reports on functional units are uploaded/recorded/shown under the central unit's record.

 4. Reports on consortia consisting of several providers will be showcased in the record of each provider separately. Consortia themselves will not be presented as a central unit.

    Only in exceptional cases, when the consortium has a long-term tradition of organising education and is recognised by stakeholders as an institution itself, will it be registered as a separate institution in DEQAR.

 5. Reports on institutions' branches and campuses, home and abroad, will be showcased in the record of the central institution (i.e. the university), while such additional branches/campuses will be shown as further locations of the institution. Only in exceptional cases, where the branch/campus has a proven long-term tradition of organising education and is recognised by stakeholders as a semi-independent institution, will it be registered in DEQAR.

 5. Providers that award full recognised degrees through a franchise or validation partnership with a higher education institution, but have no own degree-awarding power, will be recorded as an alternative provider.

 6. In cases when the status of the entity is not clearly determined by the aforementioned cases or the status is debatable, EQAR and the agency will discuss the nature of it taking into account five main indicators:

    - legal status
    - provideral independence
    - financial independence
    - stakeholders’ perceptions
    - local context and approaches to higher education

## Defining Alternative Providers

In DEQAR, an alternative provider is an provider that delivers content or provides skills training:

 1. At higher education level (i.e. EHEA QF level 5 to 8; EQF 5 to 8; EHEA cycle first to third)

 2. Does not have a full degree awarding powers (i.e. right to award bachelor, master or PhD degrees)

 3. Whose educational offer is of short nature (i.e. less workload/ECTS than a full short degree - i.e. <90 ECTS)

The mode of delivery of the classes, whether the provision is done independently or in partnership with a higher education institution, the ownership of the provider (e.g. private or public provider), the connection to the labour market and the area of study are not defining elements of the providers "alternative providers" in DEQAR.  

The use of terminology “alternative providers” varies between systems/countries. For example, in the UK, alternative providers are higher education providers who do not receive recurrent funding from Office for Students (previously HEFCE) or other public body and who are not further education colleges. The degree awarding status is not taken in consideration when defining the status in this system.

Reports for programmes done as a collaboration between a higher education institution and an alternative provider that organises programmes in the field of HE will be showcased under both entities respectively.

Similarly, an provider that offers education programmes under a franchise or validation agreement with a higher education institution would be considered an alternative provider, whereas the franchise/validation partnership would be reflected as a linkage with the HEI concerned.

## Provider Data Elements

If a record for an **provider does not already exist in DEQAR** it should be described with the elements below; required elements are marked in bold or by a **\***. Before a new record is created, data will be checked against provider data already in DEQAR. If a DEQAR provider record is identified as a match, the existing record will take precedence over submitted data.

|ELEMENT NAME |REQUIRED FOR HEIs IN OrgReg |REQUIRED FOR HEIs NOT IN OrgReg |REQUIRED FOR APs |ONE/MANY |EXAMPLE |
|:------------|:---------------------------|:-------------------------------|:----------------|:--------|:-------|
|**Official Name** |yes |yes |yes |one |*Graz University of Technology*<br>*Югозападен университет "Неофит Рилски"*<br>*Πληροφορίες για τους αλλοδαπούς φοιτητές: Είσοδος και προγράμματα*|
|Official Name, transliterated |no |no |no |one |*Yugo-zapaden universitet "Neofit Rilski”*<br>*Plirophoríes yia tous allodapoús phitités: Ísodos kai prográmmata*|
|English Name |no |no |no |one |*South-West University "Neofit Rilski", Blagoevgrad*|
|Acronym |no |no |no |one |*SWU* |
|**Location Country** |yes |yes |yes |many |*BG*<br>*BGR* |
|**Location City** |yes |yes |yes |many |*Sofia* |
|**Location Postcode** |yes |no |no |many |*Sofia* |
|Location Latitude & Longitude|no |no |no |many |*48.208356; 1.636776* |
|**Website** |yes |yes |yes |one |*http://www.swu.bg* |
|**Other Identifier** |no |yes |yes |many |*IAU-019335* |
|Identifier Resource |no |yes |yes |many |*WHED* |
|Identifier Source |no |yes (conditionally)|yes (conditionally) |many |*National register of learning providers in the UK, see https://www.ukrlp.co.uk/* |
|Type of provider |n/a |n/a |no |one |*private* |
|Qualification Level |no |no |yes |many |*0 - short cycle*<br>*1 - first cycle*<br>*2 - second cycle*<br>*3 - third cycle*|

```mermaid
erDiagram
    PROVIDER {
	TYPE FIELD "EXAMPLE"
        str website "http://www.swu.bg"
        str provider_type "private"
    }
    NAME {
	TYPE FIELD "EXAMPLE"
        str name_official "Graz University of Technology"
        str name_transliterated "Yugo-zapaden universitet 'Neofit Rilski'"
        str name_english "South-West University 'Neofit Rilski'"
        str acronym "SWU"
        date valid_until
    }
    LOCATION {
	TYPE FIELD "EXAMPLE"
        str country FK "BG, BGR"
        str city "Sofia"
        str postcode "4711"
        float latitude "48.208356"
        float longitude "1.636776"
    }
    IDENTIFIER {
	TYPE FIELD "EXAMPLE"
        str identifier "IAU-019335"
        str resource "WHED"
    }
    PROVIDER ||--|{ NAME : "known as"
    PROVIDER ||--|{ LOCATION : "based in"
    PROVIDER ||--o{ IDENTIFIER : "identified by"
```

### Name(s)

One and only one official provider name must be provided for each new provider record. Each official name that is in a non-Latin script should be accompanied by a transliterated version to support search and discovery. An English provider name should be provided for each new provider record. If provided, the English name will be used for display. An provider acronym may also be provided. (Note: alternative or other language names can be provided through the administrative interface.)

* **Official Name\*** (<code>name_official</code>; required; string)  
  The official name of each provider in the original alphabet must be provided for every new provider record. The official name will be indexed for search and may be used as the primary provider name in the search interface if no English institution name is assigned.

    *e.g. Graz University of Technology*  
    *e.g. Югозападен университет "Неофит Рилски"*  
    *e.g. Πληροφορίες για τους αλλοδαπούς φοιτητές: Είσοδος και προγράμματα*

* Official Name, transliterated (<code>name_official_transliterated</code>; not required; string)  
  A romanised transliteration should be provided if the official provider name is in non-Latin script. If no romanised form is stored locally, then [ISO romanisation standards](https://en.wikipedia.org/wiki/List_of_ISO_romanizations) can be used to created romanised forms. If transliteration is not provided, access to the provider record through the search interface will be more limited. For those languages included in the [Python transliterate package](https://pypi.org/project/transliterate/) transliterations can be generated automatically when [supplying provider data in bulk](#bulk-upload).

    *e.g. Yugo-zapaden universitet "Neofit Rilski”*  
    *e.g. Plirophoríes yia tous allodapoús phitités: Ísodos kai prográmmata*

* English Name (<code>name_english</code>; recommended; string)  
  A single English provider name should be provided for any provider without an English official name. If provided, the English name will be used as the primary name for display in the DEQAR interface; the search, however, always matches against all name versions/variations. While not required, providing an English name is strongly recommended to enhance the user experience.

    *e.g. South-West University "Neofit Rilski", Blagoevgrad*

* Provider Acronym (<code>acronym</code>; not required; string)  
  The official acronym for each provider may be provided. This will be indexed for search. It should thus be provided especially where it is commonly used to refer to the institution, so that it can be found more easily.

    *e.g. SWU*  
    *e.g. BOKU*

### Location


One or more locations must be provided for each new provider record. A location is provided as a combination of a country and a city name along with an optional latitude and longitude.

Each provider must have one and only one location designated as main legal seat.

For higher education institutions, the legal seat is considered as the higher education system in which the institution is formally recognised as such. In case an institution is a legal entity incorporated in country A but formally recognised as higher education institution in system B, the legal seat should specified in B. In case a higher education institution is formally recognised in several higher education systems, separate provider records should be created, one for each system.

For alternative providers, the legal seat is considered as the country in which the legal entity is incorporated.

For providers with multiple seats (e.g. branches), each of the locations (i.e. country and city) could be provided in a separate column with number in the brackets (`[n]`).

The first country (i.e. country_id) will be considered as the main legal seat of the provider.

* **Provider Legal Seat Country\*** (<code>country_id</code>; required; string)  
  The country where each provider has its legal seat (see above) must be provided for every new provider record.

    Each country must be provided using either an ISO 3166 alpha2 or ISO 3166 alpha3 country code (see [ISO 3166-1 standard](https://en.wikipedia.org/wiki/ISO_3166-1)), or using the DEQAR numerical ID. Provider countries will be indexed for search.

    *e.g. BG*  
    *e.g. BGR*

* **Provider Legal Seat City\*** (<code>city</code>; required; string)  
  The city name, preferably in English, where the provider has its legal seat may be provided for each provider  record. If an provider is located in more than one city, further cities can be provided as other locations (see below).

    *e.g. Sofia*

* **Provider Legal Seat Postcode\*** (<code>postcode</code>; conditionally required; string)  
  The postcode of the provider's legal seat.

    This field is required for higher education institution in systems covered by OrgReg/ETER.

    e.g. 1030

* Provider Legal Seat Latitude (<code>latitude</code>; not required; float)  
  Provider Legal Seat Longitude (<code>longitude</code>; not required; float)  
  The exact latitude and longitude of the organisaton site or the general latitude and longitude of the cityi may also be provided for each provider record.

    *e.g. 48,208,356; 1,636,776*

If the provider has further locations in the same or other countries, the agency may provide further information. In the CSV file, each additional location should be presented in a new column with the subsequent number in brackets (i.e. `[n+1]`).

The following set of columns can be copied for each additional location:

* Other Location Country (<code>other_location[n].country</code>; not required; string)  

* Other Location City (<code>other_location[n].city</code>; not required; string)  

* Other Location Postcode (<code>other_location[n].postcode</code>; conditionally required; string)  

* Other Location Latitude (<code>other_location[n].latitude</code>; not required; float)  
  Other Location Longitude (<code>other_location[n].longitude</code>; not required; float)

    The format and requirements are identical to the corresponding fields above.

### Qualification Level

The provider QF-EHEA levels may be provided for each higher education institution and must be provided for each alternative provider.

* Provider Qualification Level (<code>qf_ehea_level[n]</code>; conditionally required; string)  
  One or more qualification levels may be provided for higher education institutions and must be provided for alternative providers as either a DEQAR level name or a DEQAR level id. DEQAR uses levels based on three main frameworks/classifications:
    - [Framework for Qualifications of the European Higher Education Area](https://www.ehea.info/page-qualification-frameworks) (QF EHEA level),
    - [European Qualification Framework](https://europa.eu/europass/en/europass-tools/european-qualifications-framework) (EQF) and
    - [International Standard Classification of Education](https://uis.unesco.org/en/topic/international-standard-classification-education-isced) (ISCED).

    These are the qualification framework levels at which each higher education institution may award degrees or offer programmes at (for alternative providers). Note: if QF levels are provided, then *all* levels covered by the provider should be provided at the same time.

    In the CSV template, each level can be presented as ONE of the possible numbers OR words. Each additional level should be presented in a new column with the subsequent number in brackets (i.e. `[n+1]`).

    |ID (QF-EHEA level) |ID (EQF level, ISCED level) |name (QF-EHEA level) |
    |:--|:--|:-----------|
    |0  |5  |short cycle |
    |1  |6  |first cycle |
    |2  |7  |second cycle|
    |3  |8  |third cycle |

### Website

One and only one website link must be provided for each new provider record.

* **Provider Website (\*)** (<code>website_link</code>; required; string)  
  The URL to the primary provider website or home page. The root domain name of the site should be used when possible, without language or other qualifiers.

    *e.g. http://www.swu.bg*  
    *e.g. https://qualifications.pearson.com/*

### Identifier

Providing an identifier serves as proof of confirming the validity of the provider and aiding the users to find providers easily in other databases. The identifier can be used later to identify this provider in the report submission objects.

> A local identifier could be provided for the providers . Local identifier are for use by your agency only, whereas other identifiers can be used also by others.
> 
> Other identifier may be provided for higher education institutions in OrgReg and must be provided for higher education institutions which are not in OrgReg and for all alternative providers.
>
> EQAR runs a background list of other trusted identifiers presented below.

* Provider Identifier (<code>identifier</code>; conditionally required; string)  
  Please note that identifiers must be unique within your agency or within the resource provided.

    *e.g. HCERES21*

* Identifier Resource (<code>identifier_resource</code>; conditionally required; string)  
  If the identifier is not a local identifier of your agency, you must provide a short label designating the resource in order to distinguish it from other identifiers. As the resource tag needs to be used consistently, and the combination of identifier and resource tag needs to be globally unique in DEQAR, it should be communicated with the EQAR secretariat.

    *e.g. DE-HRK*

* Identifier Source (<code>identifier_source</code>; conditionally required; string)  
  The agency must provide other identifier for higher education institutions which are not in OrgReg and all alternative providers. The field must be filled in if the identifier is not yet known to EQAR (see table below for trusted identifiers). The source could be a national authority, an international provider or another entity.

    If the identifier is already known to EQAR (see table), there is no need to fill in this field.

    *e.g. World Higher Education Database*

The following common European or international identifier types are known in DEQAR and can be used without additional information, i.e. it is sufficient to provide the identifier resource, the identifier source does not need to be specified.

| Identifier resource | Title  | Source |
|:--------------------|:-------|:------------|
| DID-EBSI | DID for the European Blockchain Service Infrastructure (EBSI) | Decentralised Identifier (DID) that enables verifiable, decentralised digital identity within the EBSI ecosystem - data provided by higher education institutions participating in EBSI, see <https://ec.europa.eu/digital-building-blocks/wikis/display/EBSIDOC/EBSI+DID+Method> |
| Erasmus | Erasmus Institution Code | Identifier assigned by the European Commission to higher education institutions participating in the Erasmus+ programme - data harvested from ETER/OrgReg, see <https://erasmus-plus.ec.europa.eu/resources-and-tools/erasmus-charter-for-higher-education> |
| Erasmus-Charter | Erasmus Charter for Higher Education (ECHE) | Application number related to the ECHE, required for higher education institutions participating in the Erasmus+ programme - data acquired using the European University Foundation (EUF) HEI API, see <https://erasmus-plus.ec.europa.eu/resources-and-tools/erasmus-charter-for-higher-education> |
| EU-PIC | Participant Identification Code (PIC) | A PIC is assigned to legal entities participating in EU-funded programmes - data acquired using the European University Foundation (EUF) HEI API, see <https://ec.europa.eu/info/funding-tenders/opportunities/portal/screen/how-to-participate/participant-register> |
| EU-VAT | EU VAT number | Identifier of economic operators for value-added tax (VAT) within the EU system, assigned by their national authority - data acquired using the EU participant register API, see <https://ec.europa.eu/taxation_customs/vies/#/vat-validation> |
| SCHAC | SCHema for Academia | Internet domain (DNS)-based identifier of institutions, used in several European initiatives for data exchange in the education and research sector, e.g. Emrex - data acquired using the European University Foundation (EUF) HEI API, see <https://wiki.refeds.org/display/STAN/SCHAC> |
| WHED | IAU World Higher Education Database (WHED) | Identifier used in the world-wide WHED database of higher education institutions, managed by the International Association of Universities (IAU) - data harvested from ETER/OrgReg, see <https://www.whed.net/> |

The following table contains some examples of national identifiers already known in DEQAR:

| Identifier resource | Title  | Source |
|:--------------------|:-------|:------------|
| FR-SIREN | French Tax administration | see <https://sirene.fr/sirene/public/accueil> |
| UK-PIN | The UK Register of Learning Providers | see <https://www.ukrlp.co.uk/> |
| KZ-BIN | Kazakh Tax administration | see <https://kgd.gov.kz/en/services/taxpayer_search> |

### Dates

Founding and closing years or dates should be provided if known.

* Founding date (<code>founding_date</code>; not required; date)  
  Closing date (<code>closing_date</code>; conditionally required; date)  
  Dates should be formated as *YYYY-MM-DD* and years should be given in four digits (*YYYY*).

    The closing date must be provided if the provider is closed.

    *e.g. 2020-07-01*

### Hierarchical Relationship

* Parent Provider (<code>parent_id</code>; not required; string)  
  The parent can be specified by its DEQARINST ID, optionally in numerical form without the prefix *DEQARINST*.

    For higher education institutions: If the institution is a faculty or independent unit of another institution, or is part of a grouping of institutions that is also recorded in DEQAR, ETER or OrgReg, you should specify the parent institution.

    In case the parent institution is not in DEQAR or ETER/OrgReg, a request for adding the parent institution should be submitted too.

    For alternative providers: If the provider part of another provider that offers courses at higher education level, is part of a higher education institution, or is part of a grouping of providers that is also recorded in DEQAR the parent provider should be specified.

    If the parent provider is not recorded in DEQAR yet, a request for adding that provider should be submitted too. Please note that for DEQAR it is not relevant if the provider is part of a larger grouping that does work in fields other than higher education provision. Such relationships will not be recorded in DEQAR.

    *e.g. DEQARINST4711*

### Type of Alternative Provider

* Type of Alternative Provider (<code>type_provider</code>; not required; string)  
  Information of relevance only for alternative providers. The nature of the provider should be marked if known.

    Four main categories are defined:

    |ID |name |
    |:--|:-------|
    |1  |private company|
    |2  |non governmental provider|
    |3  |public – private partnership|
    |4  |public provider|
    |5  |other|

### Data Source

* Agency providing information on the provider (<code>agency_id</code>; recommended; string)  
  The agency that provides the information should provide its DEQAR ID. The ID can be consulted in the admin interface.

    *e.g. 1*  
    *e.g. 73*

* Source of information on the provider (<code>source_information</code>; recommended; string)  
  Link to databases where more information on the organization could be found.

    *e.g. World Higher*

## How to Provide Data

If you identify that providers are missing, please send us a spreadsheet with the required data.

Before sending data on a new providers, please check carefully that the providers is not yet listed in the [reference list of providers](https://admin.deqar.eu/reference/institutions). It is important to use the administrative interface to do so, as there are many institutions and few providers  recorded in DEQAR for which no reports have been uploaded yet. These are visible in the administrative interface, but not in the public interface; see also the section [Finding Existing Providers](#finding-existing-providers) above.

Please supply the providers data using the right template depending on the type of provider:

* For higher education institutions in countries covered by OrgReg/ETER:
     - [Open Document Format](files/Template_HEI_OrgReg.ods) (OpenOffice, LibreOffice, NeoOffice)
     - [Microsoft Excel format](files/Template_HEI_OrgReg.xlsx)
* For higher education institutions in other countries:
     - [Open Document Format](files/Template_HEI_lists.ods) (OpenOffice, LibreOffice, NeoOffice)
     - [Microsoft Excel format](files/Template_HEI_lists.xlsx)
* For alternative providers (irrespective of their location):
     - [Open Document Format](files/Template_AP_lists.ods) (OpenOffice, LibreOffice, NeoOffice)
     - [Microsoft Excel format](files/Template_AP_lists.xlsx)

You may save the spreadsheet in either format or as a CSV file. Send the filled spreadsheet to [deqar@eqar.eu](mailto:deqar@eqar.eu); the EQAR Secretariat will check the list shortly and return the original file with the newly generated DEQARINST IDs added.

