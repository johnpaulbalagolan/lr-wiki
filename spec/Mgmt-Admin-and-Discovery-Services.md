Management, Administrative and Discovery Services: Learning Registry Technical Specification V MS:0.50.1
========================================================================================================

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
the basic Learning Registry services used to manage, administer and
perform discovery in a distribution network.

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
    [Publish \<../Publish\_Services/index\>]{role="doc"},
    [Access \<../Access\_Services/index\>]{role="doc"},
    [Broker \<../Broker\_Services/index\>]{role="doc"}
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
part describes the network model and the
[Identity \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
[Trust \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
[Authentication \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
[Security \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"}
part describes security requirements.

Administrative Services {#Administrative Services}
-----------------------

Administrative services are used to trigger network node administrative
operations, to determine node status or to retrieve descriptive
information about a network node. They are used to support monitoring
and discovery. Future drafts or versions of this specification MAY
define additional administrative services. Future drafts or versions of
this specification MAY define additional service query arguments that
will customize the returned data.

*NB*: Provisioning administrative services is optional. They SHOULD NOT
be relied on for resource distribution network operations.

*Open Question*: Do we need to have separate services to return node
filters (now part of the general node description) or node connectivity
(currently not retrievable).

All administrative services SHALL support HTTP content negotiation. All
administrative services SHALL support return of CONTENT-TYPE:
text/plain. All administrative services SHOULD support return of
text/html, text/xml, application/rdf+xml.

### Network Node Status Service {#Network Node Status Service}

The network node status service is used to return information and
operational data about a network node. The service SHALL return all of
the key-value pairs listed that have a valid value. The service MAY
return additional key-value pairs that indicate status.

A network node SHALL maintain all of the data necessary to return the
required key-value pairs.

#### API

#### Network Node Status

> // Return the operational status of a network node
>
> DEFINE VIEW on
>
> > *network node description* document containing the required fields
> >
> > -   *network node operational* data containing the required fields
>
> QUERY
>
> TRANSFORM results to specified CONTENT-TYPE

#### Service Description

```javascript
    {
        "doc_type": "service_description",
        "doc_version": "0.20.0",
        "doc_scope": "node",
        "active": true,
        "service_id": "<uniqueid>",
        "service_type": "access",
        "service_name": "Network Node Status",
        "service_description": "Service to retrieve basic operational status information for a node",
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
        }
    }
```

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
provided. The descriptive values (service\_name, service\_description)
MAY be changed from what is specified herein.

### Network Node Description Service {#Network Node Description Service}

The network node description service is used to return descriptive
information about a network node, the resource distribution network that
it is a part of and the network community that it is a part of. The
service SHALL return all of the key-value pairs listed that have a valid
value. An implementation MAY omit the return of any key-value pair that
is an optional key-value pair in a
[Network Data Model \<Network Data Models\>]{role="ref"} for which a
value is missing or NULL. The service MAY return additional
informational values.

#### API

#### Network Node Description

> // Return the description of a network node
>
> DEFINE VIEW on
>
> > *network node description* document containing the required output
> > fields
> >
> > -   *resource distribution network description* document containing
> >     the required output fields
> > -   *resource distribution network policy* document containing the
> >     required output fields
> > -   *network community description* document containing the required
> >     output fields
> > -   *network node filter description* document containing the
> >     required output fields
>
> QUERY
>
> TRANSFORM results to specified CONTENT-TYPE

#### Service Description

    {

        "doc_type": "service_description",

        "doc_version": "0.20.0",

        "doc_scope": "node",

        "active": true,

        "service_id": "<uniqueid>",

        "service_type": "access",

        "service_name": "Network Node Description",

        "service_description": "Service to retrieve a comprehensive description of a node",

        "service_version": "0.23.0",

        "service_endpoint": "<node-service-endpoint-URL>",

        "service_auth":
                                        // service authentication and authorization descriptions

            {"service_authz": ["<authvalue>"],
                                        // authz values for the service

            "service_key": < T / F > ,
                                        // does service use an access key

            "service_https": < T / F >
                                        // does service require https

            }

    }

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
provided. The descriptive values (service\_name, service\_description)
MAY be changed from what is specified herein.

### Network Node Services Service {#Network Node Services Service}

The network node services service is used to return the list of services
available at a network node. For each service at a node, the service
SHALL return all of the key-value pairs listed that have a valid value.
An implementation MAY omit the return of any key-value pair that is an
optional key-value pair in a
[Network Data Model \<Network Data Models\>]{role="ref"} for which a
value is missing or NULL. The service MAY return additional key-value
pairs for a service.

The service SHOULD group and sort the results in some logical form,
e.g., by ACTIVE, by TYPE.

#### API

#### Network Node Services

> // Return the description of network node services
>
> DEFINE VIEW on
>
> > *network node description* document containing the required output
> > fields
> >
> > -   ALL *network node service description* documents containing the
> >     required output fields
> >
> > GROUPED and ORDERED on service attributes.
>
> QUERY
>
> TRANSFORM results to specified CONTENT-TYPE

#### Service Description

```javascript
    {
        "doc_type": "service_description",
        "doc_version": "0.20.0",
        "doc_scope": "node",
        "active": true,
        "service_id": "<uniqueid>",
        "service_type": "access",
        "service_name": "Network Node Services",
        "service_description": "Service to retrieve the list of services deployed at a node",
        "service_version": "0.21.0",
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
            }
    }
```

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
provided. The descriptive values (service\_name, service\_description)
MAY be changed from what is specified herein.

### Resource Distribution Network Policy Service {#Resource Distribution Network Policy Service}

The resource distribution network policies service is used to return
information about the policies that apply to the resource distribution
network that the network node is a part of. The service SHALL return all
of the key-value pairs listed that have a valid value. An implementation
MAY omit the return of any key-value pair that is an optional key-value
pair in a [Network Data Model \<Network Data Models\>]{role="ref"} for
which a value is missing or NULL. The service MAY return additional
policy key-value pairs. The service MAY be called at any node in the
resource distribution network; all network nodes store an identical copy
of the policy data.

#### API

#### Resource Distribution Network Policy

> // Return the description of network policies
>
> DEFINE VIEW on
>
> > *network node description* document containing the required output
> > fields
> >
> > -   *resource distribution network description* document containing
> >     the required output fields
> > -   *resource distribution network policy* document containing the
> >     required output fields
>
> QUERY
>
> TRANSFORM results to specified CONTENT-TYPE

#### Service Description

```javascript
    {
        "doc_type": "service_description",
        "doc_version": "0.20.0",
        "doc_scope": "node",
        "active": true,
        "service_id": "<uniqueid>",
        "service_type": "access",
        "service_name": "Resource Distribution Network Policy",
        "service_description": "Service to retrieve network policies from a node",
        "service_version": "0.21.0",
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
            }
    }
```

When the service is deployed at a node, appropriate values for the
placeholders (service\_id, service\_endpoint, service\_auth) SHALL be
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

  0.49.0        20110927   DR           Editorial updates to create stand alone version.Archived copy location TBD. (V MS:0.49.0)

  0.50.0        TBD        DR           Renumber all document models and service documents. Added node policy to control storage of attachments
                                        (default is stored). Archived copy location TBD. (V MS:0.50.0)

  Future        TBD                     Archived copy location TBD. (V MS:x.xx.x)

  0.50.1        20130312   JK           This document extracted from original Google Doc and converted to RestructuredText. [Archived copy (V
                                        MS:0.49.0)](https://docs.google.com/document/d/1lATgircOBUOmsoFwia8su2o--TZ88AG4GOmn5NQ6jAc/edit)
  ------------- ---------- ------------ ---------------------------------------------------------------------------------------------------------

### Working Notes and Placeholder Text
