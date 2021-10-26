# European Digital Credentials for Learning

European Digital Credentials for Learning are a recently launched standard for issuing education credentials (e.g. diplomas, transcripts of records, etc.) in a tamper-proof digital format, with authentication and verification checks built in. The standard was developed by the European Union.

DEQAR data can be loaded into the Europass Qualifications Dataset Register (QDR) on a per-country basis and then feed the Accreditation Database against which European Digital Credentials are verified.

**Your [national Europass centre](https://europa.eu/europass/en/national-europass-centres) or [EQF national coordination point](https://europa.eu/europass/en/implementation-european-qualifications-framework-eqf) are the authorised representatives who can access the QDR system and activate the link.**

## Prerequisites

 1. At least one **HEI that is interested to issue European Digital Credentials**.

    > *Why: proper testing is only possible based on an actual credential issued and by checking that accreditation validation passes.*

 2. **Correct data available in DEQAR**, at least for the HEIs that are going to issue credentials.

    > See <https://www.eqar.eu/qa-results/search/by-institution/> or <https://www.eqar.eu/qa-results/search/by-report/> (use filters to narrow down search by country)
    >
    >   - If data is missing, but HEIs/programmes have been accredited/evaluated/audited by an EQAR-registered agency (<https://www.eqar.eu/register/agencies/>), please contact that quality assurance agency and ask them to upload the reports to DEQAR.
    >
    >     Please bear in mind that only EQAR-registered agencies can upload reports in DEQAR
    >
    >   - In cases when data on quality assurance reports is incorrect, please contact the responsible agency.
    >
    >   - In cases when basic data for your institution(s) is not up to date, please contact EQAR at [aleksandra.zhivkovikj@eqar.eu](mailto:aleksandra.zhivkovikj@eqar.eu) and inform about the required changes

 3. External **quality assurance at institutional level**, e.g. institutional audit, system accreditation or similar.

    > *Why: unfortunately, support for programme accreditation is not available yet due to delays in updating the Europass QDR platform itself.*

 4. **EU/EEA membership and having a qualifications framework (NQF) referenced to European Qualifications Framework for Lifelong Learning (EQF)**.

    > *Why: European Digital Credentials can be issued by HEIs established in the EU+EEA only (because of the eIDAS regulation); the EU only accepts countries with a NQF referenced to the EQF to upload data to the QDR.*

## Prepare

**Step 1 - National authority**:

  - Check current QA reports in DEQAR and take up any issues with the responsible QAA or EQAR (see above)

**Step 2** (if needed) - **QA agency, EQAR**:

  - Fix data issues (e.g. missing reports, outdated HEI information etc.).

**Step 3 - National authority**:

  - Download [list of HEIs](https://www.eqar.eu/qa-results/download-data-sets/) and add missing EU VAT number or legal entity identifier (see eIDAS identifier) for the HEIs in your national system

    > *Why: VAT numbers or legal entity identifiers are used by Europass to correlate HEIs with accreditation records*
    >
    > **Please note**: DEQAR already has VAT numbers on file for a sizeable number of HEIs in the EU (see column *identifiers_all* in the list of HEIs), we only need identifiers of the missing ones if these should be included in the export.

  - If you have any additions, send back the list to EQAR at [colin.tueck@eqar.eu](mailto:colin.tueck@eqar.eu) and [aleksandra.zhivkovikj@eqar.eu](mailto:aleksandra.zhivkovikj@eqar.eu)

**Step 4 - EQAR**:

  - Record identifiers/VAT numbers in DEQAR, confirm that the system is "ready"

## Use

**Step 1 - National authority**:

Log into QDR at <https://europa.eu/europass/qdr/#/login>, create a new data set based on DEQAR with these parameters:

  - Type of data contained: **Accreditations**
  - Accreditation publishing scheme: **Accreditation metadata schema (2019)**
  - Namespace: **https://data.deqar.eu/**
  - Publishing method: **Hosted on your server - Automatic Update** (or Manual Update if you prefer)

Use the following download URL:

```
https://backend.deqar.eu/connectapi/v1/europass/accreditations/[ISO 3166 Alpha-3 Code, in small letters]
```

**Step 2 - HEI:**

  - Issue a digital (test) credential
  - Verify if accreditation check passes

Note down any obstacles and ideas and forward them to EQAR at [aleksandra.zhivkovikj@eqar.eu](mailto:aleksandra.zhivkovikj@eqar.eu)


