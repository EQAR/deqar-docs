## Public web interface

The DEQAR public web interface is freely accessible at:

<http://eqar.demo.slik.eu/qa-results/>

**This is a provisional preview**, it will be replaced by <https://www.deqar.eu/> when launched to the public.

## Web API

REST API is a convenient way for software developers to communicate with web services via HTTP, the protocol used by the internet. Together with JSON it provides an easy, straightforward and flexible means of exchanging data between systems.

The DEQAR Web API allows to search and discover QA reports, and to embed such functionality in own websites or applications.

The [public DEQAR web interface](public_web.md) uses the same API.

### Access

The DEQAR Web API is available to all interested parties, in line with the DEQAR Terms and Conditions.

EQAR-registered agencies have access to the Web API automatically, using their credentials for the DEQAR administrative interface and the Submission API.

For all others, use of the API is free, but subject to prior registration in order to avoid excessive resource consumption and to ensure that the information is not used in a way that jeopardises the objectives of DEQAR.

Access may be requested by simple email to [deqar@eqar.eu](mailto:deqar@eqar.eu). We will grant access to any individual or organisation unless we have reasons to believe that the information might be abused, misrepresented or used in violation of the DEQAR Terms and Conditions.

After registration you will obtain a username and password combination for the Web API. We will publish a list of registered users with access to the Web API.

### Authentication

DEQAR API endpoints manage authentication using API Tokens (through the so-called Bearer Authentication method). Upon registration, an API Token (which is basically a hash) is created for each user. Sending this token in the Authorization header will authenticate the user in place of a regular username and password. To get your authentication token you
can send a POST request to the following URL:

[https://backend.deqar.eu/accounts/get_token/](https://backend.deqar.eu/accounts/get_token/)

An example of obtaining a token using curl in command line:

```
curl -s -H "Content-Type: application/json" -XPOST https://backend.deqar.eu/accounts/get_token/ --data '{"username":"testuser","password":"testpassword"}'
```

Or for those who prefer to use the more user friendly httpie3 client:

```sh
http POST https://backend.deqar.eu/accounts/get_token/ 'username=testuser' 'password=testpassword'
```

### API Endpoints

The base URL for the following endpoints is:

`https://backend.deqar.eu/webapi/v1`

The full definitions of the following endpoints and the response objects is available as [OpenAPI Specification 3.0](https://en.wikipedia.org/wiki/OpenAPI_Specification) at:

<https://app.swaggerhub.com/apis/EQAR/WebAPI/1.0.0#/>

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

| Method | Path                                        | Semantics                                        |
| ------ | ------------------------------------------- | ------------------------------------------------ |
| GET    | `/browse/agencies/`                         | Full list of EQAR-registered agencies            |
| GET    | `/browse/agencies/{agencyID}/`              | Returns a specific registered agency record      |
| GET    | `/browse/agencies/focusing-to/{countryID}/` | List agencies operating in the specified country |
| GET    | `/browse/agencies/based-in/{countryID}/`    | List agencies based in the specified country     |

#### Institutions

These endpoints provide information on higher education institutions covered by QA results. Institutional information is managed by EQAR based on data harvested from ETER/OrgReg as well as participating agencies.

| Method | Path                                   | Semantics                                        |
| ------ | -------------------------------------- | ------------------------------------------------ |
| GET    | `/browse/institutions/`                | List or search institutions appearing in reports |
| GET    | `/browse/institutions/{institutionID}` | Returns a specific institution record            |

#### Reports

These endpoints provide information on QA results concerning a particular institution.

| Method | Path                                                           | Semantics                                                                                |
| ------ | -------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| GET    | `/browse/reports/programme/by-institution/{institutionID}`     | List programme-level reports about the specified institution                             |
| GET    | `/browse/reports/institutional/by-institution/{institutionID}` | List institutional-level reports about the specified institution                         |

