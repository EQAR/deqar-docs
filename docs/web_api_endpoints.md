# Endpoints

The base URL for the following endpoints is:

`https://backend.deqar.eu/webapi/v2`

The full definitions of the following endpoints and the response objects is available as [OpenAPI Specification 3.0](https://en.wikipedia.org/wiki/OpenAPI_Specification) at:

<https://backend.deqar.eu/webapi/v2/swagger/>

## Countries

These endpoints provide information on countries connected to agencies or institutions. For all countries part of the EHEA, country information includes a short profile of the national external quality assurance system for higher education.

| Method | Path                                            | Semantics                                                                                |
| ------ | ----------------------------------------------- | ---------------------------------------------------------------------------------------- |
| GET    | `/browse/countries/`                            | Full list of countries connected to agencies or institutions                             |
| GET    | `/browse/countries/{countryID}/`                | Returns a specific country record                                                        |
| GET    | `/browse/countries/by-agency-focus/{agencyID}/` | List of countries in which the specified agency has been operating                       |
| GET    | `/browse/countries/by-reports/`                 | List those countries with institutions for which QA reports have been submitted to DEQAR |

## Agencies

These endpoints provide information on EQAR-registered agencies. Please note that they cover both agencies that submit reports to DEQAR as well as those that do not.

| Method | Path                                        | Semantics                                         |
| ------ | ------------------------------------------- | ------------------------------------------------- |
| GET    | `/browse/agencies/`                         | Full list of EQAR-registered agencies             |
| GET    | `/browse/agencies/{agencyID}/`              | Returns a specific registered agency record       |
| GET    | `/browse/agencies/focusing-to/{countryID}/` | List agencies operating in the specified country  |
| GET    | `/browse/agencies/based-in/{countryID}/`    | List agencies based in the specified country      |
| GET    | `/browse/agencies/decisions/`               | EQAR decisions on agencies in chronological order |

## Institutions

These endpoints provide information on higher education institutions covered by QA results. Institutional information is managed by EQAR based on data harvested from ETER/OrgReg as well as participating agencies.

**Important:** The Web API lists **only institutions with at least one QA result**. To search the full list of institutions recorded in DEQAR (based on ETER/OrgReg and other sources), please use the [Connect API](institution_data.md#connect-api).

| Method | Path                                      | Semantics                                                         |
| ------ | ----------------------------------------- | ----------------------------------------------------------------- |
| GET    | `/browse/institutions/`                   | List or search institutions appearing in reports                  |
| GET    | `/browse/institutions/{institutionID}`    | Returns a specific institution record, identified by DEQARINST ID |
| GET    | `/browse/institutions/by-eter/{eter_id}/` | Specific institution record, identified by ETER ID instead        |
| GET    | `/browse/institutions/resources/`         | List known identifier resource tags (e.g. Eramus, EU-PIC, ...)    |
| GET    | `/browse/institutions/by-identifier/{resource}/{identifier}/` | Specific institution record, identified by any identifier known in DEQAR |

## Reports

These endpoints provide information on QA results concerning a particular institution.

| Method | Path | Semantics |
| ------ | -------------------------------------------------------------- | ---------------------------------------------------------------- |
| GET    | `/browse/reports/programme/by-institution/{institutionID}`     | List programme-level reports about the specified institution     |
| GET    | `/browse/reports/institutional/by-institution/{institutionID}` | List institutional-level reports about the specified institution |
| GET    | `/browse/reports/`                                             | List of reports, can be filtered by various criteria             |
| GET    | `/browse/reports/{id}/`                                        | Get details of a specific report                                 |

