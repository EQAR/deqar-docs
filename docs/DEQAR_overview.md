Structural Overview
-------------------
EQAR’s data model has been designed around four main entities: registered quality assurance **Agencies**, higher education **Institutions**, educational **Programmes** associated with institutions, and external quality assurance **Reports**. 

![DEQAR High Level Data Model](img/DEQARPhysicalERDiagram_Design31_20-01-18_highlevel.jpg =200x)


Registered agency users are invited to submit information on external quality assurance reports including information about the study programme concerned, if applicable. On the other hand, institutional information will largely be managed by EQAR based on data from ETER/OrgReg. Further information on the type of information to be collected and stored in DEQAR can be found in the [Operational Model](https://eqar.eu/fileadmin/eqar_internal/MD/MD6/Database_of_External_QA_Results_Report_Model_v3.pdf), section 5.3, page 36.

DEQAR has also included a **Country** entity, which contains information on the official external quality assurance regime in each DEQAR-related country---a country which either hosts an EQAR-registered agency or hosts an institution evaluated by a EQAR-registered agency.

![DEQAR High Level Data Model with Countries](img/DEQARPhysicalERDiagram_Design31_20-01-18_countryplain.jpg)

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

To meet these challenges, the DEQAR data model uses standard values at various levels. **Countries** are identifed via the *ISO 3166-1 standard*; **Language** data is accepted in *ISO 639-1* or *ISO 639-2/B* format.

DEQAR uses a set of standard identifiers which are provided by the system for each entity.  In several cases, we also allow agencies to provide their local or national identifiers for entities in order to ease their internal workflows.  Entities are identifed in the following ways:

| Entity      | Recommended Identification | Alternative Identification |
| ----------- | -------------------------- | -------------------------- |
| Agency      | agency acronym             | DEQAR Agency ID            |
| Institution | DEQARINST ID               | ETER ID, local identifier  |
| Programme   | local programme identifier | DEQAR Programme ID         |
| Reports     | local report identifier    | DEQAR Report ID            |

### Identifying Entities

The agency responsible for the report must be identified with any submission. An identifier should also be provided for each institution *in the case that a record for the institution already exists in DEQAR.* This allows the system to establish a direct link with the existing record. If the institution record does not exist, data must be provided instead. 

In the case of programmes and reports, agencies are encouraged to provide local identifer. We strongly urge agencies to provide their local report identifiers with each new submission of data:

- For programmes, the first time an agency provides information on a programme to DEQAR, a local (or national) idenfier can be submitted along with data on the programme; the identifier can later be used by the agency for any report on the same programme.
- For reports, the agency can provide a local identifier with each new report submitted; the local identifier may be provided for later updates using CSV or JSON and may also help each agency to synchronise its local system with DEQAR.

In more detail, the identification of each entity works as follows:

- **Agency:** Authentication is required before the submission and update of data and files. Thus, the agency responsible for each report can be identifed automatically by the system. In some cases, an agency may serve as a *proxy agency* for a *creating agency*, submitting and managing data on its behalf (as in the case of umbrella organizations). In this case, the creating agency’s unique acronym or DEQAR agency ID (which can be found in DEQAR's administrative interface) must be provided as the source of identification. For this reason, identification of the creating agency is required for each object when using CSV and JSON. 

- **Institution:** Institutions already described in DEQAR should be identified in report submissions using one of several identfiers. This allows the system to automatically link report data to existing institution records. 

    - DEQARINST IDs: DEQAR automatically generates a so-called "DEQARINST ID" for each institution record that is created in the system. These can be found through the administrative interface. (They are also be returned to the agency as part of the response object after each successful submission.) Ideally, each registered agency will store the DEQARINST IDs for institutions treated in their reports. These are recommended for use in each submission.
    
    - ETER IDs: DEQAR harvests records from the ETER/OrgReg database once a year. These records are the source many of DEQAR's institution records. The ETER ID for these institutions can be found through the administrative interface. The ETER IDs may be stored and used by agencies for submission as an alternative to the DEQARINST IDs.
    
    - Local/national identfiers: Agencies may also create and store local or national identifiers for institutions. If the agency provides a list of local or national idenfiers *in advance* to the EQAR secretariat, then these can be used for submission as an alternative to the DEQARINST IDs.
    
    - Other identification methods: If an agency cannot locate an existing institution record in DEQAR (and therefore cannot provide either the DEQARINST ID, ETER ID or local identifer), then they will need to provide institution data as the source of an entirely new record.  
    Before creating a new record, the system checks to confirm that the record does not already exist. It checks the website URL provided as well as the official and English names against all instituion records in the system.  If these do not produce a match, then a new record is created. For this reason, it is recommended that all agencies provide the root domain name (in its shortest form) of the institution website. 
    
    *Note: agencies should provide a single identifier; if more than one is provided, the DEQARINST ID will be used to establish the linkage.* 
    
- **Programme:** DEQAR will not synchronise data on programmes; however if a local or national identifer is provided at the time of submission, this will be stored in the system. The agency can use the programme identifier if it would like to simply re-use the existing programme data for subsequent reports.

- **Report:** We strongly recommend that agencies provide a local identifier with each report submitted. This will allow for subsequent updates to the record and will ease synchronisation with each agency's local system.  
    Report local identifiers will be stored and can serve to identify record for updates/resubmission. DEQAR will also automatically generate a DEQAR ID for each newly submitted report; this will be returned to agencies as part of the response object. The DEQAR ID can be used for updates/resubmission as an alternative to local identifiers.

### Other Identifiers

DEQAR also assigns DEQAR IDs to each agency's **Activities**. These identifiers, which can be found through the administrative interface, may be used instead of the activity name (string values) to identify the report activity in each CSV or JSON object. Alternatively, an agency may wish to use its own local activity identifiers, which the agency can supply through the administrative interface and then used for submission.  Only one identifier should be provided for each assigned activity.    

Finally, DEQAR provides DEQAR IDs for standard values used for **Report Status** and **Report Decision**. [link??] These can be provided instead of the equivalent string values in each CSV or JSON object.

Use of Data from ETER/OrgReg
----------------------------

DEQAR harvests records from ETER/OrgReg on an annual basis. These records serve as DEQAR's base set of records on European institutions. DEQAR stores the following ETER data on institutions: official name, English name, country, city, latitude/longitude. As a rule, DEQAR keeps ETER data stable and unchanged between harvests; alternative names and agencies' local identifiers [(see above)](https://docs.deqar.eu/DEQAR_overview/#identifying-entities) can be added by agencies through the administative interface. The EQAR secretariat also reserves the right to adapt ETER records based on the information that we receive through agencies and other sources. Added information and updates are carried through to records from subsequent harvests.

Historical Data
---------------

In the case of Agencies and Institutions, the system should record important changes in the status of these entities (ex. name changes, changed activity or status, physical relocation, etc.). Thus it is necessary to differentiate between updates in data due to typographical or syntax errors, and
“substantial” updates, which will becomemight be considered as part of
an historic data trail. On web forms and on the submission API endpoints there
will be a possibility to indicate a change request. In this case, the
overwritten data will be stored as historical data (and can be queried). It
remains unclear whether the bulk ingest and CSV upload can support this feature;
it is under discussion.
