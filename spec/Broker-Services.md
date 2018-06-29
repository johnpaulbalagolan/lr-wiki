Broker Services: Learning Registry Technical Specification V BS:0.50.1
======================================================================

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
one type of services and APIs deployable at nodes in a Learning Registry
Distribution Network.

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
    [Management \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}/[Administration \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}/[Discovery \<../Mgmt\_Admin\_and\_Discovery\_Services/index\>]{role="doc"}
-   [Learning \<../Operations/index\>]{role="doc"}
    [Registry \<../Operations/index\>]{role="doc"}
    [Operations \<../Operations/index\>]{role="doc"}

In particular, the reader needs to be aware that specific criteria for
the services and APIs are presented in the
[Data \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[Model \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[and \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[API \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[Attributes \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[and \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
[Behaviors \<../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index\>]{role="doc"}
part, the
[Resource \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
[Data \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
[Data \<../Resource\_Data\_Data\_Model/index\>]{role="doc"}
[Models \<../Resource\_Data\_Data\_Model/index\>]{role="doc"} part
describes the data that broker services process, and the
[Identity \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
[Trust \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
[Authentication \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"},
[Security \<../Identity\_Trust\_Auth\_and\_Security/index\>]{role="doc"}
part describes security requirements.

Broker Services {#Broker Services}
---------------

Broker services operate at a network node to process, transform,
augment, amplify or otherwise manipulate the resource data held at a
node. No broker services are currently defined. Broker services may be
defined in future drafts or versions of the specification.

#### Change Log

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

  0.50.0        20110926   DR           Editorial updates to create stand alone version.Archived copy location TBD. (V BS:0.50.0)

  Future        TBD                     Archived copy location TBD. (V BS:x.xx.x)

  0.50.1        20130312   JK           This document extracted from the Google Doc and converted to RestructuredText. [Archive Copy (V
                                        BS:0.50.0)](https://docs.google.com/document/d/1-dasdKJ_gDW-YEi4S7-g8ODGOp5To9xfXR-qbZVwt-Q/edit)
  ------------- ---------- ------------ ---------------------------------------------------------------------------------------------------------

Working Notes and Placeholder Text
----------------------------------
