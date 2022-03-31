# Examples

In the following, we present two examples of how the DEQAR Web API might be used in practice. You will first retrieve your user's authentication token [as described above](#authentication) or [from the Admin UI](https://admin.deqar.eu/my-profile).

## Example #1: Find an institution's accredited programmes

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

## Example #2: cross-border reports by a specific agency

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

## Example #3: use other institutional identifiers

In this example, a user looks up an institution based on the SCHAC identifier.

The client makes a first GET request to receive the list of known identifier types:

```sh
curl -s -H "Authorization: Bearer ******" "https://backend.deqar.eu/webapi/v2/browse/institutions/resources/"
```

The result shows that there are seven reports:

```json
[
    "AD-national",
    "BA-national",
    "BG-ETER.BAS.NATID",
    "BY-national",
    "CZ-ETER.BAS.NATID",
    "DE-ETER.BAS.NATID",
    "DE-HRK",
    "DID-EBSI",
    "DK-ETER.BAS.NATID",
    "ELIAS.HS_ID",
    "Erasmus",
    "Erasmus-Charter",
    "EU-PIC",
    "EU-VAT",
    "FI-ETER.BAS.NATID",
    "FR-ETER.BAS.NATID",
    "GB-ETER.BAS.NATID",
    "GE-national",
    "HR-Mozvag",
    "HU-ETER.BAS.NATID",
    "IE-ETER.BAS.NATID",
    "IT-ETER.BAS.NATID",
    "KZ-national",
    "local identifier",
    "LT-ETER.BAS.NATID",
    "LV-ETER.BAS.NATID",
    "MD-national",
    "PL-ETER.BAS.NATID",
    "PT-ETER.BAS.NATID",
    "RO-ETER.BAS.NATID",
    "SCHAC",
    "SE-ETER.BAS.NATID",
    "SI-ETER.BAS.NATID",
    "UA-national"
]
```

These resource tags can then be used in a request for a specific institution record:

```sh
curl -s -H "Authorization: Bearer ******" "https://backend.deqar.eu/webapi/v2/browse/institutions/by-identifier/SCHAC/urv.cat"
```

In the example, this returns (data abridged):

```json
{
    "closure_date": null,
    "countries": [
        {
            "city": "Tarragona",
            "country": {
                "...": "...",
                "iso_3166_alpha2": "ES",
                "iso_3166_alpha3": "ESP",
                "name_english": "Spain"
            },
            "country_source": "ETER",
            "country_valid_from": "2014-01-01",
            "country_valid_to": null,
            "country_verified": true,
            "lat": 41.122694,
            "long": 1.249866
        }
    ],
    "eter": "ES0022 - Universitat Rovira i Virgili",
    "founding_date": "1992-01-01",
    "hierarchical_relationships": {
        "includes": [
            {
                "...": "..."
            },
            {
                "...": "..."
            }
        ],
        "part_of": []
    },
    "historical_data": [],
    "historical_relationships": [],
    "id": 792,
    "identifiers": [
        {
            "agency": null,
            "identifier": "E  TARRAGO01",
            "identifier_valid_from": "1992-01-01",
            "identifier_valid_to": null,
            "resource": "Erasmus"
        },
        {
            "agency": null,
            "identifier": "E10208977",
            "identifier_valid_from": "1992-01-01",
            "identifier_valid_to": null,
            "resource": "Erasmus-Charter"
        },
        {
            "agency": null,
            "identifier": "urv.cat",
            "identifier_valid_from": "1992-01-01",
            "identifier_valid_to": null,
            "resource": "SCHAC"
        },
        {
            "agency": null,
            "identifier": "did:ebsi:ziBBPgHRMxmPaKmW1TCm9Cj",
            "identifier_valid_from": "2022-01-16",
            "identifier_valid_to": null,
            "resource": "DID-EBSI"
        },
        {
            "agency": null,
            "identifier": "999880560",
            "identifier_valid_from": "1992-01-01",
            "identifier_valid_to": null,
            "resource": "EU-PIC"
        },
        {
            "agency": null,
            "identifier": "ESQ9350003A",
            "identifier_valid_from": "1992-01-01",
            "identifier_valid_to": null,
            "resource": "EU-VAT"
        }
    ],
    "names": [
        {
            "acronym": "URV",
            "name_english": "Rovira i Virgili University",
            "name_official": "Universitat Rovira i Virgili",
            "name_official_transliterated": "",
            "name_source_note": "OrgReg-2020-CHARES0022-1",
            "name_valid_to": null,
            "name_versions": []
        }
    ],
    "qf_ehea_levels": [
        {
            "qf_ehea_level": "first cycle",
            "qf_ehea_level_source": "ETER",
            "qf_ehea_level_source_note": "",
            "qf_ehea_level_valid_from": "2014-01-01",
            "qf_ehea_level_valid_to": null
        },
        {
            "qf_ehea_level": "second cycle",
            "qf_ehea_level_source": "ETER",
            "qf_ehea_level_source_note": "",
            "qf_ehea_level_valid_from": "2014-01-01",
            "qf_ehea_level_valid_to": null
        },
        {
            "qf_ehea_level": "third cycle",
            "qf_ehea_level_source": "ETER",
            "qf_ehea_level_source_note": "",
            "qf_ehea_level_valid_from": "2014-01-01",
            "qf_ehea_level_valid_to": null
        }
    ],
    "website_link": "http://www.urv.cat"
}
```

