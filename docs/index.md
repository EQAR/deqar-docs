DEQAR is the Database of External Quality Assurance Results.

## About the project

![Co-founded by the Erasmus+ programme of the European Union](img/LogosBeneficairesErasmus+RIGHT_EN_web.png)

The Database of External Quality Assurance Reports (DEQAR) project was selected for EU co-funding under Erasmus+ Key Action 3 - European Forward-Looking Cooperation Projects.

The main aim of the DEQAR project is the development of a database that will enhance access to reports and decisions on higher education institutions/programmes externally reviewed against the ESG, by an EQAR-registered agency.

The database is expected to enable a broad range of users, including but not limited to:

* Recognition information centres (ENIC-NARICs)
* Recognition officers in higher education institutions
* Students
* Quality assurance agencies
* Ministry representatives and other national authorities

to satisfy their information needs and support different types of decisions (e.g. recognition of degrees, mobility of students, portability of grants/loans). A first public preview version of the database will be available in May 2018.

Through this database EQAR will contribute to the transparency of external quality assurance in the European Higher Education Area.

Read more about the DEQAR project and partners involved at: <http://www.deqar.eu/>

## DEQAR EcoSystem

* DEQAR backend - A [DRF](http://www.django-rest-framework.org/) applicaiton responsible for managing the data-model, providing API endpoints for submission, file uploads and the admin user interface. - [DEQAR backend on GitHub](https://www.github.com/eqar/eqar_backend)
* DEQAR administrative interface - <https://admin.deqar.eu/> - A ReactJS frontend for end-users and EQAR staff to manage data in DEQAR. - [DEQAR frontend on GitHub](https://www.github.com/eqar/eqar_frontend)
* Public website

## Questions and bug reports

No matter how thorough our internal testing, bugs and errors may still occur. If you encounter any problem submitting data and/or files, please share these with us through the [DEQAR Trello board](https://trello.com/b/cogOpUeh/deqar-board) under Questions and Answer list, where you can add your questions/issue as a new card, or comment on an existing card if somebody else already raised the same question.

Please use one of the predefined labels for new cards: technical CSV, technical API, or technical web interface. Please also add to your card the CSV file/JSON data that caused the problem, so that the EQAR secretariat and developers can reproduce the error.

In case you are interested contributing to the codebase or you would like to share your thoughts and ideas, we welcome you to do so through the project's [GitHub page](https://github.com/EQAR/eqar_backend)

## Terminology

In the present documentation, we use key words according to the definitions in [RFC 2119](https://tools.ietf.org/html/rfc2119), which is widely-used in internet standards. That is:

 - **Must** signals that the element (or cluster of elements) has to be provided; otherwise the record in question will be rejected.
 - **Should** signals that we highly recommend that the element (or cluster of elements) be provided, unless providing it would be impossible in the particular case or cause prohibitively large effort.
 - **May** signasl that the element (or cluster of elements) is truly optional, and can be provided if applicable or if the agency feels it might be useful.
