# Release Notes

This page summarises the main changes introduced by the release of **Submission API v2**.

## Breaking changes

The following changes are are not fully backwards-compatible:

### Required fields

Two programmes-related fields were designated to become required in the future, which is the case with API v2:

- Degree outcome (`programme[n].degree_outcome`)
- Programme Qualification Level according to the QF-EHEA (`programme[n].qf_ehea_level`)

This will ensure that all programmes/micro-credentials are formally classified systematically according to type and level. The level is already indicated for 95% of programmes in DEQAR.

**Implementation:** The two fields are required in the CSV file (with the field names mentioned above), the API, or the form.

### Separation of report creation and update (POST / PUT)

API v1 allows to either create or update a report by making a POST request to `/submissionapi/v1/submit/report`. Whether this will create or update a report depends on whether an existing DEQAR report ID or local_identifier are provided, and if they exist. The current design is not very clean, as the intention is only implicit and the request might lead to a different than the intended effect.

API v2 will clearly distinguish between creation (a POST request) and update (a PUT request) of a report. For updates, reports can still be identified either by their DEQAR report ID or the agency's local identifier provided at creation.

A creation request with a duplicate local identifier will lead to an error. Likewise, an update request will yield an error if the report does not yet exist. Hence, the intention of the request will be clear and it will either lead to the intended effect or an error. This is also in line with the HTTP protocol, where PUT is an idempotent method while POST is not.

To facilitate synchronisation we will also provide an additional endpoint (a GET request) that can be used to query whether a specific local identifier is already known in DEQAR.

**Implementation:** The changes are reflected in the [Swagger]({{ deqar.root }}/submissionapi/v2/swagger/) / [ReDoc]({{ deqar.root }}/submissionapi/v2/redoc/) documentation.  
Besides the separation, a new endpoint helps you check your report's local identifier against the DEQAR system.

### Only one report creation/update per request

API v1 allowed the submission of several reports in one HTTP request. This feature was rarely used, but created some difficulties. Very large requests sometimes lead to timeouts. More importantly, internal server errors in the middle of a package sometimes left the calling implementation without a response for the entire package.

The API v2 will only support the creation/update of a single report per request to make requests more stable and "atomic".

Implementations that currently submit packages of several reports should do the iteration over the package client-side and make separate requests.

When running bulk uploads/updates you might be requested to throttle request not to exceed a rate limit.

**Implementation:** The changes are reflected in the [Swagger]({{ deqar.root }}/submissionapi/v2/swagger/) / [ReDoc]({{ deqar.root }}/submissionapi/v2/redoc/) documentation.  
Currently for the test period we didn't introduce throttle. We will check how API requests influence performance.

### Institutions managed separately

While the API v1 allowed for it technically, the creation of institution records together with a submitted reports has been deprecated for several years already. This will be fully removed and reports can thus only be submitted for existing institutions.

Institutions are synced from OrgReg, additions beyond OrgReg can be requested manually.

Other providers can be requested for addition manually, too.

**Implementation:** Unnecessary fields were removed entirely form the v2 endpoints.

## Other changes

The following additional non-breaking changes are noteworthy:

### Activities & European Approach

Currently, one report belongs to one and only one ESG activity. This has sometimes led to intentional duplications, e.g. where two or more quality labels, represented by distinct ESG activities, where evaluated in a single procedure.

Moreover, there have been some instances where European Approach-aligned joint programme accreditations have been uploaded under another joint programme ESG activity.

Two options are under considerations:

- Introducing an additional (boolean) field indicating whether a report is a European Approach report. This would be required for all joint programme reports. That is, a European Approach could either be uploaded linked to the designated European Approach ESG activity, or under another activity but marked as European Approach.
- Enabling that one report is linked to several activities. That is, if necessary, a European Approach report could be linked to both the designated European Approach ESG activity as well as a "regular" joint programme activity. Moreover, this could be used for other cases, e.g. multiple labels.

