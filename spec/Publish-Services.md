Publish Services: Learning Registry Technical Specification V PS:0.50.1
=======================================================================

See the [Change Log](#change-log) for links to prior stable versions.

Major changes and additions from the prior version (0.24.0) are marked with ▲.

Significant deletions use ~~strikethrough text~~.

Features to be deprecated in a future version are indicated with ▼.

This document is part of one or more versions of the
[Learning \<../Technical\_Spec/index\>]{role="doc"}
[Registry \<../Technical\_Spec/index\>]{role="doc"}
[Technical \<../Technical\_Spec/index\>]{role="doc"}
[Specification \<../Technical\_Spec/index\>]{role="doc"}. It may contain
links to other parts of the Specification. These links may link to the
most recent version of a part, not to the version of the part that
corresponds to this version of this part. Go to the appropriate version
of the Specification that links to this version of this part, and follow
the links there to the referenced part to find the version of the part
that corresponds to this version of this part.

This document is part of the
[Learning \<../Technical\_Spec/index\>]{role="doc"}
[Registry \<../Technical\_Spec/index\>]{role="doc"}
[Technical \<../Technical\_Spec/index\>]{role="doc"}
[Specification \<../Technical\_Spec/index\>]{role="doc"}. It describes
the basic Learning Registry services used to publish (push) resource
documents into a distribution network.

This document is not standalone. The reader should be familiar with
other parts of the specification, including, but not limited to:

-   [General \<../General\_Matter/index\>]{role="doc"}
    [Matter \<../General\_Matter/index\>]{role="doc"}, including
    Licenses, Notation, Versioning, Glossary, References
-   [Resource \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
    [Distribution \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
    [Network \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
    [Model \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
-   [Resource \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
    [Data \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
    [Data \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
    [Models \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
-   [Identity \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
    [Trust \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
    [Authentication \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
    [Security \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"}
-   [Data \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
    [Model \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
    [and \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
    [API \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
    [Attributes \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
    [and \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
    [Behaviors \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
-   [Other \<../Services\_and\_APIs/index\>]{role="doc"}
    [Services \<../Services\_and\_APIs/index\>]{role="doc"} including
    [Distribution \<../Distribution\_Services/index\>]{role="doc"},
    [Access \<../Access\_Services/index\>]{role="doc"},
    [Broker \<../Broker\_Services/index\>]{role="doc"},
    [Management \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}/[Administration \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}/[Discovery \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}
-   [Learning \<../Operations/index\>]{role="doc"}
    [Registry \<../Operations/index\>]{role="doc"}
    [Operations \<../Operations/index\>]{role="doc"}

In particular, the reader needs to be aware that specific criteria for
services and APIs are presented in the
[Data \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[Model \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[and \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[API \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[Attributes \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[and \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[Behaviors \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
part, the
[Resource \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
[Distribution \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
[Network \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
[Model \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
part describes the network model, the
[Resource \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
[Data \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
[Data \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
[Models \<../Resource\_Data\_Data\_Model/index\>]{role="doc"} part
describes the model of published data and the
[Identity \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
[Trust \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
[Authentication \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
[Security \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"}
part describes security requirements.

Resource Data Publish Services {#Resource Data Publish Services}
------------------------------

Publish services are used to push resource data into the network. They
are used by external publishing edge nodes. All resource data publishing
services SHALL [apply filters \<Resource Data Filtering\>]{role="ref"}
if present to restrict the resource data that is published to the node.
All resource data publishing services SHALL
[apply validation \<Resource Data Validation and Publication\>]{role="ref"}
to restrict the resource data that is published to the node. The
validation process MAY also provide local updates to the resource
document prior to it being published. Any resource data publishing
service MAY reject any resource data for any reason:

-   From an untrusted submitter
-   From an anonymous submitter
-   Not signed
-   Signature not valid
-   Does not conform to the node's ToS.
-   Is larger than the node can store.

All resource data publishing services SHALL reject any document with a
\"do\_not\_distribute\" key-value pair; this verification SHALL be
performed before any other verification and SHALL short circuit all
other verification.

*NB*: There is no defined mechanism to define the acceptable ToS for a
node. A node MAY advertise acceptable ToS in the node description
document, but this MAY not be accurate.

*NB*: How a data publishing service decides if it accepts or rejects
resource data that comes from an untrusted submitter, is not signed,
signature cannot be validated, or that does not conform to the data
publishing service's ToS is determined by the data publishing service's
policy and is not defined in this specification.

*NB*: How a data publishing service decides that a document is too large
is determined by the data publishing service's policy and is not defined
in this specification.

Future drafts or versions of this specification MAY define additional
resource data publish services.

### Basic Publish Service {#Basic Publish Service}

The basic publish service pushes an instance of a resource data
description document (or a set of documents) directly to a node in a
resource distribution network. It is the most basic, direct mechanism to
publish resource data.

Each resource data description document in the supplied set is published
independently. In addition to the overall service return indicating
status, there SHALL be one returned object per resource data description
document, aligned 1:1 to the documents in the supplied resource data
description document array, indicating status of publishing of the
resource data description document.

Each resource data description document SHALL be published to the node's
resource data description document database. Prior to being published,
it SHALL be validated: e.g., the syntax MUST be correct, mandatory
values MUST be present, all values MUST come from the appropriate data
space. The document SHALL also be subject to all filters defined at the
node. Documents that do not pass the filters SHALL NOT be published. The
document MAY also be subject to verification of ToS and submitter
information (including presence and validity of digital signature).
Documents from anonymous submitters, untrusted submitters, unsigned
documents, or documents with a ToS that is not acceptable to the node
MAY be rejected. Documents that are too large MAY be rejected.

The publication process provides values for specific elements in the
resource data description document.

If the resource data description document does not have an assigned
identifier, the service SHALL assign one and return the value.

If the resource data description document has an identifier and a
document with the same identifier exists in the resource data
description document collection, the new document SHALL be an update,
replacing the existing document in total. If the resource data
description document is being updated, the value of an immutable element
SHALL NOT be changed.

The publication process SHALL set values for publish\_node, ,
update\_timestamp, [▲ node\_timestamp]{role="changes"},
create\_timestamp. All timestamp values SHALL be the identical. All
timestamp values SHALL be UTC 0.

*NB*: There are no restrictions on the size of a batch publish document
set, either in the number of elements or the total size of the HTTP
message. An implementation SHALL indicate any size limits in the service
description.

*NB*: The process currently does not handle attachments.

*NB*: The process currently does not support updating published
documents.

*Open* *Question*: Publishing to the node is by the node owner. Do we
need more to support trust?

*NB*: The process currently does not handle attachments.

#### API

#### Basic Publish

> // Publish each resource data description document in the supplied
> list
>
> // Perform Validation
>
> VALIDATE the *resource* *data* *description* document does not contain
> a do\_not\_distribute key.
>
> > IF do\_not\_distribute key is present
> >
> > > THEN // create the global error object
> > >
> > > > OK := F
> > > >
> > > > error := \"cannot publish\" // an appropriate error for global
> > > > condition
> > > >
> > > > EXIT
>
> VALIDATE the publish request
>
> :   // apply appropriate business rules
>
> > IF there is an overall error
> >
> > > THEN // create the global error object
> > >
> > > > OK := F
> > > >
> > > > error := \"error msg\" // an appropriate error for global
> > > > condition
> > > >
> > > > EXIT
>
> OK := T
>
> :   // global return status
>
> FOR EACH *resource* *data* *description* document
>
> > VALIDATE the *resource* *data* *description* document
> >
> > :   // all syntactical and semantic rules
> >
> > IF there is an error
> >
> > > THEN
> > >
> > > :   // create an error object array element object for the
> > >     individual document
> > >
> > > > OK := F
> > > >
> > > > error := \"error msg\" // an appropriate error for the document
> > > >
> > > > doc\_ID := supplied doc\_ID
> > > >
> > > > SKIP
> >
> > IF the *network* *node* *filter* *description* document exists and
> > contains active filters
> >
> > > THEN PERFORM filtering and store only documents that pass the
> > > filter
> > >
> > > IF the *resource* *data* *description* document does NOT pass the
> > > filter
> > >
> > > > THEN // indicate filtering was applied
> > > >
> > > > > OK := F
> > > > >
> > > > > error := \"rejected by filter\" // an appropriate filtering
> > > > > message
> > > > >
> > > > > doc\_ID := supplied doc\_ID
> > > > >
> > > > > SKIP
> >
> > IF the service applies ToS checks
> >
> > > AND the *resource* *data* *description* document TOS is
> > > unacceptable
> > >
> > > > THEN
> > > >
> > > > :   // indicate ToS was rejected
> > > >
> > > > > OK := F
> > > > >
> > > > > error := \"rejected by ToS\" // an appropriate message
> > > > >
> > > > > doc\_ID := supplied doc\_ID
> > > > >
> > > > > SKIP
> >
> > IF the service does not accept anonymous submissions
> >
> > > AND the *resource* *data* *description* document has
> > > submitted\_type==\"anonymous\"
> > >
> > > > THEN // indicate submitted type was rejected
> > > >
> > > > > OK := F
> > > > >
> > > > > error := \"anon submission rejected\" // an appropriate
> > > > > message
> > > > >
> > > > > doc\_ID := supplied doc\_ID
> > > > >
> > > > > SKIP
> >
> > IF the service validates the submitter
> >
> > > AND the *resource* *data* *description* document submitter cannot
> > > be verified or trusted
> > >
> > > > THEN // indicate submitter was rejected
> > > >
> > > > > OK := F
> > > > >
> > > > > error := \"rejected submitter\" // an appropriate message
> > > > >
> > > > > doc\_ID := supplied doc\_ID
> > > > >
> > > > > SKIP
> >
> > IF the service requires a signature
> >
> > > AND the *resource* *data* *description* document signature not
> > > present
> > >
> > > > THEN // indicate signature was rejected
> > > >
> > > > :   OK := F
> > > >
> > > >     error := \"no signature\" // an appropriate message
> > > >
> > > >     doc\_ID := supplied doc\_ID
> > > >
> > > >     SKIP
> > > >
> > IF the service validates the signature
> >
> > > AND the *resource* *data* *description* document signature cannot
> > > be verified
> > >
> > > > THEN
> > > >
> > > > :   // indicate signature was rejected
> > > >
> > > > > OK := F
> > > > >
> > > > > error := \"rejected signature\" // an appropriate message
> > > > >
> > > > > doc\_ID := supplied doc\_ID
> > > > >
> > > > > SKIP
> >
> > IF the node limits the size of document that can be stored
> >
> > > AND the *resource* *data* *description* document is too large
> > >
> > > > THEN // indicate document too large
> > > >
> > > > > OK := F
> > > > >
> > > > > error := \"too large\" // an appropriate message
> > > > >
> > > > > doc\_ID := supplied doc\_ID
> > > > >
> > > > > SKIP
> >
> > IF *resource* *data* *description* document did not have a supplied
> > doc\_ID
> >
> > > THEN generate a new unique doc\_ID
> >
> > [▲ graveyard := \[\]]{role="changes"}
> >
> > [IF \*resource\* \*data\* \*description\* document has a non-empty \"replaces\" property]{role="changes"}
> >
> > > [THEN // check that document can be published according to replacement policy]{role="changes"}
> > >
> > > > [FOR EACH \*resource\* \*data\* \*description\* specifed in \"replaces\" property]{role="changes"}
> > > >
> > > > > [IF the original \*resource data description\* document can be replaced]{role="changes"}
> > > > >
> > > > > > [THEN // indicate tombstone can be created]{role="changes"}
> > > > > >
> > > > > > > [CREATE \*tombstone document\* for original \*resource data description\* document]{role="changes"}
> > > > > > >
> > > > > > > [PUSH  \*tombstone document\* to graveyard]{role="changes"}
> > > > > >
> > > > > > [IF the replacement \*resource data description\* document violates \*replacement policy\*]{role="changes"}
> > > > > >
> > > > > > > [THEN // indicate that replacement is invalid and not permitted]{role="changes"}
> > > > > > >
> > > > > > > > [OK := F]{role="changes"}
> > > > > > > >
> > > > > > > > [error := \"rejected replacement\" // an appropriate message]{role="changes"}
> > > > > > > >
> > > > > > > > [doc\_ID := supplied doc\_ID]{role="changes"}
> > > > > > > >
> > > > > > > > [SKIP]{role="changes"}
> >
> > PUBLISH the *resource* *data* *description* document to the node by
> > the owner of the node to the node's resource data description
> > document database
> >
> > > SET publish\_node, update\_timestamp,
> > > [▲ node\_timestamp]{role="changes"}, create\_timestamp
> >
> > IF there is a publishing error
> >
> > > THEN
> > >
> > > :   // create an error object array element object for the
> > >     individual document
> > >
> > > > OK := F
> > > >
> > > > error := \"publish failed\"
> > > >
> > > > :   // an appropriate error for the publish failure
> > > >
> > > > doc\_ID := supplied doc\_ID
> > > >
> > > > SKIP
> >
> > [▲ VALIDATE tombstones in graveyard may be saved.]{role="changes"}
> >
> > > IF tombstones are permitted to be saved by *replacement policy*
> > >
> > > > THEN
> > > >
> > > > > FOR EACH tombstone in graveyard
> > > > >
> > > > > > IF *tombstone document* exists for *resource data
> > > > > > description document* specified in *tombstone document*:
> > > > > >
> > > > > > > SKIP
> > > > > >
> > > > > > ELSE
> > > > > >
> > > > > > > UPDATE original *resource data description document* specified in *tombstone document* with the *tombstone document*
> > > > > > >
> > > > > > > :   // this is a replacement operation
> > > > > > >
> > > > > > >     // create a return object array element object for the
> > > > > > >     individual document
> > > > > > >
> > OK := T
> >
> > doc\_ID
> >
> > :   // supplied or generated doc\_ID
> >
#### Service Description

```javascript
    {
        "doc_type": "service_description",
        "doc_version": "0.20.0",
        "doc_scope": "node",
        "active": true,
        "service_id": "<uniqueid>",
        "service_type": "publish",
        "service_name": "Basic Publish",
        "service_description": "Service to directly publish one or more resource description documents to the node",
        "service_version": "0.23.0",
        "service_endpoint": "<node-service-endpoint-URL>",
        "service_auth":
                                        // service authentication and authorization descriptions
        {
            "service_authz": ["<authvalue>"],
                                        // authz values for the service
            "service_key": < T / F > ,
                                        // does service use an access key
            "service_https": < T / F >
                                        // does service require https
        },
        "service_data":
        {
            "doc_limit": integer,
                                        // specify the maximum number of documents in a batch
            "msg_size_limit": integer
                                        // specify the maximum message size
        }
    }
```

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
provided. Appropriate values for the service\_data elements SHALL be
provided. The descriptive values (service\_name, service\_description)
MAY be changed from what is specified herein.

### SWORD Publish Service

[SWORD](http://www.google.com/url?q=http%3A%2F%2Fswordapp.org%2F&sa=D&sntz=1&usg=AFQjCNHNjbuSIPXGlVbbWTlOZJYcQXnMSQ)
(Simple Web-service Offering Repository Deposit) is a profile of the
Atom Publishing Protocol (known as APP or ATOMPUB). The SWORD APP API
provides a mechanism for a repository to publish its metadata or
paradata to a node in the resource distribution network. Unless
specified, the service SHALL support the SWORD V 1.3 protocol.

The SWORD service currently supports publishing of a resource data
description document to a node. A node corresponds to a SWORD
collection; there is only one collection to deposit to. The service
supports SWORD developer features and mediated deposit. The service
currently only supports the deposit JSON encoded resource data
description documents. Package support is currently not specified.

The service end points for the protocol operations are:

  ------------------ ----------------------------------------------------
  **Atom** **Pub**   **SWORD** **API** **Endpoint**
  **Protocol**
  **Operation**

  Retrieving a       GET \<node-service-endpoint-url\>/swordservice
  Service Document

  Listing            Currently not supported. To be added in a later
  Collections        version of the specification.

  Creating a         POST \<node-service-endpoint-url\>/swordpub
  Resource

  Editing a Resource Currently not supported. May be added in a later
                     version of the specification.

  Deleting a         Currently not supported. May be added in a later
  Resource           version of the specification

  Retrieving a       Not supported \-- provided via the Atom Pub Service
  Resource
  ------------------ ----------------------------------------------------

*Open* *Question*: Should SWORD just publish the raw metadata or
paradata document and let the service create the JSON?

Each of the protocol operations are specified separately. The Service
Description document SHALL apply to the entire API.

#### Retrieve Service Document

The SWORD Service Document endpoint SHALL return an XML SWORD Service
Document with the following settings:

-   Global element settings:
-   \<sword:version\> element: 1.3
-   \<sword:verbose\> element: true
-   \<sword:noOp\> element: true
-   Workspace settings: There SHALL be only one workspace. The \<title\>
    element of the workspace SHALL be the community\_name from the
    *network* *community* *description* *data* *model*. If the
    community\_name is missing, the value SHALL be the community\_id
    from the *network* *community* *description* *data* *model.*
-   Collection settings: There SHALL be only one collection.
    -   IRI (http attribute): URL of the network node
    -   \<title\> element: The title of the collection SHALL be the
        node\_name from the *network* *node* *description* *data*
        *model*. If the node\_name is missing, the value SHALL be the
        node\_id from the *network* *node* *description* *data* *model*.
    -   \<accept\> element: application/json
    -   \<sword:mediation\> element: true
    -   \<dcterms:abstract\> element: The abstract SHALL be the
        node\_description from the *network* *node* *description* *data*
        *model*. If the node\_description is missing, the element SHALL
        be omitted.
    -   \<sword:collectionPolicy\> element MAY be present. The value is
        determined by the policies of the node, network or community
        (e.g., for the public Learning Registry community, the policy is
        the terms of service for the community,
        [<https://www.learningregistry.org/tos/>](https://www.learningregistry.org/tos/)
        )
    -   \<sword:treatment\> and \<sword:service\> elements SHALL be
        omitted.

##### API

##### SWORD: swordservice

> // return the service document

> Build XML results document
>
> EMIT the Atom Pub and SWORD namespace declarations
>
> EMIT the required elements
>
> ::: {.sourcecode}
> xml
>
> \<sword:version\>1.3\</sword:version\>
> \<sword:verbose\>true\</sword:verbose\>
> \<sword:noOp\>true\</sword:verbose\>
> :::
>
> EMIT the workspace elements
>
> ::: {.sourcecode}
> xml
>
> \<workspace\>
>
> :   \<atom:title\>community\_name or community\_id from the *network
>     community description data model*\<atom:title\>
> :::
>
> IF the \[on-behalf-of-user\] is permitted to publish to the node
>
> > THEN EMIT the collection elements
> >
> > ::: {.sourcecode}
> > xml
> >
> > \<collection href=\"URL of the network node\"\>
> >
> > :   \<atom:title\>node\_name or node\_id from the *network node
> >     description data model*\</atom:title\>
> >     \<accept\>application/json\</accept\>
> >     \<sword:mediation\>true\</sword:mediation\>
> >     \<dcterms:abstract\>node\_description from the *network node
> >     description data model*\</dcterms:abstract\>
> >     \<sword:collectionPolicy\>Policy URL\</sword:collectionPolicy\>
> >
> > \</collection\>
> > :::
>
> Complete XML elements
>
> ::: {.sourcecode}
> xml
>
> \</workspace\>
> :::
>
> > \</service\>

#### Create a Resource

> in a future draft of the specification

##### API

##### SWORD: swordpub

    // pseudo code

##### Service Description

```javascript
    {
        "doc_type": "service_description",
        "doc_version": "0.20.0",
        "doc_scope": "node",
        "active": true,
        "service_id": "<uniqueid>",
        "service_type": "publish",
        "service_name": "SWORD APP Publish V1.3",
        "service_description": "Service to publish resource description documents to a node using the SWORD 1.3 protocol",
        "service_version": "0.10.0",
        "service_endpoint": "<node-service-endpoint-URL>",
        "service_auth":
                                        // service authentication and authorization descriptions
        {
            "service_authz": ["<authvalue>"],
                                        // authz values for the service
            "service_key": < T / F > ,
                                        // does service use an access key
            "service_https": < T / F >
                                        // does service require https
        },
        "service_data":
        {
            "version": "1.3"
        }
    }
```

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
provided. Appropriate values for the service\_data elements SHALL be
provided. The descriptive values (service\_name, service\_description)
MAY be changed from what is specified herein.

### Basic Delete Service {#Basic Delete Service}

▼ The Basic Delete Service is deprecated 20130226. Use of a resource data description document with a \"replaces\" property to delete and replace existing resource data description documents.

The basic delete service \"deletes" an instance of a resource data
description document (or a set of documents) directly from a node in a
resource distribution network.

Each resource data description document identified in the supplied set
is deleted independently. In addition to the overall service return
indicating status, there SHALL be one returned object per resource data
description document, aligned 1:1 to the documents identified in the
supplied resource data description document array, indicating deletion
of the resource data description document.

The service MAY implement different deletion policies:

-   *ignore* \-- the deletion SHALL be acknowledged but the document is
    not deleted.
-   *mark* \-- the status of the document is changed to indicate that it
    has been deleted. The document SHALL NOT be returned by any access
    service.
-   *delete* \-- the document SHALL be deleted. What "deleted" means is
    dependent on the underlying implementation.
-   *purge* \-- the service SHALL, at some point, remove deleted
    documents.

*NB*: There are no restrictions on the size of a batch publish document
set, either in the number of elements or the total size of the HTTP
message. An implementation SHALL indicate any size limits in the service
description.

*NB*: Only the owner of a document may delete it.

*NB*: A mechanism to delete all resource data description documents
associated with a single resource identifier (resource locator) is not
provided since these resource data description documents may have
different owners.

*NB*: The deletion process SHALL be consistent with the
[Resource \<Resource Data Persistence\>]{role="ref"}
[Data \<Resource Data Persistence\>]{role="ref"}
[Persistence \<Resource Data Persistence\>]{role="ref"} policy.

#### API

#### Basic Delete

> [▼ The Basic Delete Service is deprecated 20130226. Use of a resource data description document with a \"replaces\" property to delete and replace existing resource data description documents.]{role="deprecation"}
>
> > // Obtain the resource data description document for each supplied
> > ID
>
> FOR EACH *resource* *data* *description* document ID
>
> > Put the *resource* *data* *description* document ID in the results
> > object
> >
> > IF the document does not exist
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"document doesn't exist\"
> > > >
> > > > SKIP
> >
> > IF the document has been deleted
> >
> > > THEN
> > >
> > > > OK := FALSE
> > > >
> > > > error := \"document already deleted
> > > >
> > > > SKIP
> > > >
> > > > > // otherwise delete
> >
> > OK := TRUE
> >
> > CASE delete\_action
> >
> > > ignore:
> > >
> > > > NO OP
> > >
> > > mark:
> > >
> > > > set a flag on the document that it is deleted
> > > >
> > > > :   // ACTIVE := FALSE
> > > >
> > > delete:
> > >
> > > > perform a system-level delete
> > > >
> > > > :   // whatever \"delete\" means
> > > >
> > > purge:
> > >
> > > > perform a system-level delete
> > > >
> > > > :   // whatever \"delete\" means
> > > >
> > > > trigger system level purge
> > > >
> > > > :   // may run at some later time
> > > >
#### Service Description

▼ The Basic Delete Service is deprecated 20130226. Use of a resource data description document with a \"replaces\" property to delete and replace existing resource data description documents.

```javascript
{
	"doc_type": "service_description",
	"doc_version": "0.20.0",
	"doc_scope": "node",
	"active": true,
	"service_id": "<uniqueid>",
	"service_type": "delete",
	"service_name": "Basic Delete",
	"service_description": "Delete Service",
	"service_version": "0.10.0",
	"service_endpoint": "<node-service-endpoint-URL>",
	"service_auth":
									// service authentication and authorization descriptions
	{
		"service_authz": ["<authvalue>"],
									// authz values for the service

		"service_key": < T / F > ,
									// does service use an access key

		"service_https": < T / F >
									// does service require https

	},

	"service_data":
	{
		"delete_action": "string",
									// fixed vocabulary ["ignore", "mark", "delete", "purge"]
									// ignore -- ignore the delete request
									// mark -- mark the document as deleted
									// delete -- delete the document from the document store
									// purge -- purge the document

		"doc_limit": integer,
									// specify the maximum number of documents in a batch

		"msg_size_limit": integer
									// specify the maximum message size
	}

}
```

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
provided. Appropriate values for the service\_data elements SHALL be
provided. The descriptive values (service\_name, service\_description)
MAY be changed from what is specified herein.

### Change Log

*NB*: The change log only lists major updates to the specification.

*NB*: Updates and edits may not results in a version update.

*NB*: See the [Learning \<../Technical\_Spec/index\>]{role="doc"}
[Registry \<../Technical\_Spec/index\>]{role="doc"}
[Technical \<../Technical\_Spec/index\>]{role="doc"}
[Specification \<../Technical\_Spec/index\>]{role="doc"} for prior
change history not listed below.

  ------------- ---------- ------------ ---------------------------------------------------------------------------------------------------------
  **Version**   **Date**   **Author**   **Change**

                20110921   DR           This document extracted from the monolithic V 0.24.0 document. [Archived copy (V
                                        0.24.0)](https://docs.google.com/document/d/1Yi9QEBztGRzLrFNmFiphfIa5EF9pbV5B6i9Tk4XQEXs/edit?hl=en_US)

  0.49.0        20110927   DR           Editorial updates to create stand alone version.Archived copy location TBD. (V PS:0.49.0)

  0.50.0        TBD        DR           Renumber all document models and service documents. Added node policy to control storage of attachments
                                        (default is stored). Archived copy location TBD. (V PS:0.50.0)

  Future        TBD                     Logging/tracking emit as paradata to services. Deprecate node\_timestamp. Details of attachments on
                                        publish, obtain, harvest.Archived copy location TBD. (V PS:x.xx.x)

  0.50.1        20130227   JK           Un-deprecated node\_timestamp. Amended Publishing algorithm to handle replacement documents. [Archive
                                        copy (V PS:0.49.0)](https://docs.google.com/document/d/1kgTyRk1kIM3QvfU2JB1C9ARMuL7fCqsba7mOLQ3IKlw/edit)
  ------------- ---------- ------------ ---------------------------------------------------------------------------------------------------------

### Working Notes and Placeholder Text
