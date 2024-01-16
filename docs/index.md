DEQAR Documentation
===================

## About DEQAR

The Database of External Quality Assurance Reports (DEQAR) is maintained by the [European Quality Assurance Register for Higher Education (EQAR)](https://www.eqar.eu/). DEQAR enhances access to quality assurance reports and decisions on higher education providers and/or their educational programmes. The quality of the organisations/programmes is externally reviewed against the Standards and Guidelines for Quality Assurance in the European Higher Education Area (ESG), by an EQAR-registered agency.

The database is expected to satisfy the information needs of a broad range of users, including but not limited to:

* Recognition information centres (ENIC-NARICs)
* Recognition officers in higher education institutions
* Students
* Quality assurance agencies
* Ministry representatives and other national authorities
* Employers

The database also supports different types of activities (e.g. issuing digital credentials, recognition of degrees, mobility of students, portability of grants/loans etc.). Through this database, EQAR thus contributes to the transparency of external quality assurance in the European Higher Education Area.

### EU funding

The development and initial maintenance of DEQAR was financially supported by the Erasmus+ programme of the European Union.

The initial DEQAR project was selected for EU co-funding under Erasmus+ Key Action 3 - European Forward-Looking Cooperation Projects. It ran from November 2017 to October 2019. [More about the project and partners involved](https://www.eqar.eu/kb/projects/deqar-project/)

The DEQAR CONNECT project was selected for EU co-funding in 2020 and ran until June 2022. [More about DEQAR CONNECT and the partners involved](https://www.eqar.eu/kb/projects/deqar-connect/).

Currently, DEQAR is further developed and maintained, mainly through EQAR’s own budgets.

![Co-founded by the Erasmus+ programme of the European Union](img/LogosBeneficairesErasmus+RIGHT_EN_web.png)

## Ecosystem

All software components of DEQAR are open source and available on GitHub:

* [DEQAR backend](https://www.github.com/eqar/eqar_backend) - A [DRF](http://www.django-rest-framework.org/) application responsible for managing the data-model, providing API endpoints for submission, file uploads and the admin user interface.
* [DEQAR administrative interface](https://github.com/EQAR/deqar_frontend) - <https://admin.deqar.eu/> - A ReactJS frontend for registered agency users and EQAR staff to manage data in DEQAR.
* [DEQAR public user interface](https://github.com/EQAR/deqar_public_ui) - <https://www.deqar.eu/> - A section on the EQAR website, powered by WordPress and a custom theme, linking to the Web API of the DEQAR backend.

## Questions and bug reports

Despite thorough internal testing, bugs and errors may still occur. If you encounter any problem submitting data and/or files, please share these with us by email to <mailto:deqar@eqar.eu> or by opening an [issue on GitHub](https://github.com/EQAR/eqar_backend/issues). Please also include the CSV file/JSON data that caused the problem, so that the EQAR secretariat and developers can reproduce the error.

In case you are interested contributing to the codebase or you would like to share your thoughts and ideas, we welcome you to do so through the DEQAR [GitHub page](https://github.com/EQAR/eqar_backend)

## Terminology

In the present documentation, we use different keywords:

### Requirement levels

The documentation uses the definitions in [RFC 2119](https://tools.ietf.org/html/rfc2119), which is widely-used in internet standards. That is:

 - "**Must**" signals that the element (or cluster of elements) has to be provided; otherwise the record in question will be rejected.
 - "**Should**" signals that we highly recommend that the element (or cluster of elements) be provided, unless providing it would be impossible in the particular case or cause prohibitively large effort.
 - "**May**" signals that the element (or cluster of elements) is truly optional, and can be provided if applicable or if the agency feels it might be useful.

### Data types

The data types used in DEQAR follow the common definitions:

 - **String**: sequence of characters, digits, or symbols &ndash; always treated as text (e.g. `0034`; `institutional accreditation`; `1`)

 - **Date**: sequence of numbers pointing to a day and month within a calendar year (e.g. `2023-08-02`); where it is indicated so, the date format can be specified (e.g. see [report validity](https://docs.deqar.eu/report_data/#validity)), otherwise dates must be provided in the format `YYYY-MM-DD` (i.e. in date format `%Y-%m-%d`).

 - **Integer**: Numeric data type for numbers without fractions (e.g. `2`)

### Definitions

 - **Provider**: any actor that provides degree programmes, micro-credentials or other learning opportunities in terms of teaching, classes, learning materials, etc. This may include higher education institutions (public, private, academic, professional, preparatory, initial, continuing, adult, local, foreign, cross-border, European or international), as well as alternative providers, including employers, companies, social partners, NGOs, public authorities and others.
 - **Higher education institution** (**HEI**): an entity that has full degree awarding powers at higher education level (i.e. EQF levels 5 to 8; QF-EHEA cycle first to third) recognised by at least one national authority.
 - **Alternative provider**: an entity that provides learning opportunities at higher education level (i.e. EQF levels 5 to 8; QF-EHEA cycle first to third), but does not have full (recognised) degree awarding powers themselves[^1].
 - **Awarder**: the body that certifies the micro-credential. The awarding body may differ from the provider, e.g. in the case of partnerships, franchise.
 - **Programme**: learning provision that can lead to a full degree (traditional programmes offered by HEIs) or to another type of certificate (i.e. micro-credentials offered by HEIs or alternative providers). Whenever there is a difference, the handbook points to “programme leading to full degree” and “programme not leading to a full degree” (i.e. micro-credentials).
 - **Micro-credential**: a certified small volume of learning not leading to a full degree. Micro-credentials may be provided through a cooperation of different providers.
 - **Joint programme**: an integrated curriculum coordinated and offered jointly by different higher education institutions, and leading to double/multiple degrees or a joint degree.
 - **Joint degree**: a single document awarded by higher education institutions offering the joint programme and nationally acknowledged as the recognised award of the joint programme.
 - **Double/multiple degrees**: separate degrees awarded by higher education institutions offering the joint programme attesting the successful completion of this programme (if two degrees are awarded by two institutions, this is a ‘double degree’).
 - **QF-EHEA level**: expressed as a cycle defined in the overarching [Framework of Qualifications of the European Higher Education Area](https://www.ehea.info/page-qualification-frameworks) (QF-EHEA); when used for a programme, the indication of a level refers to the learning outcomes of the programme aligning with the generic learning outcomes as defined for the given cycle in the QF-EHEA.

### Entity relationship diagrams

The explanations of the data model are accompanied by entity relationship diagrams with the commonly-used [Crow's foot notation](https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model#Crow's_foot_notation). These illustrate the relationships between different entities and the cardinality of that relationship. The following example illustrates the four possible symbols:

```mermaid
erDiagram
    Artist ||--o{ Song : "performs"
    Person }|--o| School : "is current student of"
```

Read: every Artist may have zero, one or more Songs, while each Song is performed by exactly one Artist. A Person may be a current student of one School or not be a student of any School, but may not be a student of several Schools at once, while a School has one or more Persons as students.

[^1]: The use of terminology “alternative providers” varies between systems/countries. For example, in England (UK),  alternative providers are higher education providers who do not receive recurrent funding from Office for Students (previously HEFCE) or other public body and who are not further education colleges. The degree awarding status is not taken in consideration when defining the status in this system.
