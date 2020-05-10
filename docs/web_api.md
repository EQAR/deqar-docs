# Search and Discovery

## Public web interface

The DEQAR public web interface is freely accessible at:

<https://www.deqar.eu/>

The current DEQAR web interface is the initial stable release. We are always looking for ways to improve the interface. You can make suggestions via the survey integrated on all DEQAR pages or send us an email at [deqar@eqar.eu](https://mailto:deqar@eqar.eu).

## Web API

REST API is a convenient way for software developers to communicate with web services via HTTP, the protocol used by the internet. Together with JSON it provides an easy, straightforward and flexible means of exchanging data between systems.

The DEQAR Web API allows to search and discover QA reports, and to embed such functionality in own websites or applications.

The [public DEQAR web interface](#public-web-interface) uses the same API.

### Get Access

The DEQAR Web API is available to all interested parties, in line with the [DEQAR Terms and Conditions](https://www.eqar.eu/legal-notice/deqar/).

EQAR-registered agencies have access to the Web API automatically, using their [credentials for the DEQAR administrative interface](data_submission.md#webform) and the Submission API.

For all others, use of the API is free, but subject to prior registration in order to avoid excessive resource consumption and to ensure that the information is not used in a way that jeopardises the objectives of DEQAR.

Access may be requested by simple email to [deqar@eqar.eu](mailto:deqar@eqar.eu). We will grant access to any individual or organisation unless we have reasons to believe that the information might be abused, misrepresented or used in violation of the DEQAR Terms and Conditions.

After registration you will obtain a username and password combination for the Web API. We will publish a list of registered users with access to the Web API.

### Authentication

DEQAR API endpoints manage authentication using API Tokens (through the so-called Bearer Authentication method). Upon registration, an API Token (which is basically a hash) is created for each user. Sending this token in the Authorization header will authenticate the user in place of a regular username and password. To get your authentication token you can send a POST request to the following URL:

<https://backend.deqar.eu/accounts/get_token/>

An example of obtaining a token using curl in command line:

```sh
curl -s -H "Content-Type: application/json" -XPOST https://backend.deqar.eu/accounts/get_token/ --data '{"username":"testuser","password":"testpassword"}'
```

Or for those who prefer to use the more user friendly httpie3 client:

```sh
http POST https://backend.deqar.eu/accounts/get_token/ 'username=testuser' 'password=testpassword'
```

### API Endpoints

The base URL for the following endpoints is:

`https://backend.deqar.eu/webapi/v2`

The full definitions of the following endpoints and the response objects is available as [OpenAPI Specification 3.0](https://en.wikipedia.org/wiki/OpenAPI_Specification) at:

<https://backend.deqar.eu/webapi/v2/swagger/>

#### Countries

These endpoints provide information on countries connected to agencies or institutions. For all countries part of the EHEA, country information includes a short profile of the national external quality assurance system for higher education.

| Method | Path                                            | Semantics                                                                                |
| ------ | ----------------------------------------------- | ---------------------------------------------------------------------------------------- |
| GET    | `/browse/countries/`                            | Full list of countries connected to agencies or institutions                             |
| GET    | `/browse/countries/{countryID}/`                | Returns a specific country record                                                        |
| GET    | `/browse/countries/by-agency-focus/{agencyID}/` | List of countries in which the specified agency has been operating                       |
| GET    | `/browse/countries/by-reports/`                 | List those countries with institutions for which QA reports have been submitted to DEQAR |

#### Agencies

These endpoints provide information on EQAR-registered agencies. Please note that they cover both agencies that submit reports to DEQAR as well as those that do not.

| Method | Path                                        | Semantics                                         |
| ------ | ------------------------------------------- | ------------------------------------------------- |
| GET    | `/browse/agencies/`                         | Full list of EQAR-registered agencies             |
| GET    | `/browse/agencies/{agencyID}/`              | Returns a specific registered agency record       |
| GET    | `/browse/agencies/focusing-to/{countryID}/` | List agencies operating in the specified country  |
| GET    | `/browse/agencies/based-in/{countryID}/`    | List agencies based in the specified country      |
| GET    | `/browse/agencies/decisions/`               | EQAR decisions on agencies in chronological order |

#### 

#### Institutions

These endpoints provide information on higher education institutions covered by QA results. Institutional information is managed by EQAR based on data harvested from ETER/OrgReg as well as participating agencies.

| Method | Path                                      | Semantics                                                         |
| ------ | ----------------------------------------- | ----------------------------------------------------------------- |
| GET    | `/browse/institutions/`                   | List or search institutions appearing in reports                  |
| GET    | `/browse/institutions/{institutionID}`    | Returns a specific institution record, identified by DEQARINST ID |
| GET    | `/browse/institutions/by-eter/{eter_id}/` | Specific institution record, identified by ETER ID instead        |

#### Reports

These endpoints provide information on QA results concerning a particular institution.

| Method | Path | Semantics |
| ------ | -------------------------------------------------------------- | ---------------------------------------------------------------- |
| GET    | `/browse/reports/programme/by-institution/{institutionID}`     | List programme-level reports about the specified institution     |
| GET    | `/browse/reports/institutional/by-institution/{institutionID}` | List institutional-level reports about the specified institution |
| GET    | `/browse/reports/`                                             | List of reports, can be filtered by various criteria             |
| GET    | `/browse/reports/{id}/`                                        | Get details of a specific report                                 |

### Examples

In the following, we present two examples of how the DEQAR Web API might be used in practice. You will first retrieve your user's authentication token [as described above](#authentication) or [from the Admin UI](https://admin.deqar.eu/my-profile).

#### Example #1: Find an institution's accredited programmes

In this example, the user needs to know whether a Master degree in Automotive Engineering from RWTH Aachen University is accredited. Let's assume the user enters `aachen` into a search box. The client makes a `GET` request to:

```sh
curl -s -H "Authorization: Bearer ******" "https://backend.deqar.eu/webapi/v2/browse/institutions/" --get --data query=aachen
```

We'll get 4 matching results:

```json
{
  "count": 4,
  "results": [
    {
      "country": [
        "Germany"
      ],
      "qf_ehea_level": [
        "third cycle",
        "first cycle",
        "second cycle"
      ],
      "place": [
        {
          "country": "Germany",
          "lat": null,
          "long": null,
          "city": "Aachen"
        }
      ],
      "eter_id": "DE0069",
      "hierarchical_relationships": {
        "includes": [],
        "part_of": []
      },
      "id": "382",
      "score": 31.92261,
      "deqar_id": "DEQARINST0382",
      "name_official_display": "RWTH Aachen",
      "name_primary": "Aachen University",
      "website_link": "http://www.rwth-aachen.de",
      "name_select_display": "Aachen University (DE0069)",
      "name_sort": "AachenUniversity"
    },
    ((...))
  ],
  "facets": {
    ((...))
    "facet_fields": {
      "reports_agencies": [
        "AAQ",
        1,
        "ACQUIN",
        1,
        "AHPGS",
        2,
        "AQAS",
        3,
        "ASIIN",
        2,
        "FIBAA",
        3,
        "ZEvA",
        1
      ],
      "qf_ehea_level_facet": [
        "first cycle",
        4,
        "second cycle",
        4,
        "third cycle",
        1
      ],
      "status_facet": [
        "part of obligatory EQA system",
        4,
        "voluntary",
        2
      ],
      "country_facet": [
        "Germany",
        4
      ],
      ((...))
    }
  }
}
```

Now we can fetch the quality assurance reports on the institution in question, using its ID `382`.

This is done separately for the institutional and programme level. For the institutional level, the client makes a request to:

```sh
curl -s -H "Authorization: Bearer ******" "https://backend.deqar.eu/webapi/v2/browse/reports/institutional/by-institution/382/"
```

Result:

```json
{
  "count": 1,
  "next": null,
  "previous": null,
  "results": [
    {
      "id": 47914,
      "agency_name": "Swiss Agency of Accreditation and Quality Assurance",
      "agency_acronym": "AAQ",
      "agency_id": 3,
      "agency_url": "https://backend.deqar.eu/webapi/v1/browse/agencies/3/",
      "agency_esg_activity": "System accreditation in Germany",
      "agency_esg_activity_type": "institutional",
      "name": "System accreditation",
      "institutions": [
        {
          "id": 382,
          "deqar_id": "DEQARINST0382",
          "name_primary": "Aachen University",
          "website_link": "http://www.rwth-aachen.de"
        }
      ],
      "institutions_hierarchical": [],
      "institutions_historical": [],
      "programmes": [],
      "report_valid": true,
      "valid_from": "2018-09-14",
      "valid_to": "2024-09-30",
      "status": "part of obligatory EQA system",
      "decision": "positive",
      "report_files": [
        {
          "file_display_name": "",
          "file": null,
          "languages": [
            "German"
          ]
        }
      ],
      "report_links": [
        {
          "link_display_name": "View report record on agency site",
          "link": "https://antrag.akkreditierungsrat.de/akkrstudiengaenge/74812917-e23c-4f7a-a425-a5ca72ad6493/"
        }
      ],
      "local_identifier": "7c0a1e10-0334-4cd8-a1a9-61dc901ffe98",
      "other_comment": null,
      "flag": "none"
    }
  ]
}
```

We see that RWTH Aachen has a system accreditation by AAQ. But let's assume the degree we are concerned about was awarded in 2017, whereas the system accreditation is valid from September 2018 only.

To get information on programme level external QA we need to make a further GET request to:

```sh
curl -s -H "Authorization: Bearer ******" "https://backend.deqar.eu/webapi/v2/browse/reports/programme/by-institution/382/"
```

We see that there are 331 programme accreditation reports and can browse through the result pages with custom limit and offset parameters, e.g.:

```sh
curl -s -H "Authorization: Bearer ******" "https://backend.deqar.eu/webapi/v2/browse/reports/programme/by-institution/382/" --get --data limit=20 --data offset=100
```

We can now identify the programme we were looking for. While the programme accreditation is no longer valid (it was superseded by the system accreditation we saw above), it was valid at the time relevant for us, i.e. in 2017 when the degree was issued:

```json
{
    "count": 331,
    "next": "https://backend.deqar.eu/webapi/v2/browse/reports/programme/by-institution/382/?limit=20&offset=120",
    "previous": "https://backend.deqar.eu/webapi/v2/browse/reports/programme/by-institution/382/?limit=20&offset=80",
    "results": [
        {
            "id": 25106,
            "agency_name": "Accreditation Agency for Study Programmes of Engineering, Information Science, Natural Sciences and Mathematics",
            "agency_acronym": "ASIIN",
            "agency_id": 19,
            "agency_url": "https://backend.deqar.eu/webapi/v1/browse/agencies/19/",
            "agency_esg_activity": "Programme accreditation",
            "agency_esg_activity_type": "programme",
            "name": "Programme accreditation",
            "institutions": [
                {
                    "id": 382,
                    "deqar_id": "DEQARINST0382",
                    "name_primary": "Aachen University",
                    "website_link": "http://www.rwth-aachen.de"
                }
            ],
            "institutions_hierarchical": [],
            "institutions_historical": [],
            "programmes": [
                {
                    "id": 42791,
                    "name_primary": "Automotive Engineering",
                    "programme_names": [
                        {
                            "name": "Automotive Engineering",
                            "name_is_primary": true,
                            "qualification": "Master"
                        }
                    ],
                    "programme_identifiers": [
                        {
                            "identifier": "e036d81b-cd3c-3ac7-15f7-5c2fdd01db0c",
                            "agency": "ASIIN - Accreditation Agency for Study Programmes of Engineering, Information Science, Natural Sciences and Mathematics",
                            "resource": "local identifier"
                        }
                    ],
                    "nqf_level": "",
                    "qf_ehea_level": "second cycle",
                    "countries": []
                }
            ],
            "report_valid": false,
            "valid_from": "2013-09-27",
            "valid_to": "2019-09-30",
            "status": "part of obligatory EQA system",
            "decision": "positive with conditions or restrictions",
            "report_files": [
                {
                    "file_display_name": "Akkreditierungsbericht_RWTH_Aachen_Ma_Automotive_Engineering_2013-09-27.pdf",
                    "file": "https://backend.deqar.eu/reports/ASIIN/20190826_1647_Akkreditierungsbericht_RWTH_Aachen_Ma_Automotive_Engineering_2013-09-27.pdf",
                    "languages": [
                        "German"
                    ]
                }
            ],
            "report_links": [
                {
                    "link_display_name": "View report record on agency site",
                    "link": "https://antrag.akkreditierungsrat.de/akkrstudiengaenge/e036d81b-cd3c-3ac7-15f7-5c2fdd01db0c/"
                }
            ],
            "local_identifier": "6ea3a64c-925d-d733-a2b3-5f8444e007e8",
            "other_comment": "",
            "flag": "none"
        },
        ((...))
    ]
}
```

#### Example #2: cross-border reports by a specific agency

In the second example, the end user needs to look for evaluations carried out by IEP in North Macedonia.

The report browsing endpoint allows to search for reports directly (i.e. not via institutions) and provides a number of search/filter facets. In the example, we want the reports ordered by the calculated validity date (that is, the explicit validity date or 6 years from the report date).

The client makes a GET request to:

```sh
curl -s -H "Authorization: Bearer ******" "https://backend.deqar.eu/webapi/v2/browse/reports/" --get --data agency=IEP --data country=North+Macedonia --data ordering=-valid_to_calculated
```

The result shows that there are seven reports:

```json
{
    "count": 7,
    "results": [
        {
            "country": [
                "North Macedonia"
            ],
            "agency_name": "Institutional Evaluation Programme",
            "programmes": [],
            "id": "3929",
            "agency_esg_activity_type": "institutional",
            "report_files": [
                {
                    "languages": [
                        "English"
                    ],
                    "file": "/reports/IEP/20180924_1056_iep%20mk_seeu%20report_final.pdf",
                    "file_display_name": "Evaluation report"
                }
            ],
            "agency_esg_activity": "Institutional evaluation",
            "institutions": [
                {
                    "id": 1709,
                    "website_link": "http://www.seeu.edu.mk/mk",
                    "deqar_id": "DEQARINST1709",
                    "name_primary": "South East European University - Tetovo"
                }
            ],
            "valid_from": "2018-01-01T00:00:00Z",
            "date_created": "2018-09-24T10:56:21.384Z",
            "score": 1.0,
            "agency_acronym": "IEP",
            "valid_to_calculated": "2023-01-01T00:00:00Z",
            "report_links": [],
            "date_updated": "2018-09-24T10:56:21.384Z",
            "flag_level": "none",
            "status": "voluntary",
            "decision": "not applicable"
        },
        ((...))
    ]
}
```

The list includes most information on the reports already. The full details of the report can be retrieved from:

```sh
curl -s -H "Authorization: Bearer ******" "https://backend.deqar.eu/webapi/v2/browse/reports/3929/"
```

In the example:

```json
{
    "id": 3929,
    "agency_name": "Institutional Evaluation Programme",
    "agency_acronym": "IEP",
    "agency_id": 31,
    "agency_url": "https://backend.deqar.eu/webapi/v1/browse/agencies/31/",
    "agency_esg_activity": "Institutional evaluation",
    "agency_esg_activity_type": "institutional",
    "name": "Institutional evaluation",
    "institutions": [
        {
            "id": 1709,
            "deqar_id": "DEQARINST1709",
            "name_primary": "South East European University - Tetovo",
            "website_link": "http://www.seeu.edu.mk/mk"
        }
    ],
    "institutions_hierarchical": [],
    "institutions_historical": [],
    "programmes": [],
    "report_valid": true,
    "valid_from": "2018-01-01",
    "valid_to": null,
    "status": "voluntary",
    "decision": "not applicable",
    "report_files": [
        {
            "file_display_name": "Evaluation report",
            "file": "https://backend.deqar.eu/reports/IEP/20180924_1056_iep%20mk_seeu%20report_final.pdf",
            "languages": [
                "English"
            ]
        }
    ],
    "report_links": [],
    "local_identifier": null,
    "other_comment": "",
    "flag": "none"
}
```

