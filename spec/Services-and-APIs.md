Services and APIs: Learning Registry Technical Specification V SA:0.50.1
========================================================================

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
It is an introduction to the Learning Registry services.

This document is not standalone. The reader should be familiar with
other parts of the specification, including, but not limited to:

-   [General Matter \<../General\_Matter/index\>]{role="doc"}, including
    Licenses, Notation, Versioning, Glossary, References
-   [Resource Distribution Network Model \<../Resource\_Distribution\_Network\_Model/index\>]{role="doc"}
-   [Resource Data Data Models \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
-   [Identity, Trust, Authentication, Security \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"}
-   [Data Model and API Attributes and Behaviors \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
-   [Learning \<../Operations/index\>]{role="doc"}
    [Registry \<../Operations/index\>]{role="doc"}
    [Operations \<../Operations/index\>]{role="doc"}

Different types of services are detailed independently.

-   [Distribution \<../Distribution\_Services/index\>]{role="doc"}
-   [Publish \<../Publish\_Services/index\>]{role="doc"}
-   [Access \<../Access\_Services/index\>]{role="doc"}
-   [Broker \<../Broker\_Services/index\>]{role="doc"}
-   [Management \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}/[Administration \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}/[Discovery \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}

Services and APIs
-----------------

The services and their APIs provide the functionality that edge node
producer and consumer agents use to push resource data into the
distribution network and to discover and pull resource data from the
network. They also define how to distribute the resource data throughout
a network and how to manage, discover and observe resource distribution
network behavior.

The specification defined types of services follows. Any non gateway
node MAY provide any of these services. A node MAY provide additional
services not specified herein.

-   [Distribution \<../Distribution\_Services/index\>]{role="doc"}
    -   [Resource Data Distribution Service \<Resource Data Distribution Service\>]{role="ref"}
-   [Publish \<../Publish\_Services/index\>]{role="doc"}
    -   [Basic Publish Service]{role="ref"}
    -   [Basic Delete Service]{role="ref"}
-   [Access \<../Access\_Services/index\>]{role="doc"}
    -   [Basic Obtain Service]{role="ref"}
    -   [Basic Harvest Service]{role="ref"}
    -   [OAI-PMH Harvest Service]{role="ref"}
-   [Broker \<../Broker\_Services/index\>]{role="doc"} \-- none
    currently defined
-   [Management \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}/[Administration \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}/[Discovery \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}
    -   [Network Node Status Service]{role="ref"}
    -   [Network Node Description Service]{role="ref"}
    -   [Network Node Services Service]{role="ref"}
    -   [Resource Distribution Network Policy Service]{role="ref"}

*NB*: There is no mechanism to reserve names for APIs, tag them as
authoritative (i.e., they are defined in this specification), etc. A
future version of the specification MAY extend the service definition to
include tags (e.g., authoritative, experimental, third-party) and other
validation or conformance information.

Services and APIs are RESTful and bound to a particular node in the
resource distribution network. Service descriptions include the API call
(HTTP binding), the API arguments, the message payload (using the
JSON-like notation), the service results (using JSON-like notation),
error codes, an informative pseudo code description of a *possible*
implementation, and the network node service description data.

The
[Network Node Service Description Data Model \<Network Node Service Description Data Model\>]{role="ref"}
provides a machine and human readable description of the service; an
instance of the description document is stored at the node that provides
the service.

Additional constraints on API attributes, HTTP bindings (headers, HTTP
errors), error processing and behaviors are described in the
[Data Model and API Attributes and Behaviors \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
part of the specification.

Except as noted, services SHALL NOT be required to be provisioned at a
node. An implementation SHALL NOT assume the provision of any service at
any node, i.e., the implementation of one service cannot rely upon
another service.

▲Except as noted, services SHALL be fully independent; the
implementation and provisioning of a service at a node SHALL NOT assume
that any other service is deployed at the node.

#### Change Log

*NB*: The change log only lists major updates to the specification.

*NB*: Updates and edits may not results in a version update.

*NB*: See the
[Learning Registry Technical Specification \<../Technical\_Spec/index\>]{role="doc"}
for prior change history not listed below.

  ------------- ---------- ------------ ---------------------------------------------------------------------------------------------------------
  **Version**   **Date**   **Author**   **Change**

                20110921   DR           This document extracted from the monolithic V 0.24.0 document. [Archived copy (V
                                        0.24.0)](https://docs.google.com/document/d/1Yi9QEBztGRzLrFNmFiphfIa5EF9pbV5B6i9Tk4XQEXs/edit?hl=en_US)

  0.50.0        20110927   DR           Editorial updates to create stand alone version. Clarify non dependence of service deployment.Archived
                                        copy location TBD. (V SA 0.50.0)

  Future        TBD                     Archived copy location TBD. (V SA:x.xx.x)

  0.50.1        20130312   JK           This document extracted from Google Doc and converted to RestructuredText. [Archive copy (V
                                        SA:0.50.0)](https://docs.google.com/document/d/1RGRnuaQ9YFsWLExPnrQRGEgZT5fx000nGGo-PKeFLrY/edit)
  ------------- ---------- ------------ ---------------------------------------------------------------------------------------------------------

Working Notes and Placeholder Text
----------------------------------
