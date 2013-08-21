The Learning Registry provides RESTful services to access metadata and paradata about educational resources.  The guidance below is intended to help you write software that will use the Learning Registry’s services to consume metadata and paradata.

## Harvesting Records

The harvest service is the recommended service to use when getting started (other services that can be used are obtain and slice).  The harvest listrecords verb returns (in batches of 100 documents) records within an optional specific time/date range.  Both GET and POST methods are supported.  The GET method is shown below.

GET /harvest/listrecords?from=<date>&until=<date>&resumption_token=<token>

Example: https://node01.public.learningregistry.net/harvest/listrecords

Results are returned as an array of JSON.  The main elements of the result object are:
* “OK”: boolean // T if successful
* “error”: “string” // only present if NOT OK describing error
* “responseDate”: “string” // timestamp
* “request”: {} // object containing request
* “listrecords”: [] // array of records
* “resumption_token”: “string” // flow control resumption token, NULL if end

[Insert code guidance for harvesting and dealing with resumption tokens]

## Parsing Records

Each record in the Learning Registry is based on the resource data description data model.  The primary elements in the data model are:
* “resource_data”: “string” // describes the resource itself (metadata or paradata).
* “resource_locator”: “string” // URL of the resource

The “resource_data” comes in different forms that are described by the following elements of the resource data description data model:
* “resource_data_type”: “string” // vocabulary of types [“metadata”, “paradata”, …]
* “payload_schema_format”: “string” // schema MIME type

While there are many payload_schema_formats that could be encountered, it is important to be familiar with the [common data schema formats](https://github.com/LearningRegistry/LearningRegistry/wiki/Common-Data-Schema-Formats-in-Learning-Registry) that are found in the Learning Registry.

[Insert code guidance for parsing recognized patterns robustly]