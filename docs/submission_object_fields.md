### agency

The report creator agency.

** required:** yes   
** one or many:** many   
** type: ** string   
** accepted values: ** Agency DEQAR ID; Agency Acronym

JSON examples:

```javascript
{
    "agency": "ACQUIN"
}
```
```javascript
{
    "agency": "18"
}
```
CSV examples: 

| agency | 
| ------ |
| ACQUIN |

| agency | 
| ------ |
| 18 |

Validation:

* The system tries to identify a valid Agency record in DEQAR.   
* The system checks if you are eligible to submit report to this agency.   

Error messages:

* This field is required.
* Please provide valid Agency DEQAR ID.
* Please provide valid Agency Acronym.
* You can't submit data to this Agency.

### local_identifier

The local identifier of the Report.

** required:** no   
** one or many:** one   
** type: ** string   
** accepted values: ** any string value

JSON example:

```javascript
{
    "local_identifier": "QAA1153-March15"
}
```

CSV example: 

| local_identifier | 
| ------ |
| ACQUINQAA1153-March15 |

Validation:

* The system checks if there were reports submitted with this local identifier.
* **IMPORANT!** - If a match is found for the same local identifier then the submission is treated like as an update, so all incoming data will overwrite the existing report data. Therefore local identifier is recommended to be unique.  