One additional consideration is whether the same ESG activity could be linked to several agencies at once. Currently, where several agencies implement identical activities these are internally duplicated, i.e. they are two (or more) separate records with different IDs. Examples of this are:

- European Approach for QA of Joint Programmes (duplicated for dozens of agencies)
- Programme and system accreditation in Germany
- Spanish country-wide harmonised external QA frameworks, e.g. DOCENTIA

**Implementation:** The changes are reflected in the [Swagger]({{ deqar.root }}/submissionapi/v2/swagger/) / [ReDoc]({{ deqar.root }}/submissionapi/v2/redoc/) documentation. Now you will have a chance to submit more activities per report. This will affect submission API v2, CSV upload and the form as well. The new field structure in the API is:

```json
activities: [
	{
		id: "Identifier of the Agency ESG Activity",
		local_identifier: "Local identifier of the ESG Activity",
		agency: "Identifier or the acronym of the agency whose  
                 local identifier is used. If not provided, the 
                 agency of the report will be used.",
		group: "Identifier of the Agency ESG Activity Group"
	}
]
```

This also changes how CSV handles activities. So in the new version instead of using a single value, multiple values can be submitted:

```
activities[n].id, activities[n].local_identifier, activities[n].agency, activities[n].group
```

A new validation rule was also set up. If you select multiple agencies (one main agency and one or more contributing agencies), at least one activity per agency must be selected. In submission API v1, you can still use the old method to submit one activity per report.

If you select various types of activities (one institutional and one programme), the one with the most strict validation would be run. For example, if you assign an institutional activity and a joint programme one, your report should have more than one institution and at least one programme assigned.

As you see, a new field called group is included, reflecting the additional consideration. Now, every agency activity belongs to an Activity Group. This is the "common" aggregator of the same kind of agency activities. When you submit data, you have the chance to submit this Activity Group ID instead of the activity id. The system then checks and selects all the activities belonging to the specified group, assigned to the submitting and contributing agencies. 

### File upload

Currently, report files can be submitted as a URL or uploaded via a separate API endpoint.  
In addition, API v2 will allow submitting a file "inline" as a Base64-encoded string.

**Implementation:** The changes are reflected in the [Swagger]({{ deqar.root }}/submissionapi/v2/swagger/) / [ReDoc]({{ deqar.root }}/submissionapi/v2/redoc/) documentation.  
In the new submission API v2, you either submit your file with a URL, or you can embed it as a base64 string in the submission package. One of the two methods should be used. To make file management easier, there are separate endpoints available to add a new file to an existing report (POST), update an already submitted file (PUT), or remove a file from a report (DELETE), if there were more than one file submitted.

### Duplicates

Currently, DEQAR does not include an automated check for possible duplicate reports. (The recent large-scale duplicate check was a semi-automated, one-time exercise.)

In the future, a warning email might be sent to the agency concerned if a new report is created that appears to be a duplicate of an existing one.

**Implementation:** Once a report is submitted, the system runs an automated check on the newly submitted report. It checks if an existing report with the following matching values are present in the system:

```yaml
- valid_from
- valid_to
- decision
- activities
- institutions
- programme:
    - name
    - qf_ehea_level
    - workload_ects
```

If there are reports with the same values, a warning message will be sent for you, warning you about the possible duplication.

### Platforms

Following the expansion of DEQAR to include additional providers, the system will now support reports to be linked to one or more organisations acting as platforms in addition to the education provider(s). While the education provider is responsible for the educational content, the platform offers the technical or organizational framework necessary for delivering that education—such as an e-learning platform or a Learning Management System (LMS).

**Implementation:** A new field called platforms was added to the data model. You can use the same method to identify a platform with education providers. The system checks that in a report, an education provider can't act as a platform as well. 

## Timing

The new API v2 was finalised and launched on 31 March 2025.

Both APIs work by December 2025.

API v1 will be closed from January 2026.

