DEQAR Documentation
===================

## About DEQAR

The Database of External Quality Assurance Reports (DEQAR) is maintained by the [European Quality Assurance Register for Higher Education (EQAR)](https://www.eqar.eu/). DEQAR enhances access to quality assurance reports and decisions on higher education institutions/programmes externally reviewed against the ESG, by an EQAR-registered agency.

The database is expected to enable a broad range of users, including but not limited to:

* Recognition information centres (ENIC-NARICs)
* Recognition officers in higher education institutions
* Students
* Quality assurance agencies
* Ministry representatives and other national authorities

to satisfy their information needs and support different types of decisions (e.g. recognition of degrees, mobility of students, portability of grants/loans). Through this database EQAR thus contributes to the transparency of external quality assurance in the European Higher Education Area.

### EU funding

The development and maintenance of DEQAR was/is financially supported by the Erasmus+ programme of the European Union.

The initial DEQAR project was selected for EU co-funding under Erasmus+ Key Action 3 - European Forward-Looking Cooperation Projects. It ran from November 2017 to October 2019. [More about the project and partners involved](https://www.eqar.eu/kb/projects/deqar-project/)

The DEQAR CONNECT project was selected for EU co-funding in 2020 and will run until February 2022. [More about DEQAR CONNECT and the partners involved](https://www.eqar.eu/kb/projects/deqar-connect/)

![Co-founded by the Erasmus+ programme of the European Union](img/LogosBeneficairesErasmus+RIGHT_EN_web.png)

## Ecosystem

All software components of DEQAR are open source and available on GitHub:

* [DEQAR backend](https://www.github.com/eqar/eqar_backend) - A [DRF](http://www.django-rest-framework.org/) applicaiton responsible for managing the data-model, providing API endpoints for submission, file uploads and the admin user interface.
* [DEQAR administrative interface](https://github.com/EQAR/deqar_frontend) - <https://admin.deqar.eu/> - A ReactJS frontend for registered agency users and EQAR staff to manage data in DEQAR.
* [DEQAR public user interface](https://github.com/EQAR/deqar_public_ui) - <https://www.deqar.eu/> - A section of the EQAR website, powered by WordPress and a custom theme, linking to the Web API of the DEQAR backend.

## Questions and bug reports

No matter how thorough our internal testing, bugs and errors may still occur. If you encounter any problem submitting data and/or files, please share these with us by email to <mailto:deqar@eqar.eu>, by opening an issue on GitHub or through the [DEQAR CONNECT Trello board](https://trello.com/b/ADhRNeK3/deqar-connect). Please also include the CSV file/JSON data that caused the problem, so that the EQAR secretariat and developers can reproduce the error.

In case you are interested contributing to the codebase or you would like to share your thoughts and ideas, we welcome you to do so through the project's [GitHub page](https://github.com/EQAR/eqar_backend)

## Terminology

In the present documentation, we use key words according to the definitions in [RFC 2119](https://tools.ietf.org/html/rfc2119), which is widely-used in internet standards. That is:

 - **Must** signals that the element (or cluster of elements) has to be provided; otherwise the record in question will be rejected.
 - **Should** signals that we highly recommend that the element (or cluster of elements) be provided, unless providing it would be impossible in the particular case or cause prohibitively large effort.
 - **May** signals that the element (or cluster of elements) is truly optional, and can be provided if applicable or if the agency feels it might be useful.
