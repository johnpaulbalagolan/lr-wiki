Access Services: Learning Registry Technical Specification V AS:0.50.1
======================================================================

See the [Change Log](#change-log) for links to prior stable versions.

Major changes and additions from the prior version (0.24.0) are marked with ▲.

Significant deletions use ~~strikethrough text~~.

Features to be deprecated in a future version are indicated with ▼.

This document is part of one or more versions of the
[Learning Registry Technical Specification \<../Technical\_Spec/index\>]{role="doc"}.
It may contain links to other parts of the Specification. These links
may link to the most recent version of a part, not to the version of the
part that corresponds to this version of this part. Go to the
appropriate version of the Specification that links to this version of
this part, and follow the links there to the referenced part to find the
version of the part that corresponds to this version of this part.

This document is part of the
[Learning Registry Technical Specification \<../Technical\_Spec/index\>]{role="doc"}.
It describes the basic Learning Registry services used to access (pull)
resource documents from a distribution network.

This document is not standalone. The reader should be familiar with
other parts of the specification, including, but not limited to:

-   [General Matter \<../General\_Matter/index\>]{role="doc"}, including
    Licenses, Notation, Versioning, Glossary, References
-   [Resource Distribution Network Model \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
-   [Resource Data Data Models \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
-   [Identity, Trust, Authentication, Security \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"}
-   [Data Model and API Attributes and Behaviors \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
-   [Other Services \<../Services\_and\_APIs/index\>]{role="doc"}
    including
    [Distribution \<../Distribution\_Services/index\>]{role="doc"},
    [Publish \<../Publish\_Services/index\>]{role="doc"},
    [Broker \<../Broker\_Services/index\>]{role="doc"},
    [Management/Administration/Discovery \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}
-   [Learning Registry Operations \<../Operations/index\>]{role="doc"}

In particular, the reader needs to be aware that specific criteria for
services and APIs are presented in the
[Data Model and API Attributes and Behaviors \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
part, the
[Resource Distribution Network Model \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
part describes the network model, the
[Resource Data Data Models \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
part describes the model of published data and the
[Identity, Trust, Authentication, Security \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"}
part describes security requirements.

Resource Data Access Services {#Resource Data Access Services}
-----------------------------

Access services are used to pull resource data from the network. They
are used by external access edge nodes to obtain one or more resource
data description documents for "off network" processing. These services
MAY be used to access individual resource data description documents by
document ID or collations of all resource data description documents for
each unique resource. Future drafts or versions of this specification
MAY define additional resource data access services.

*NB*: The services do not currently define a specific process to find or
maintain all resource data description documents in a collation for a
specific resource locator, i.e., for a unique resource identifier. A
future version of the specification MAY define additional resource data
document types that maintain collation descriptions.

### Basic Obtain Service {#Basic Obtain Service}

The basic obtain service pulls an instance of a resource data
description document (or a set of documents) directly from a node on a
resource distribution network. It is the most basic, direct mechanism to
access resource data.

For the list of supplied request IDs, the service SHALL return the
corresponding resource data description documents from the node's
resource data description document database where they exist.
Optionally, the service MAY return just the document IDs and not full
documents. The results SHALL be aligned 1:1 with the IDs in the request.

If the request ID is not provided, the service MAY return all or a
service-determined subset of the resource data description documents.
The service description SHALL specify how the service implementation
responds to an ALL request (returning ALL, none, or a limited subset).
When returning a subset of the documents, the service SHOULD return the
documents with the most recent ▲node\_timestamp values.

*NB*: To support buffering, the service MAY return a smaller number of
results than it advertises.

Open Question: What does *most* *recent* mean when requesting via
resource ID.

Request IDs MAY be:

-   the document ID for a resource data description document. The
    service SHALL return the single resource data description document
    that matches the ID.
-   a unique resource identifier, e.g., the resource locator. The
    service SHALL return all resource data description documents for the
    specified resource.

If a specified ID does no resolve to a resource data description
document in the node's resource data description document database, the
result object returned SHALL be NULL.

The internal storage of a resource data description document MAY include
additional key-value pairs not defined in this specification. The
service MAY return all stored key-value pairs, or only the key-value
pairs defined in this specification for the resource data description
document. The service document SHALL indicate if the returned documents
are limited to the specification-defined key-value pairs only or if all
stored key-value pairs are returned.

[▲The service description SHALL specify if the service implementation supports flow control, i.e., pagination of results\--one page of results is returned at a time.
If flow control is supported, the service MAY return partial results set when called.
If the results returned is not the complete set of requested documents or IDs, the service SHALL return a resumption token.
The service SHALL determine how large of a set to return per call.
NB: The service MAY determine the size of results set on a per call basis.]{role="changes"}

[▲In response to the next call to the service from the same client that includes the resumption token, the service MAY return another portion of the results set, including a new resumption token if the response is still not the complete set of results.
When the results set is complete, the service SHALL return a resumption token with a value of NULL.
The service SHALL NOT return a resumption token if it does not support flow control or if the entire results set is returned on the first call.]{role="changes"}

[▲When flow control is supported, the \*next\* request MAY include the resumption token.
If the request includes a resumption token, the service SHOULD attempt to return the next portion of the results.
When the client begins making requests with a resumption token, only the most recent token MAY be used in the call.
Any client call without a resumption token invalidates the current resumption token.
Including a resumption token on the first call SHALL return a flow control error.]{role="changes"}

[▲The service SHALL determine how long to maintain state to support flow control and how many clients it can support simultaneously.
If the service cannot return the next portion of the results, it SHALL return a flow control error.]{role="changes"}

[▲To support integrity of results sets, if the set of documents stored at the node changes in a way such that the sequence of calls will not return all the requested results, e.g., documents are added between calls to the service, the service SHALL return a flow control error.]{role="changes"}

[\*▲NB\*: To support communication error recovery, the client MAY repeatedly call the service using the same resumption token.]{role="changes"}

*NB*: The format of the resumption token is not specified; the service
MAY use any format or encoding needed to support flow control.

*NB*: There are no restrictions on number of requested documents or in
the total size of the HTTP message or response. An implementation SHALL
indicate any size limits in the service description.

*NB*: The default is that IDs are for resources, not documents.

*NB*: The default is to return full resource data description documents,
not just IDs.

[\*▲NB\*: By default, flow control is not supported.]{role="changes"}

*NB*: The request of *by* *document* or *by* *resource* applies to the
entire list of request IDs.

*NB*: The mechanism of matching a supplied request ID to a resource
locator is not specified.

*NB*: The process currently does not handle attachments.

*NB*: Including a list of IDs and requesting IDs only as a result is
effectively a NO-OP, the results match the input.

*ToDo*: Extend to produce (log) a usage record of the obtain.

#### API

#### Basic Obtain

> // Obtain the resource data description documents for each supplied ID
>
> IF by\_doc\_ID AND by\_resource\_ID
>
> > THEN
> >
> > > error // only one can be true
> > >
> > > EXIT
>
> [▲IF resumption\_token present and NOT flow\_control]{role="changes"}
>
> > [THEN]{role="changes"}
> >
> > > [error  // flow control error]{role="changes"}
> > >
> > > [EXIT]{role="changes"}
>
> [IF resumption\_token present AND]{role="changes"}
>
> > [(resumption\_token DOES NOT MATCH saved state for this this client]{role="changes"}
> >
> > > [// test must recognize that client did not get last results and is re-requesting last set]{role="changes"}
> > >
> > > [// or client may be requesting next set]{role="changes"}
> > >
> > > [OR]{role="changes"}
> >
> > [server has lost state)]{role="changes"}
> >
> > > [THEN]{role="changes"}
> > >
> > > > [error  // flow control error]{role="changes"}
> > > >
> > > > [EXIT]{role="changes"}
>
> IF by\_doc\_ID
>
> > IF request\_ID not specified
> >
> > > THEN set doc\_IDs in request\_ID array
> > >
> > > > // based on the values in the service description (none, ALL,
> > > > subset)
> >
> > FOR EACH request\_ID
> >
> > > [▲IF flow\_control AND resumption\_token is present]{role="changes"}
> > >
> > > > [THEN SKIP if entry is prior to resumption point]{role="changes"}
> > >
> > > [IF results object exceeds flow control or results size limits]{role="changes"}
> > >
> > > > [THEN EXIT LOOP]{role="changes"}
> >
> > Put the request\_ID in the results object
> >
> > IF ids\_only THEN SKIP
> >
> > GET the corresponding *resource* *data* *description* document
> >
> > > IF Successful
> > >
> > > > THEN PUT the *resource* *data* *description* document in the
> > > > results object
> > > >
> > > > > // all stored key-value pairs or only those defined in the
> > > > > spec
> > > > >
> > > > > // as defined in the service description
> > > >
> > > > ELSE PUT NULL in the results object
> >
> > [▲IF Loop ended normally]{role="changes"}
> >
> > > [IF flow\_control and resumption token is present]{role="changes"}
> > >
> > > > [THEN return NULL resumption\_token in results]{role="changes"}
> > > >
> > > > [ELSE omit resumption\_token from results]{role="changes"}
> >
> > [IF Loop exited because of flow control or results size limits]{role="changes"}
> >
> > > [IF flow\_control]{role="changes"}
> > >
> > > > [THEN return appropriate resumption\_token]{role="changes"}
>
> IF by\_resource\_ID
>
> > IF request\_ID not specified
> >
> > > THEN set unique\_resource\_locations in request\_ID array
> > >
> > > > // based on the values in the service description (none, ALL,
> > > > subset)
> >
> > FOR EACH request\_ID
> >
> > > [▲IF flow\_control AND resumption\_token is present]{role="changes"}
> > >
> > > > [THEN SKIP if entry is prior to resumption point]{role="changes"}
> > >
> > > [IF results object exceeds flow control or results size limits]{role="changes"}
> > >
> > > > [THEN EXIT LOOP]{role="changes"}
> > >
> > > IF NOT ids\_only
> > >
> > > > THEN FIND the collation of resource data description documents
> > > >
> > > > WHERE resource\_locator MATCHES supplied request\_ID
> > >
> > > IF Successful
> > >
> > > > PUT the request ID in the results object
> > > >
> > > > IF ids\_only THEN SKIP
> > > >
> > > > FOR EACH *resource data description* document
> > > >
> > > > GET the corresponding *resource data description* document
> > > >
> > > > > PUT the *resource data description* document in the results
> > > > > object
> > > > >
> > > > > > // all stored key-value pairs or only those defined in the
> > > > > > spec
> > > > > >
> > > > > > // as defined in the service description
> > >
> > > ELSE PUT NULL in the results object
> >
> > [▲IF Loop ended normally]{role="changes"}
> >
> > > [IF flow\_control and resumption token is present]{role="changes"}
> > >
> > > > [THEN return NULL resumption\_token in results]{role="changes"}
> > >
> > > [ELSE omit resumption\_token from results]{role="changes"}
> >
> > [IF Loop exited because of flow control or results size limits]{role="changes"}
> >
> > > [IF flow\_control]{role="changes"}
> > >
> > > > [THEN return appropriate resumption\_token]{role="changes"}

#### Service Description

::: {.sourcecode}
javascript

{

> \"doc\_type\": \"service\_description\",
>
> \"doc\_version\": \"0.20.0\",
>
> \"doc\_scope\": \"node\",
>
> \"active\": true,
>
> \"service\_id\": \"\<uniqueid\>\",
>
> \"service\_type\": \"access\",
>
> \"service\_name\": \"Basic Obtain\",
>
> \"service\_description\": \"Service to access individual resource
> description documents given a list of one or more document IDs or
> resource URL\",
>
> \"service\_version\": \"0.21.0\",
>
> \"service\_endpoint\": \"\<node-service-endpoint-URL\>\",
>
> \"service\_auth\":
>
> :   // service authentication and authorization descriptions
>
> {
>
> > \"service\_authz\": \[\"\<authvalue\>\"\],
> >
> > :   // authz values for the service
> >
> > \"service\_key\": \< T / F \> ,
> >
> > :   // does service use an access key
> >
> > \"service\_https\": \< T / F \>
> >
> > :   // does service require https
> >
> },
>
> \"service\_data\":
>
> {
>
> > \"id\_limit\": integer,
> >
> > :   // specify the maximum number of IDs
> >
> >     // the service will return when requesting ALL
> >
> >     // 0 means ALL is not a valid request
> >
> >     // optional, return ALL if missing
> >
> > \"doc\_limit\": integer,
> >
> > :   // specify the maximum number of documents
> >
> >     // the service will return when requesting ALL
> >
> >     // 0 means ALL is not a valid request
> >
> >     // optional, return ALL if missing
> >
> > \"spec\_kv\_only\": boolean,
> >
> > :   // T to return only spec-defined key-value pairs
> >
> >     // F to return all stored key-value pairs
> >
> >     // optional, default F
> >
> > \"flow\_control\": boolean
> >
> > :   // ▲ T if the implementation supports flow control
> >
> >     // F if flow control is not supported
> >
> >     // optional, default F, no flow control
> >
> }

}
:::

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
provided. Appropriate values for the service\_data elements SHALL be
provided. The descriptive values (service\_name, service\_description)
MAY be changed from what is specified herein.

### Basic Harvest Service {#Basic Harvest Service}

The basic harvest service can be used by an external agent to connect to
a node to harvest (pull) the resource data description documents held by
the node. The service is patterned after the OAI-PMH specification. The
service is designed to be extended to support full OAI-PMH--compliant
harvesting.

The service can harvest the native JSON encoded metadata or paradata
resource data, i.e., it harvests the resource data in the native format,
not XML-encoded Dublin Core metadata or some other metadata
dissemination. Harvest is done by resource data description document ID
or by resource ID, i.e., by resource locator. Set-based harvesting is
not currently supported. Flow control is not currently supported.
OAI-PMH verbs are included directly in the HTTP path (rather than as an
argument to provide a more RESTful API). Both GET and POST encoding of
requests are supported.

The internal JSON storage of a resource data description document MAY
include additional key-value pairs not defined in this specification.
The service MAY return all stored key-value pairs, or only the key-value
pairs defined in this specification for the resource data description
document. The service document SHALL indicate if the returned documents
are limited to the specification-defined key-value pairs only or if all
stored key-value pairs are returned.

*OAI-PMH* *Extension*: IDs MAY be:

-   the document ID for a resource data description document. The
    service SHALL return the single resource data description document
    that matches the ID.
-   a unique resource identifier, e.g., the resource locator. The
    service SHALL return all resource data description documents for the
    specified resource that satisfy other harvest criteria.

Mapping of Learning Registry Basic Harvest to OAI-PMH Concepts

  ------------------------ ----------------------------------------------
  **Native OAI-PMH         **Learning Regisry Harvest API Concept**
  Concept**

  Repository (harvest API  Node Resource Data Description Document
  end point)               Database

  Resource (something that Resource
  has records)

  Item (something in the   Resource Data, e.g., an individual Resource
  repository for which a   Data Description Document or a collation of
  record can be            Resource Data Description Documents for a
  disseminated)            unique Resource

  Record (dissemination    Resource Data Description Document, JSON
  output)                  Encoded

  Item Identifier (URI)    Resource Data Description Document ID
                           orResouce ID/Resource Locator

  Metadata Format          Resource Data Description Document JSON Object
                           Schema

  Set                      *Sets* *for* *organizing* *resource* *data*
                           *are* *not* *defined* *in* *this* *version*
                           *of* *the* *specification*

  GetRecord Verb           \<nodelURL\>harvest/getrecord

  ListRecords Verb         \<nodelURL\>harvest/listrecords

  ListIdentifiers Verb     \<nodelURL\>harvest/listidentifiers

  Identify Verb            \<nodelURL\>harvest/identify

  ListMetadataFormats Verb \<nodelURL\>harvest/listmetadataformats

  ListSets Verb            \<nodelURL\>harvest/listsets
  ------------------------ ----------------------------------------------

Each of the six harvest verbs are specified separately. The Service
Description document SHALL apply to the entire API.

The network node SHALL maintain a value for the earliest publication
time for documents harvestable from the node (earliestDatestamp).
Time-based harvesting MAY request harvest for documents published,
updated or deleted after that time. The node MAY maintain documents with
an earlier timestamp, but these documents SHALL NOT be accessible via
harvest. The granularity for access via the timestamp MAY be days or
seconds. The granularity of the timestamp SHALL be stored in the service
description document.

*NB*: The actual timestamp MAY have a finer granularity.

*NB*: All times are UTC 0.

#### Get Record

The Get Record verb returns the resource data description documents for
the specified resource data document ID or resource ID. If the request
ID is a resource data description document ID, the service SHALL return
the single resource data description document that matches the ID. If
the request ID is a unique resource identifier, e.g., the resource
locator, the service SHALL return all resource data description
documents for the specified resource. The API only returns JSON.
Different metadata formats cannot be specified. The service SHALL return
complete resource data description documents.

*NB*: The process currently does not handle attachments.

*NB*: The default is that IDs are for resources, not documents.

*ToDo*: Extend to produce (log) a usage record of the harvest.

##### API

##### Basic Harvest: GetRecord

> // Return the resource data description documents for the supplied ID
>
> Build results object
>
> > responseDate := time of report // time/date encoding
> >
> > request := // the API request
> >
> > > {\"verb\": \"getrecord\", // the literal \"getrecord\"
> > >
> > > \"identifier\": ID, // request ID
> > >
> > > \"by\_doc\_ID\": boolean, // request value
> > >
> > > \"by\_resource\_ID\": boolean, // request value
> > >
> > > \"HTTP\_request\": \"string\" // the HTTP request as a string
> > >
> > > }
> >
> > IF request\_ID not supplied // return error
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := "badArgument\"
> > > >
> > > > EXIT
> >
> > IF by\_doc\_ID AND by\_resource\_ID
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"badArgument\" // only one can be true
> > > >
> > > > EXIT
> >
> > IF by\_resource\_ID // get the list of documents otherwise it's just
> > the requested ID
> >
> > > THEN
> > >
> > > > FIND the collation of resource data description document IDs
> > > >
> > > > WHERE resource\_locator MATCHES request \<identifier\>
> >
> > FOR EACH resource data description document ID
> >
> > GET the corresponding *resource data description* document
> >
> > IF successful
> >
> > > THEN
> > >
> > > > // return resource data
> > > >
> > > > // header
> > > >
> > > > [▲datestamp := node\_timestamp from the \*resource\* \*data\* \*description\*]{role="changes"}
> > > >
> > > > identifier := resource data description document ID
> > > >
> > > > IF delete\_data\_policy \<\> \"no\"
> > > >
> > > > > AND the *resource* *data* *description* document has been
> > > > > deleted
> > > > >
> > > > > THEN status := \"deleted\"
> > > >
> > > > // resource data
> > > >
> > > > PUT the *resource* *data* *description* document in the results
> > > > object
> > > >
> > > > > // all stored key-value pairs or only those defined in the
> > > > > spec
> > > > >
> > > > > // as defined in the service description
> > > >
> > > > OK := TRUE
> > >
> > > ELSE // not found error
> > >
> > > > PUT NULL in the results object
> > > >
> > > > OK := FALSE
> > > >
> > > > error := \"idDoesNotExist\"
>
> TRANSFORM results to specified CONTENT-TYPE

#### List Records

The List Records verb returns the resource data description documents
for document added to the node within a specified time/date range. The
API only returns JSON. The service SHALL return complete resource data
description documents. Different metadata formats cannot be specified.
Flow control is not currently supported. Set-based harvesting is not
currently supported. Return of attachments is not currently supported.

*NB*: List records does not support access by resource locator.
Documents may only be accessed by document ID.

*ToDo*: Extend to produce (log) a usage record of the harvest.

##### API

##### Basic Harvest: ListRecords

> // Return the resource data description documents for the specified
> time range
>
> Build results object
>
> > responseDate := time of report // time/date encoding
> >
> > request := // the API request
> >
> > {
> >
> > :   \"verb\": \"listrecords\", // the literal \"listrecords\"
> >
> >     \"from\": \"string\", // specified start of harvest time/date
> >     range
> >
> >     \"until\": \"string\", // specified end of harvest time/date
> >     range
> >
> >     \"HTTP\_request\": \"string\" // the HTTP request as a string
> >
> > }
> >
> > IF from \> until // return error
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"badArgument\"
> > > >
> > > > EXIT
> >
> > IF granularity of from time \<\> granularity of until time // return
> > error
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"badArgument\"
> > > >
> > > > EXIT
> >
> > IF granularity of from time \< service granularity // request is for
> > seconds, service instance only supports days (not seconds)
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"badArgument\"
> > > >
> > > > EXIT
> >
> > IF from not specified THEN from := earliest timestamp
> >
> > IF until not specified THEN until := latest timestamp
> >
> > FOR EACH *resource* *data* *description* document
> >
> > > IF from \<= [▲node\_timestamp]{role="changes"} from the *resource*
> > > *data* *description* document
> > >
> > > > \<= until // timestamp inclusive in \[from:until\] range
> > >
> > > THEN
> > >
> > > > // return header for resource data
> > > >
> > > > [▲datestamp := node\_timestamp from the resource\* \*data\* \*description\*]{role="changes"}
> > > >
> > > > identifier := resource data description document ID
> > > >
> > > > IF the delete\_data\_policy \<\> \"no\"
> > > >
> > > > > AND the r\*esource\* *data* *description* document has been
> > > > > deleted
> > > > >
> > > > > THEN status := \"deleted\"
> > > >
> > > > // return the resource data
> > > >
> > > > PUT the r\*esource\* *data* *description* document in the
> > > > results object
> >
> > IF listrecords array is empty
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"noRecordsMatch\"
> > >
> > > ELSE
> > >
> > > > OK := TRUE
>
> TRANSFORM results to specified CONTENT-TYPE

#### List Identifiers

The List Identifiers verb returns the OAI-PMH header information from
the resource data description documents for the specified resource data
document IDs within a specified time/date range. The API only returns
JSON. Different metadata formats cannot be specified. Flow control is
not currently supported. Set-based harvesting is not currently
supported.

The API is functionally equivalent to the List Records API, only header
information returned; no resource data is returned. Data elements are
renamed to map to the the OAI-PMH specification.

*NB*: There is currently no mechanism to return the collection of ids of
resources where a new resource data description document has been added
to the collation of documents for a resource within the specified time
range. Documents may only be accessed by document ID.

##### API

##### Basic Harvest: ListIdentifiers

> // Return the resource data description document headers for the
> specified time range
>
> Build results object
>
> > responseDate := time of report // time/date encoding
> >
> > request := // the API request
> >
> > {
> >
> > :   \"verb\": \"listidentifiers\", // the literal
> >     \"listidentifiers\"
> >
> >     \"from\": \"string\", // specified start of harvest time/date
> >     range
> >
> >     \"until\": \"string\", // specified end of harvest time/date
> >     range
> >
> >     \"HTTP\_request\": \"string\" // the HTTP request as a string
> >
> > }
> >
> > IF from \> until // return error
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"badArgument\"
> > > >
> > > > EXIT
> >
> > IF granularity of from time \<\> granularity of until time // return
> > error
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"badArgument\"
> > > >
> > > > EXIT
> >
> > IF granularity of from time \< service granularity
> >
> > > // request is for seconds, service instance only supports days
> > > (not seconds)
> > >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"badArgument\"
> > > >
> > > > EXIT
> >
> > IF from not specified THEN from := earliest timestamp
> >
> > IF until not specified THEN unti := latest timestamp
> >
> > FOR EACH *resource* *data* *description* document
> >
> > > IF from \<= [▲node\_timestamp]{role="changes"} from the *resource
> > > data description* document
> > >
> > > > \<= until // timestamp inclusive in \[from:until\] range
> > >
> > > THEN // return header for resource data
> > >
> > > > [▲datestamp := node\_timestamp fromt the \*resource data description\*]{role="changes"}
> > > >
> > > > identifier := resource data description document ID
> > > >
> > > > IF the delete\_data\_policy \<\> \"no\"
> > > >
> > > > > AND the *resource data description* document has been deleted
> > > > >
> > > > > THEN status := \"deleted\"
> >
> > IF listidentifiers array is empty
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"noRecordsMatch\"
> > >
> > > ELSE
> > >
> > > OK := TRUE
>
> TRANSFORM results to specified CONTENT-TYPE

#### Identify

The Identify verb returns a description of the harvest end point. The
service SHALL return the values in JSON. The service SHALL return all of
the key-value pairs listed. The service MAY return additional key-value
pairs that describe the harvest service.

A network node SHALL maintain all of the data necessary to return the
required key-value pairs.

##### API

##### Basic Harvest: Identify

> // Return the description of the harvest service
>
> Build results object
>
> > OK := TRUE
> >
> > responseDate := time of report // time/date encoding
> >
> > request := // the API request
> >
> > {
> >
> > :   \"verb\": \"identify\", // the literal \"identify\"
> >
> >     \"HTTP\_request\": \"string\" // the HTTP request as a string
> >
> > }
> >
> > node\_id := node\_id from the *network node description*
> >
> > repositoryName := node\_name from the *network node description*
> >
> > baseURL := \<node-service-endpoint-URL\> // URL of the network node
> >
> > protocolVersion := \"2.0\" // the OAI-PMH version
> >
> > service\_version := service\_version from the *Harvest* *service*
> > *description*
> >
> > earliestDatestamp := timestamp
> >
> > > // the oldest guaranteed publish/update or delete timestamp
> > >
> > > // time/date encoding with service-specified granularity
> >
> > deletedRecord := deleted\_data\_policy from the node\_policy from
> > the
> >
> > > *network node description*
> >
> > granularity := granularity from the *Harvest service description*
> >
> > adminEmail := node\_admin\_identity from the *network node
> > description*
> >
> > TRANSFORM results to specified CONTENT-TYPE

#### List Metadata Formats

The List Metadata Formats verb returns the list of metadata formats
available for harvests. The harvest API only returns JSON encoded
resource data descriptions: this is the only metadata format defined in
the service description. The metadataPrefix SHALL be the value specified
in the metadataformats structure in the service description (e.g.,
\"LR\_JSON\_0.10.0\"). The service SHALL return all of the key-value
pairs listed. The service SHALL NOT return additional key-value pairs.

The services does not support the retrieval of the metadata format for
an individual resource data description document. Including a ID in the
request SHOULD produce an error.

##### API

##### Basic Harvest: List Metadata Formats

> // Return the description of the metadata formats supported for
> harvest
>
> Build results object
>
> > OK := TRUE
> >
> > responseDate := time of report // time/date encoding
> >
> > request := // the API request
> >
> > > {
> > >
> > > :   \"verb\": \"listmetadataformats\", // the literal
> > >     \"listmetadataformats\"
> > >
> > >     \"HTTP\_request\": \"string\" // the HTTP request as a string
> > >
> > > }
> >
> > metadataFormat := metadataformat structure from the *Harvest*
> > *service* *description*
> >
> > > // the key-value pair \[{\"metadataPrefix\":
> > > \"LR\_JSON\_0.10.0\"}\]
> >
> > TRANSFORM results to specified CONTENT-TYPE

#### List Sets

The List Sets verb returns the list of sets used to organize resource
data descriptions. Support for sets is not defined in this version of
the specification. The API SHALL return a standard error indicating that
sets are not available.

##### API

##### Basic Harvest: List Sets

> // Return the description of the sets available for harvest
>
> Build results object
>
> > OK := FALSE
> >
> > error := \"noSetHierarchy\"
> >
> > responseDate := time of report // time/date encoding
> >
> > request := // the API request
> >
> > {
> >
> > :   \"verb\": \"listsets\", // the literal \"listsets\"
> >
> >     > \"HTTP\_request\": \"string\" // the HTTP request as a string
> >
> > }
>
> TRANSFORM results to specified CONTENT-TYPE

##### Service Description

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
provided. Appropriate values for the service\_data elements SHALL be
provided. The descriptive values (service\_name, service\_description)
MAY be changed from what is specified herein.

### OAI-PMH Harvest Service {#OAI-PMH Harvest Service}

The OAI-PMH harvest services can be used by an external agent to connect
to a node to harvest (pull) the resource data (e.g., the metadata or
paradata) contained in the resource data description documents stored at
the node. The service defines how to harvest a variety of metadata
formats (DC, LOM), paradata formats, etc., along with full resource data
description documents stored at the node. Unless specified, the service
SHALL support OAI-PMH V2.0. Harvest is done by resource data description
document ID or by resource ID, i.e., by resource locator. Set-based
harvesting is not currently supported. Flow control is not currently
supported.

*OAI-PMH* *Extension*: IDs MAY be:

-   the document ID for a resource data description document. The
    service SHALL return the single resource data description document
    that matches the ID.
-   a unique resource identifier, e.g., the resource locator. The
    service SHALL return all resource data description documents for the
    specified resource that satisfy other harvest criteria.

*NB*: The service could be built using basic harvest service. The core
functionality is present in basic harvest service. A transformation
would be applied to the results to convert them from JSON to XML.

To support extensions, the OAI-PMH XSD has been extended. A copy of the
schema is currently available at:
<https://www.learningregistry.org/documents/downloads/OAI-PMH-LR.xsd>
This schema:

-   adds the ID arguments for GetRecord
-   supports the return of a multiple records from GetRecord
-   adds the ID arguments for ListMetatdataFormats
-   makes metadataNamespace optional

*NB*: There is no guarantee of persistence of the XSD. The service
description for the OAI-PMH harvest service includes a schema location
key-value pair used to indicate the persistent XSD location.

Mapping Learning Registry OAI-PMH Harvest to OAI-PMH Concepts

  ------------------------ ----------------------------------------------
  **Native OAI-PMH         **Learning Registry Harvest API Concept**
  Concept**

  Repository (harvest API  Node Resource Data Description Document
  end point)               Database

  Resource (something that Resource
  has records)

  Item (something in the   Resource Data, e.g., an individual Resource
  repository for which a   Data Description Document or a collation of
  record can be            Resource Data Description Documents for a
  disseminated)            unique Resource

  Record (dissemination    Resource Data Description Document Resource
  output)                  Data

  Item Identifier (URI)    Resource Data Description Document ID
                           orResource ID/Resource Locator

  Metadata Format          Resource Data Description Document Payload
                           Schema

  Set                      *Sets* *for* *organizing* *resource* *data*
                           *are* *not* *defined* *in* *this* *version*
                           *of* *the* *specification*

  GetRecord Verb           \<nodelURL\>OAI-PMH?verb=GetRecord

  ListRecords Verb         \<nodelURL\>OAI-PMH?verb=ListRecords

  ListIdentifiers Verb     \<nodelURL\>OAI-PMH?verb=ListIdentifiers

  Identify Verb            \<nodelURL\>OAI-PMH?verb=Identify

  ListMetadataFormats Verb \<nodelURL\>OAI-PMH?verb=ListMetadataFormats

  ListSets Verb            \<nodelURL\>OAI-PMH?verb=ListSets
  ------------------------ ----------------------------------------------

Each of the six harvest verbs are specified separately. The Service
Description document SHALL apply to the entire API.

The network node SHALL maintain a value for the earliest publication
time for documents harvestable from the node (earliestDatestamp).
Time-based harvesting MAY request harvest for documents published,
updated or deleted after that time. The node MAY maintain documents with
an earlier timestamp, but these documents SHALL NOT be accessible via
harvest. The granularity for access via the timestamp MAY be days or
seconds. The granularity of the timestamp SHALL be stored in the service
description document.

*NB*: The actual timestamp MAY have a finer granularity.

*NB*: All times are UTC 0.

*NB*: As specified in OAI-PMH, the granularity in response data SHALL be
seconds.

*OAI-PMH* *Extension*: If the requested dissemination format in
metadataPrefix matches the JSON metadataPrefix in the servcie
description (e.g., \"LR\_JSON\_0.10.0\"), the service SHALL behave as
the basic harvest service, i.e., it returns the complete resource data
description document as JSON.

The internal JSON storage of a resource data description document MAY
include additional key-value pairs defined in this specification. The
service MAY return all stored key-value pairs, or only the key-value
pairs defined in this specification for the resource data description
document. The service document SHALL indicate if the returned documents
are limited to the specification-defined key-value pairs only or if all
stored key-value pairs are returned.

#### Get Record

The Get Record verb returns resource data (e.g., the metadata or
paradata) that matches the requested dissemination format for the
specified resource data description document ID or resource ID.

*OAI-PMH* *Extension*: If the request ID is a resource data description
document ID, the service SHALL return the metadata dissemination for the
single resource data description document that matches the ID. If the
request ID is a unique resource identifier, e.g., the resource locator,
the service SHALL return the metadata disseminations for all resource
data description documents for the specified resource.

The Get Record verb SHALL support the return any resource\_data that
matches the requested dissemination format that is associated with the
requested resource data document, i.e., any payload where the
payload\_schema matches the requested dissemination format. An
implementation MAY support the translation of the stored resource\_data
to the requested dissemination format. An implementation MAY support
equivalence matching for the requested dissemination format, e.g., the
available format X is recognized to be the same as the requested format
Y. An implementation MAY support the automated generation of
resource\_data in the requested dissemination format.

The Get Record verb SHALL support the return of resource\_data
independent of where it is stored in the payload, i.e., it returns any
inline, attached or referenced resource data in the payload of the
specified resource data description document.

If the requested metadata dissemination is not available for the
requested ID, the service SHALL return a cannotDisseminateFormat error.

*OAI-PMH* *Extension*: If the requested dissemination format in
metadataPrefix matches the JSON metadataPrefix in the servcie
description (e.g., \"LR\_JSON\_0.10.0\"), the service SHALL behave as
the basic harvest service, i.e., it returns the complete resource data
description document as JSON. This behavior is NOT specified in the
pseudo code below.

*ToDo*: Extend to produce (log) a usage record of the harvest.

##### API

##### OAI-PMH: GetRecord

> // Return the resource data from the resource data description
> document for the ID in the request
>
> Build XML results document
>
> EMIT OAI-PMH namespace declarations
>
> EMIT the required + extension elements
>
> > \<responseDate\>time of report\<responseDate\>
> >
> > \<request
> >
> > > verb=\"GetRecord\" // the literal \"GetRecord\"
> > >
> > > identifier=\<ID\> // request ID
> > >
> > > metadataPrefix=\<metadataformat\> // requested metadata format
> > >
> > > by\_doc\_ID=\<boolean\> // by document request flag
> > >
> > > by\_resource\_ID=\<boolean\> // by resource request flag
> > >
> > > \>
> > >
> > > HTTP\_request // the HTTP request as a string
> >
> > \</request\>
>
> IF identifier not supplied // return error element
>
> > \<error code=\"badArgument\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF metadataPrefix not supplied // return error element
>
> > \<error code=\"badArgument\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF by\_doc\_ID AND by\_resource\_ID
>
> > \<error code=\"badArgument\" /\> // only one can be true
> >
> > Complete XML
> >
> > EXIT
>
> // Does the document exist
>
> IF by\_doc\_ID AND
>
> > no *resource* *data* *description* document with doc\_ID =
> > \<identifier\>
> >
> > THEN
> >
> > > \<error code=\"idDoesNotExist\" /\>
> > >
> > > Complete XML
> > >
> > > EXIT
>
> IF by\_resource\_ID AND no *resource* *data* *description* document
> with resource\_locator = \<identifier\>
>
> > THEN
> >
> > > \<error code=\"idDoesNotExist\" /\>
> > >
> > > Complete XML
> > >
> > > EXIT
>
> IF by\_resource\_ID // get the list of documents otherwise it's just
> the requested ID
>
> > THEN
> >
> > > FIND the collation of resource data description documents IDs as
> > > \<identifier\>
> > >
> > > WHERE resource\_locator MATCHES request \<identifier\>
>
> FOR EACH resource data description document IDs
>
> // Is there an acceptable metadata format
>
> IF payload\_schema \<\> \<resourcedataformat\> OR
>
> > NOT *Same\_As* *or* *Translatable* (payload\_schema,
> > \<resourcedataformat\>)
> >
> > \<error code=\"cannotDisseminateFormat\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> Build \<GetRecord\>
>
> \<GetRecord\>
>
> Build \<record\>
>
> \<record\>
>
> > EMIT \<header\>
> >
> > \<header
> >
> > > IF delete\_data\_policy \<\> \"no\"
> > >
> > > AND the *resource data description* document has been deleted
> > >
> > > THEN status =\"deleted\"
> > >
> > > \>
> >
> > \<identifier\>resource data description document
> > doc\_ID\</identifier\>
> >
> > > \<datastamp\> [▲node\_timestamp]{role="changes"} from the
> > > *resource data description* \</datestamp\>
> >
> > \</header\>
> >
> > EMIT \<metadata\>
> >
> > \<metadata\>
> >
> > > CASE
> > >
> > > > payload\_placement = \"inline\"
> > > >
> > > > > EMIT resource data in XML
> > > >
> > > > payload\_placement = \"attachment\"
> > > >
> > > > > EMIT attached document in XML
> > > >
> > > > payload\_placement = \"linked\"
> > > >
> > > > > Get resource data from payload\_schema\_locator
> > > > >
> > > > > EMIT document in XML
> > >
> > > IF EMIT fails
> > >
> > > > \<error code=\"cannotDisseminateFormat\" /\>
> > > >
> > > > Complete XML
> > > >
> > > > EXIT
> >
> > \</metadata\>
>
> \</record\>
>
> \</GetRecord\>

#### List Records

The List Records verb returns the resource data description documents
for the specified resource data document IDs within a specified
time/date range. Set-based harvesting is not currently supported.

The List Records verb SHALL support the return of any resource\_data
that matches the requested dissemination format that is associated with
the specified resource data document, i.e., any payload where the
payload\_schema matches the requested dissemination format. An
implementation MAY support the translation of the stored resource\_data
to the requested dissemination format. An implementation MAY support
equivalence matching for the requested dissemination format, e.g., the
available format X is recognized to be the same as the requested format
Y. An implementation MAY support the automated generation of
resource\_data in the requested dissemination format.

The List Records verb SHALL support the return of resource\_data
independent of where it is stored in the payload, i.e., it returns any
inline, attached or referenced resource data in the payload of the
specified resource data description document.

*NB*: The combination of processing deleted records and records that do
not have the specified metadata dissemination is not clear in the
OAI-PMH specification. Since not all resource data description documents
support all formats, the service only returns deleted status for
documents that match the requested dissemination format.

*NB*: A test to determine if no records match the requested metadata
dissemination format is not included. The resulting error code of
cannotDisseminateFormat does not occur. If no records match the
requested metadata dissemination format, the error code SHALL be
noRecordsMatch.

*OAI-PMH Extension*: If the requested dissemination format in
metadataPrefix matches the JSON metadataPrefix in the servcie
description (e.g., \"LR\_JSON\_0.10.0\"), the service SHALL behave as
the basic harvest service, i.e., it returns the complete resource data
description document as JSON. This behavior is NOT specified in the
pseudo code below.

*NB*: List records does not support access by resource locator.
Documents may only be accessed by document ID.

*ToDo*: Extend to produce (log) a usage record of the harvest.

##### API

##### OAI-PMH: ListRecords

> // Return the resource data description documents for the specified
> time range
>
> Build XML results document
>
> EMIT OAI-PMH namespace declarations
>
> EMIT the required elements
>
> > \<responseDate\>time of report\<responseDate\>
> >
> > \<request
> >
> > > verb=\"ListRecords\" // the literal \"ListRecords\"
> > >
> > > metadataPrefix=\<metadataformat\> // requested metadata format
> > >
> > > from=\<date\> // start of harvest time/date range
> > >
> > > until=\<date\> // end of harvest time/date range
> > >
> > > \>
> > >
> > > HTTP\_request // the HTTP request as a string
> >
> > \</request\>
>
> IF from \> until // return error
>
> > \<error code=\"badArgument\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF granularity of from time \<\> granularity of until time // return
> error
>
> > \<error code=\"badArgument\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF granularity of from time \< service granularity
>
> > // request is for seconds, service instance only supports days (not
> > seconds)
> >
> > \<error code=\"badArgument\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF from not specified THEN from := earliest timestamp
>
> IF until not specified THEN until := latest timestamp
>
> Build \<ListRecords\>
>
> \<ListRecords\>
>
> FOR EACH *resource data description* document
>
> > IF from \<= [▲node\_timestamp]{role="changes"} from the *resource
> > data description* document
> >
> > > \<= until // timestamp inclusive in \[from:until\] range
> >
> > THEN
> >
> > IF payload\_schema \<\> \<resourcedataformat\> OR
> >
> > > NOT *Same\_As or Translatable* (payload\_schema,
> > > \<resourcedataformat\>)
> > >
> > > NEXT LOOP
> >
> > THEN
> >
> > > Build a \<record\>
> > >
> > > \<record\>
> > >
> > > EMIT \<header\>
> > >
> > > \<header
> > >
> > > > IF delete\_data\_policy \<\> \"no\"
> > > >
> > > > AND the *resource data description* document has been deleted
> > > >
> > > > > THEN status =\"deleted\"
> > > >
> > > > \>
> > >
> > > \<identifier\>resource data description document ID\</identifier\>
> > >
> > > \<datastamp\> [▲node\_timestamp]{role="changes"} from the
> > > *resource data description* \</datestamp\>
> > >
> > > \</header\>
> > >
> > > EMIT \<metadata\>
> > >
> > > \<metadata\>
> > >
> > > > CASE
> > > >
> > > > > payload\_placement = \"inline\"
> > > > >
> > > > > > EMIT resource data in XML
> > > > >
> > > > > payload\_placement = \"attachment\"
> > > > >
> > > > > > EMIT attached document in XML
> > > > >
> > > > > payload\_placement = \"linked\"
> > > > >
> > > > > > Get resource data from payload\_schema\_locator
> > > > > >
> > > > > > EMIT document in XML
> > > >
> > > > IF EMIT fails
> > > >
> > > > > \<error code=\"cannotDisseminateFormat\" /\>
> > > > >
> > > > > Complete XML
> > > > >
> > > > > EXIT
> > >
> > > \</metadata\>
>
> \</record\>
>
> \</ListRecords\>
>
> IF \<ListRecords\> is empty
>
> THEN
>
> > DELETE \<ListRecords\> element
> >
> > \<error code=\"noRecordsMatch\" /\>
> >
> > Complete XML
> >
> > EXIT

#### List Identifiers

The List Identifiers verb returns the header information for the
resource data description documents for the specified resource data
document IDs within a specified time/date range. Flow control is not
currently supported. Set-based harvesting is not s currently supported.

The API is functionally equivalent to the List Records API, only header
information is returned; no resource data is returned.

*NB*: There is currently no mechanism to return the collection of ids of
resources where a new resource data description document has been added
to the collation of documents for a resource within the specified time
range. Documents may only be accessed by document ID.

##### API

##### OAI-PMH: ListIdentifiers

> // Return the resource data description document headers for the
> specified time range
>
> Build XML results document
>
> EMIT OAI-PMH namespace declarations
>
> EMIT the required elements
>
> > \<responseDate\>time of report\<responseDate\>
> >
> > \<request
> >
> > > verb=\"ListIdentifiers\" // the literal \"ListIdentifiers\"
> > >
> > > metadataPrefix=\<metadataformat\> // requested metadata format
> > >
> > > from=\<date\> // start of harvest time/date range
> > >
> > > until=\<date\> // end of harvest time/date range
> > >
> > > \>
> > >
> > > HTTP\_request // the HTTP request as a string
> >
> > \</request\>
>
> IF from \> until // return error
>
> > \<error code=\"badArgument\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF granularity of from time \<\> granularity of until time // return
> error
>
> > \<error code=\"badArgument\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF granularity of from time \< service granularity
>
> > // request is for seconds, service instance only supports days (not
> > seconds)
> >
> > \<error code=\"badArgument\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF from not specified THEN from := earliest timestamp
>
> IF until not specified THEN until := latest timestamp
>
> Build \<ListIdentifiers\>
>
> \<ListListIdentifers\>
>
> FOR EACH *resource data description* document
>
> > IF from \<= [▲node\_timestamp]{role="changes"} from the *resource
> > data description* document
> >
> > > \<= until // timestamp inclusive in \[from:until\] range
> >
> > THEN
> >
> > IF payload\_schema \<\> \<resourcedataformat\> OR
> >
> > > NOT *Same\_As or Translatable* (payload\_schema,
> > > \<resourcedataformat\>)
> > >
> > > NEXT LOOP
> >
> > THEN
> >
> > Build a \<record\>
> >
> > \<record\>
> >
> > EMIT \<header\>
> >
> > \<header
> >
> > > IF delete\_data\_policy \<\> \"no\"
> > >
> > > AND the *resource data description* document has been deleted
> > >
> > > THEN status =\"deleted\"
> > >
> > > \>
> >
> > \<identifier\>resource data description document ID\</identifier\>
> >
> > \<datastamp\> [▲node\_timestamp]{role="changes"} from the *resource
> > data description* \</datestamp\>
> >
> > \</header\>
>
> \</record\>
>
> \</ListRecords\>
>
> IF \<ListRecords\> is empty
>
> > THEN
> >
> > DELETE \<ListRecords\> element
> >
> > \<error code=\"noRecordsMatch\" /\>
> >
> > Complete XML
> >
> > EXIT

#### Identify

The Identify verb returns a description of the OAI-PMH harvest end
point. The service SHALL return all of the values specified in the
OAI-PMH specification, using the specified XML schema. The service MAY
return additional XML elements that describe the harvest service
specified in the OAI-PMH specification.

A network node SHALL maintain all of the data necessary to return the
required elements.

##### API

##### OAI-PMH: Identify

> // Return the description of the harvest service
>
> Build XML results document
>
> EMIT OAI-PMH namespace declarations
>
> EMIT the required elements
>
> > \<responseDate\>time of report\<responseDate\>
> >
> > \<request
> >
> > > verb=\"Identify\" // the literal \"Identify\"
> > >
> > > \>
> > >
> > > HTTP\_request // the HTTP request as a string
> >
> > \</request\>
>
> Build \<Identify\>
>
> EMIT the required elements
>
> ::: {.sourcecode}
> xml
>
> \<Identitfy\>
>
> > \<repositoryName\>node\_name from the *network node
> > description*\</repositoryName\>
> >
> > \<baseURL\>URL of the network node\</baseURL\>
> >
> > \<protocolVersion\>2.0\</protocolVersion\>
> >
> > \<earliestDatestamp\>the oldest guaranteed publish/update or delete
> >
> > > timestamp\</earliestDatestamp\>
> >
> > \<deletedRecord\>deleted\_data\_policy from the node\_policy from
> > the
> >
> > > *network node description*\</deletedRecord\>
> >
> > \<granularity\>granularity from the *OAI-PMH Harvest service
> > description*\</granularity\>
> >
> > \<adminEmail\>node\_admin\_identity from the *network node
> > description*\</adminEmail\>
>
> \</Identify\>
> :::

#### List Metadata Formats

The List Metadata Formats verb returns the list of metadata formats
available for harvests. The service SHALL return all of the elements
specified in the OAI-PMH specification, using the specified XML schema.
The service SHALL NOT return additional XML elements.

The metadata format is a triple of three XML elements:
\<metadataPrefix\>, \<schema\> and \<metadataNameSpace\>. The service
determines the available formats from the payload\_schema key-value pair
in the resource data description documents. Each value in the
payload\_schema array SHALL be considered as a separate dissemination
format, i.e., a separate value for \<metadataPrefix\>. The value for
\<schema\> SHALL be the value of corresponding payload\_schema\_locator.

Determining the value of \<metadataNameSpace\> is optional. The service
does not define how to determine the value for \<metadataNameSpace\>.

*NB*: Both \<schema\> and \<metadataNameSpace\> are optional elements in
the \<metadataFormat\>.

If an identifier is provided, the metadata formats SHALL be returned
only for the identified resource data description documents. If an
identifier is *not* provided, the metadata formats SHALL be returned for
*all* resource data description documents.

*OAI-PMH* *Extension*: If the request ID is a resource data description
document ID, the service SHALL return the metadata formats for the
single resource data description document that matches the ID. If the
request ID is a unique resource identifier, e.g., the resource locator,
the service SHALL return the metadata format for all resource data
description documents for the specified resource.

Only unique dissemination formats SHALL be included in the list of
formats. Duplicate dissemination formats SHALL be removed. A duplicate
SHALL have identical \<metadataPrefix\>, \<schema\> and
\<metadataNameSpace\> values to those of another entry. Two
dissemination formats that differ in both \<schema\> or
\<metadataNameSpace\> values SHALL be considered to be unique. Two
dissemination formats that differ in only \<schema\> values SHALL be
considered to be unique unless the service can determine that the actual
schemata are identical copies. Determining if two schemata values
represent identical copies is optional.

Values for payload\_schema that correspond to generic schemata (e.g.,
\"XML\", \"RDF\") SHOULD be removed from the list of dissemination
formats.

The service MAY order the resulting list of formats by the occurrences,
most common first.

The service SHOULD NOT return values that do not satisfy the OAI-PMH
requirement that \<metadataPrefix\> be a string of "any valid URI
unreserved characters".

The service SHALL include the Learning Registry JSON resource data
description document format

metadataPrefix specified in the metadataformats structure in the service
description (e.g., \"LR\_JSON\_0.10.0\") in the results list of formats.

##### API

##### OAI-PMH: List Metadata Formats

> // Results View
>
> Define a view of the resource data description documents
>
> > IF identifier is provided
> >
> > > THEN
> > >
> > > IF by\_doc\_ID
> > >
> > > > THEN use the resource data description document where doc\_ID =
> > > > \<identifier\>
> > >
> > > IF by\_resource\_ID
> > >
> > > > THEN use all resource data description documents where
> > > > resource\_locator = \<identifier\>
> > >
> > > ELSE use all resource data description documents
> >
> > View includes: payload\_schema, payload\_schema\_locator
> >
> > Expand to one payload\_schema\_locator for each value in
> > payload\_schema
> >
> > Optionally order by (1) payload\_schema, (2)
> > payload\_schema\_locator
> >
> > Remove duplicates preserving ordering
> >
> > Filter to remove unneeded entries
> >
> > Add all Same\_As or Translatable metadata formats
> >
> > Add all metadata formats that can be automatically generated
>
> // Return the description of the metadata formats supported for
> harvest
>
> Build XML results document
>
> EMIT OAI-PMH namespace declarations
>
> > EMIT the required elements
> >
> > \<responseDate\>time of report\<responseDate\>
> >
> > \<request
> >
> > > verb=\"ListMetadataFormats\" // the literal
> > > \"ListMetadataFormats\"
> > >
> > > identifier=\<ID\> // request ID
> > >
> > > by\_doc\_ID=\<boolean\> // by document request flag
> > >
> > > by\_resource\_ID=\<boolean\> // by resource request flag
> > >
> > > \>
> > >
> > > HTTP\_request // the HTTP request as a string
> >
> > \</request\>
>
> IF by\_doc\_ID AND by\_resource\_ID
>
> > \<error code=\"badArgument\" /\> // only one can be true
> >
> > Complete XML
> >
> > EXIT
>
> IF \<identifier\> provided AND
>
> > by\_doc\_ID AND
> >
> > no *resource* *data* *description* document with doc\_ID =
> > \<identifier\>
> >
> > \<error code=\"idDoesNotExist\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF \<identifier\> provided AND
>
> > by\_resoruce\_ID AND
> >
> > no *resource* *data* *description* document with resource\_locator =
> > \<identifier\>
> >
> > \<error code=\"idDoesNotExist\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> IF \<identifier\> provided AND Results View is empty
>
> > \<error code=\"noMetadaFormats\" /\>
> >
> > Complete XML
> >
> > EXIT
>
> Build \<ListMetadataFormats\>
>
> \<ListMetadataFormats\>
>
> FOR EACH element in Results View
>
> // Add Learning Registry Native JSON format
>
> \<ListMetadataFormats\>
>
> IF \<ListMetadataFormats\> is empty
>
> > THEN
> >
> > DELETE \<ListMetadataFormats\> element
> >
> > \<error code=\"noMetadaFormats\" /\>
> >
> > Complete XML
> >
> > EXIT

#### List Sets

The List Sets verb returns the list of sets used to organize resource
data descriptions. Support for sets is not defined in this version of
the specification. The API SHALL return a standard error indicating that
sets are not available.

##### API

##### OAI-PMH: List Sets

> // Return the description of the sets available for harvest
>
> Build XML results document
>
> EMIT OAI-PMH namespace declarations
>
> EMIT the required elements
>
> > \<responseDate\>time of report\<responseDate\>
> >
> > \<request
> >
> > > verb=\"ListSets\" // the literal \"ListSets\"
> > >
> > > \>
> > >
> > > HTTP\_request // the HTTP request as a string
> >
> > \</request\>
>
> // No Set Support
>
> \<error code=\"noSetHierarchy\" /\>

##### Service Description

```javascript
    {
        "doc_type": "service_description",
        "doc_version": "0.20.0",
        "doc_scope": "node",
        "active": true,
        "service_id": "<uniqueid>",
        "service_type": "access",
        "service_name": "OAI-PMH Harvest",
        "service_description": "Service to retrieve metadata/paradata from resource description documents using the OAI-PMH 2.0 protocol",
        "service_version": "0.10.0",
        "service_endpoint": "<node-service-endpoint-URL>/OAI-PMH",
        "service_auth":
                                        // service authentication and authorization descriptions
            {"service_authz": ["<authvalue>"],
                                        // authz values for the service
            "service_key": < T / F > ,
                                        // does service use an access key
            "service_https": < T / F >
                                        // does service require https
            },
        "service_data":
            {"version": "OAI-PMH 2.0",
            "schemalocation": "<XSD URL>",
                                        // location of the Learning Registry Extended OAI-PMH
                                        // XSD used to validate service responses
            "spec_kv_only": boolean
                                        // T to return only spec-defined key-value pairs
                                        // F to return all stored key-value pairs
                                        // optional, default F
                                        // Applies only when the requested output is
                                        // LR_JSON_0.10.0
            }
    }
```

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
provided. Appropriate values for the service\_data elements SHALL be
provided. The descriptive values (service\_name, service\_description)
MAY be changed from what is specified herein.

*NB*: A copy of the schema is currently available at:
<https://www.learningregistry.org/documents/downloads/OAI-PMH-LR.xsd>
There is no guarantee of persistence of this copy of the XSD. A deployed
service instance SHOULD use an existing copy of the XSD or maintain a
private copy of the XSD according to the node's data persistence
policies.

#### Change Log

*NB*: The change log only lists major updates to the specification.

*NB*: Updates and edits may not results in a version update.

*NB*: See the
[Learning Registry Technical Specification \<../Technical\_Spec/index\>]{role="doc"}
for prior change history not listed below.

  ------------- ---------- ------------ ---------------------------------------------------------------------------------------------------
  **Version**   **Date**   **Author**   **Change**

                20110921   DR           This document extracted from the monolithic V 0.24.0 document. [Archived copy (V
                                        0.24.0)](https://docs.google.com/document/d/1Yi9QEBztGRzLrFNmFiphfIa5EF9pbV5B6i9Tk4XQEXs/edit)

  0.49.0        20110927   DR           Editorial updates to create stand alone version.Archived copy location TBD. (V AS:0.49.0)

  0.50.0        TBD        DR           Renumber all document models and service documents. Added node policy to control storage of
                                        attachments (default is stored). Add page size as service doc setting with flow control.Archived
                                        copy location TBD. (V AS:0.50.0)

  Future        TBD                     ToS attribution output to OAI. Harvest flow control. Flow control to OAI. Logging/tracking emit as
                                        paradata to services. Deprecate node\_timestamp. Details of attachments on publish, obtain,
                                        harvest.Archived copy location TBD .(V AS:x.xx.x)

  0.50.1        20130312   JK           This document extracted from Google Doc and converted to RestructuredText. [Archived copy (V
                                        AS:0.49.0)](https://docs.google.com/document/d/1RRR7ZUjZRYgIyoIXPLsAZKluahqY7_Q7Gb00PHGHw8A/edit)
                                        node\_timestamp removed from deprecation.
  ------------- ---------- ------------ ---------------------------------------------------------------------------------------------------

#### Working Notes and Placeholder Text

-   Flow control consistency
-   Indicate how OAI returns linked payloads \-- what's wrong with it
-   How does a service find its service doc
-   The APIs that use Basic Auth
    -   1)  use SSL

    -   2)  depending on the node, the SSL cert may be self signed or
            signed by a CA.

    -   3)  put the Basic Auth credentials in the https request

    -   4)  the entire request is then signed when sent to LR

    -   Q: does the entire result come back as https?
