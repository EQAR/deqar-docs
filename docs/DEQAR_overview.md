Structural Overview
-------------------
EQAR’s data model has been designed around four main entities: registered quality assurance **Agencies**, higher education **Institutions**, educational **Programmes** associated with institutions, and external quality assurance **Reports**. 

[DEQAR High Level Data Model](img/DEQARPhysicalERDiagram_Design31_20-01-18_highlevel.jpg)

Registered agency users are invited to submit information on external quality assurance reports including information about the study programme concerned, if applicable. On the other hand, institutional information will largely be managed by EQAR based on data from ETER/OrgReg. Further information on the type of information to be collected and stored in DEQAR can be found in the [Operational Model](https://eqar.eu/fileadmin/eqar_internal/MD/MD6/Database_of_External_QA_Results_Report_Model_v3.pdf), section 5.3, page 36.

DEQAR has also included a **Country** entity, which contains information on the official external quality assurance regime in each DEQAR-related country---a country which either hosts an EQAR-registered agency or hosts an institution evaluated by a EQAR-registered agency.

[DEQAR High Level Data Model with Countries](img/DEQARPhysicalERDiagram_Design31_20-01-18_countryplain.jpg)

Functional Overview
-------------------
DEQAR supports three core activities:

- **Submission of data objects:** agencies submit objects and PDF files meeting defined criteria using one of three methods (individual records via webform; batch CSV file via webform; or as JSON via API).  
- **Administration of records:** data is ingested and records are created, stored and managed by EQAR staff and agencies over the longer term.
- **Search and discovery of information:** records are published on an public web interface for search, retrieval and export or download by end users.

more...

Role of Standards and Identifers 
--------------------------------

As DEQAR aggregates data from different sources, we face several challenges:

1. To keep the same data from different sources synchronised (e.g. the same institution may be described slightly differently by different agencies),
2. To try to avoid duplication, and
3. To identify already existing records for update if necessary.

To meet these challenges, the DEQAR data model uses standard values on various levels. Countries are identifed via the *ISO 3166-1 standard*; language data is accepted in *ISO 639-1* or *ISO 639-2/B* format.

DEQAR uses a set of standard identifiers which are provided by the system for each entity.  In several cases, we also allow agencies to provide their local identifiers for entities in order to ease their internal workflow.  Entities are identifed in the following ways:

| Entity      | Primary Identification     | Alternative Identification |
| ----------- | -------------------------- | -------------------------- |
| Agency      | agency acronym             | DEQAR Agency ID            |
| Institution | DEQARINST ID               | ETER ID, local identifier  |
| Programme   | local programme identifier | DEQAR Programme ID         |
| Reports     | local report identifier    | DEQAR Report ID            |

The agency responsible for the report must always be identified with any submission. The institution(s) should be identified when submitting a report if there is already a record for the institution in DEQAR. In the case of programmes and reports, we strongly encourage agencies to provide their locally stored identifiers with each new submission:
- For programmes, the first time an agency provides information on a programme to DEQAR, a local idenfier can be submitted along with information on the programme; the identifier can later be used by the agency for any report on the same programme.
- For reports, the agency can provide a local identifier with each new report submitted; the local identifier may be provided for later updates using JSON/API or CSV and may also help each agency to synchronise its local system with DEQAR.

In more details, each entity works as follows:
- **Agency:** Authentication is required before the submission and update of data and files. Thus, the agency responsible for each report can be identifed automatically by the system. In some cases, an agency may serve as a *proxy agency* for a *creating agency*, submitting and managing data on its behalf (as in the case of umbrella organizations). In this case, the creating agency’s unique acronym or DEQAR agency ID (which can be found in DEQAR's administrative interface) must be provided as the source of identification. Identification of the creating agency is required for each object when using CSV and JSON. 
- **Institution:** Institutions already in DEQAR should be identified in new report submissions using one of the following identfiers.  
    - *DEQARINST IDs:*  DEQAR automatically generates a so-called "DEQARINST IDs" for each institution record that is created in the system. Ideally, each registered agency will store the DEQARINST IDs for institutions treated in their reports.
    - *ETER IDs:*  DEQAR harvests records from the ETER/OrgReg database once a year.  These are the source many of DEQAR's institution records. The ETER ID If an ETER ID is available, no further data on the institution is required.
    - *Local identfiers:*  For institutions not in ETER but already in the DEQAR, a local Identif can be used.
    - *Other identification methods:*  If there is no ETER ID, DEQAR ID or the identifer does not produce a match, the website address of the institution will be used as an alternative means of identifcation and will be matched against the ETER list and data on already submitted institutions. This failing, the name of the institution in English or original language will be used. If the process produces no match with the ETER list or with existing HEI data, then the record will be fagged for checking by the EQAR secretariat. (If a record lacks an ETER ID, but a match is found among the ETER registered institutions, then the ETER ID can be included in the response.)
 All instituions  

- **Programme:** DEQAR will not sync data on programmes; however if a local or national identifer is provided, this will be saved and can serve as a primary identifer if further reports are submitted for the same programme later.

    another paragraph

- **Report:** Each report will receive an identifer generated by the DEQAR system. If an agency uses a local identifer for its reports, then this will be saved and can serve as the primary identifer for the purpose of resubmission.

DEQAR also assigns IDs to Agency 

DEQAR highly recommends the submission of local identifers for each submitted entity. These may come in handy when data must be updated via any of the batch
interfaces.

Use of Data from ETER/OrgReg
----------------------------

Historical Data
---------------

In the case of Agencies and Institutions, the system should record important
changes in the status of these entities (ex. name changes, changed activity or
status, physical relocation, etc.). Thus it is necessary to differentiate
between updates in data due to typographical or syntax errors, and
“substantial” updates, which will becomemight be considered as part of
an historic data trail. On web forms and on the submission API endpoints there
will be a possibility to indicate a change request. In this case, the
overwritten data will be stored as historical data (and can be queried). It
remains unclear whether the bulk ingest and CSV upload can support this feature;
it is under discussion.
