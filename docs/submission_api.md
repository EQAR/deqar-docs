REST API is a convenient way for software developers to communicate with web
services via HTTP, the protocol used by the internet. Together with JSON it
provides an easy, straightforward and flexible means of exchanging data between
systems. With the possibility of sending complex request and response objects,
we can accept structured data and give immediate feedbacks (e.g. error checks,
warnings) about the submitted data as well as metadata enhancements (e.g. ETER
IDs on HEIs, when applicable; links to new records on the EQAR public interface,
etc.).

# API Endpoint

The address of the submission endpoint is:
[https://backend.deqar.eu/submissionapi/v1/submit/report](https://backend.deqar.eu/submissionapi/v1/submit/report)

This is the URL that you can use to make a POST request including the Submission
Request Object as JSON object or many objects as JSON array of objects in the
request body. In the submission draft we had originally planned to create
separate endpoints for individual and bulk submission requests, but in order to
make things easier for submitting agencies, we have created a single endpoint
that accepts single submission objects and arrays of objects as well.

# Authentication

Requests for submission to DEQAR are only accepted from registered users and
must therefore be identified. DEQAR API endpoints manage authentication using
API Tokens (through the so-called Bearer Authentication method2). Upon
registration, an API Token (which is basically a hash) is created for each user.
Sending this token in the Authorization header will authenticate the user in
place of a regular username and password. To get your authentication token you
can send a POST request to the following URL:

[https://backend.deqar.eu/accounts/get_token/](https://backend.deqar.eu/accounts/get_token/)

An example of obtaining a token using curl in command line:

```
curl -s -H "Content-Type: application/json" -XPOST https://https://backend.deqar.eu/accounts/get_token/ --data '{"username":"testuser","password":"testpassword"}'
```

The username is the agency’s acronym (in lower case, see reference list).
For the testing period, the password is the username followed by #2018.

Or for those who prefer to use the more user friendly httpie3 client:

```
http POST https://eqar-backend.herokuapp.com/accounts/get_token/ 'username=testuser' 'password=testpassword'
```

# Submission Request Object

The Submission Request Object is the JSON object or array of objects which is
the manifestation of a report or set of reports an agency wants to submit.
Fields names and accepted types are similar to those detailed in the Submission
Template spreadsheet.

The full definition of request and response objects can be find in OpenAPI format under:

[https://app.swaggerhub.com/apis/EQAR/SubmissionAPI/1.0.0](https://app.swaggerhub.com/apis/EQAR/SubmissionAPI/1.0.0)

# Submission of Files

Files (PDF versions of reports) can be submitted in two separate ways:

 - The submitted URLs will be harvested asynchronously upon successful submission.
 - Files can be submitted directly to a dedicated endpoint as part of a PUT request:
   `https://backend.deqar.eu/submissionapi/v1/submit/reportfile/<report_file_id>/<filename>`

   `report_file_id`: The id number of the Report File object available in the
response after successful submission. The `report_file_id` is contained in the response object of the successful report submission.
   `filename`: The name of the file that you will submit in this request.

# JSON Submission Request Object Examples

The examples below show how a Submission Request Object might look for different types of reports:

- [Institutional report](https://raw.githubusercontent.com/EQAR/eqar_backend/master/submissionapi/examples/institutional.json)
- [Programme report](https://raw.githubusercontent.com/EQAR/eqar_backend/master/submissionapi/examples/programme.json)
- [Institutional/Programme report](https://raw.githubusercontent.com/EQAR/eqar_backend/master/submissionapi/examples/institutional_programme.json)
- [Joint Programme report](https://raw.githubusercontent.com/EQAR/eqar_backend/master/submissionapi/examples/joint_programme.json)

