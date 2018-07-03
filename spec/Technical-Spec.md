# Learning Registry Technical Specification V 0.51.0

See the [Change Log](#change-log) for links to prior stable versions.

<span style="background-color:#d9ead3">Major changes and additions from the prior version (0.50.1) are marked with ▲.</span>

Significant deletions use <span style="color:#cc0000">~~strikethrough text~~</span>.

<span style="background-color:#ffe599">Features to be deprecated in a future version are indicated with ▼.</span>

**This document is the whole of the Learning Registry Technical Specification.**

## Technical Specification Introduction

This document provides the technical specification for the Learning
Registry. It specifies the network model, data models and APIs. It does
not specify policy-based operational procedures or the instantiation or
deployment of the Learning Registry. It does not specify internal data
models or internal APIs. The specification focuses on the APIs used by
external agents and the data models and APIs required for overall
operations of a network and general interoperability of external agents.
While targeted at a document-oriented infrastructure, the specification
itself is independent of any particular toolset. The document is
currently a work in progress; its structure, organization and content
are subject to change.

## Technical Specification Contents

- [1. General Matter: Learning Registry Technical Specification - V GM:0.51.0](/General_Matter/index)
  - [1.1. Learning Registry Overview](/General_Matter/index#learning-registry-overview)
  - [1.2. Specification License](/General_Matter/index#specification-license)
  - [1.3. Notation](/General_Matter/index#notation)
  - [1.4. Conformance](/General_Matter/index#conformance)
  - [1.5. Specification Versioning](/General_Matter/index#specification-versioning)
  - [1.6. Technical Specification Overview](/General_Matter/index#technical-specification-overview)
    - [1.6.1. Design Principles](/General_Matter/index#design-principles)
  - [1.7. Glossary](/General_Matter/index#glossary)
  - [1.8. References](/General_Matter/index#references)
  - [1.9. Change Log](/General_Matter/index#change-log)
  - [1.10. Working Notes and Placeholder Text](/General_Matter/index#working-notes-and-placeholder-text)
- [2. Resource Distribution Network Model: Learning Registry Technical Specification V NM:0.50.1](/Resource_Distribution_Network_Model/index)
  - [2.1. Resource Distribution Network Model](/Resource_Distribution_Network_Model/index#resource-distribution-network-model)
    - [2.1.1. Network Nodes and Node Services](/Resource_Distribution_Network_Model/index#network-nodes-and-node-services)
    - [2.1.2. Network Topology](/Resource_Distribution_Network_Model/index#network-topology)
    - [2.1.3. Network Data Models](/Resource_Distribution_Network_Model/index#network-data-models)
    - [2.1.4. Network Description](/Resource_Distribution_Network_Model/index#network-description)
  - [2.2. Change Log](/Resource_Distribution_Network_Model/index#change-log)
  - [2.3. Working Notes and Placeholder Text](/Resource_Distribution_Network_Model/index#working-notes-and-placeholder-text)
- [3. Resource Data Data Model: Learning Registry Technical Specification V RM:0.51.0](/Resource_Data_Data_Model/index)
  - [3.1. Resource Data Data Models](/Resource_Data_Data_Model/index#resource-data-data-models)
    - [3.1.1. Resource Data Description Data Model](/Resource_Data_Data_Model/index#resource-data-description-data-model)
    - [3.1.2. Metadata Formats](/Resource_Data_Data_Model/index#metadata-formats)
    - [3.1.3. Paradata Formats](/Resource_Data_Data_Model/index#paradata-formats)
    - [3.1.4. Resource Data](/Resource_Data_Data_Model/index#resource-data)
    - [3.1.5. Tombstones](/Resource_Data_Data_Model/index#tombstones)
  - [3.2. Change Log](/Resource_Data_Data_Model/index#change-log)
  - [3.3. Working Notes and Placeholder Text](/Resource_Data_Data_Model/index#working-notes-and-placeholder-text)
- [4. Identity, Trust, Auth and Security: Learning Registry Technical Specification V IT:0.51.0](/Identity_Trust_Auth_and_Security/index)
  - [4.1. Identity and Digital Signatures](/Identity_Trust_Auth_and_Security/index#identity-and-digital-signatures)
    - [4.1.1. Signing a Resource Data Description Document](/Identity_Trust_Auth_and_Security/index#signing-a-resource-data-description-document)
    - [4.1.2. Validation the Signature of a Resource Data Description Document](/Identity_Trust_Auth_and_Security/index#validation-the-signature-of-a-resource-data-description-document)
  - [4.2. Authorization and Authentication](/Identity_Trust_Auth_and_Security/index#authorization-and-authentication)
    - [4.2.1. Authentication](/Identity_Trust_Auth_and_Security/index#authentication)
    - [4.2.2. Authorization](/Identity_Trust_Auth_and_Security/index#authorization)
    - [4.2.3. Network Communications Security](/Identity_Trust_Auth_and_Security/index#network-communications-security)
    - [4.2.4. Network Ports](/Identity_Trust_Auth_and_Security/index#network-ports)
  - [4.3. Trust](/Identity_Trust_Auth_and_Security/index#trust)
  - [4.4. Security and Information Assurance](/Identity_Trust_Auth_and_Security/index#security-and-information-assurance)
  - [4.5. Change Log](/Identity_Trust_Auth_and_Security/index#change-log)
  - [4.6. Working Notes and Placeholder Text](/Identity_Trust_Auth_and_Security/index#working-notes-and-placeholder-text)
../Data\_Model\_and\_API\_Attributes\_and\_Behaviors/index
../Services\_and\_APIs/index ../Distribution\_Services/index
../Publish\_Services/index ../Access\_Services/index
../Broker\_Services/index ../Mgmt\_Admin\_and\_Discovery\_Services/index
../Operations/index
:::

#### Change Log

*NB*: The change log only lists major updates to the specification.

*NB*: Updates and edits may not results in a version update.

*NB*: See the individual partsg of the Technical Specification for specific changes to that part.

| **Version** | **Date** | **Author** | **Change** |
|:-----------:|:--------:|:----------:|:----------:|
| 0.10.0 | 20110117 | DR | Initial public release (lacks resource data model). [Archived copy (V 0.10.0)](https://docs.google.com/document/d/1mJhXzZTwF7S8lfuV0j0axJJCahLDtGCZtCaeeB81x7Q/edit?hl=en)
| 0.15.0 | 20110222 | DR | Added filtering. Added basic harvest. Added resource data model. Added basic delete. [Archived copy (V 0.15.0)](https://docs.google.com/document/d/1LGwYxEqSRe4tdV4at6x8WWXI7nfXMGoY4x3kO5UqIgY/edit?hl=en)
| 0.16.0 | 20110310 | DR | Added OAI-PMH harvest. Obtain extended to support by doc\_ID or by resource\_ID/locator access. Documented Obtain. Basic Harvest extended to support doc\_ID or by resource\_ID/locator access for GetRecord. [Archived copy (V 0.16.0)](https://docs.google.com/document/d/1em8LdbX9tkvB66yqoe96MNKdAWTyt_lMSQjyzAREYWg/edit?hl=en)
| 0.17.0 | 20110415 | DR | Clarified that services are optional, described operational requirements to provision services. Revised XSD to support OAI-PMH harvest by resouce\_ID. Clarified times are UTC 0. Clarified distributeAPI to uncouple it from other APIs. Add ToS checks to distribute and publish. Update reource doc to include ToS attribution. Added SWORD API. [Archived copy (V 0.17.0)](https://docs.google.com/document/d/1UyN_cacpCz4Xj8G4XEGcnzAC57hS3UZyng6aJGtvXdM/edit?hl=en)
| 0.20.0 | 20110422 | DR | Added digital signature k-v pairs to resource documents. Added public key k-v pairs to all description documents. Updated network and node policy descripitons. Added signature, trust, \... verification to publish. Added identity section. Defined ALL behavior for obtain for size limited. Defined returning spec JSON vs. stored JSON for obtain and harvest. Authn (none, basic, SSH, Oauth, \...). Authz (access keys). [Archived copy (V 0.20.0)](https://docs.google.com/document/d/1wd_mwuFubtZsUS6p9_nyAgabzldf1bfhITN3sRlw7sc/edit?hl=en)
| 0.21.0 | 20110706 | DR | Updated how to sign documents. Modified resource document description to restructure identity. Added JSONP to APIs. Obtain flow control (to be moved to a common location to add to other APIs). [Archived copy (V 0.21.0)](https://docs.google.com/document/d/1jREjZ9N9Bzifn_kWy2rmGNe6E1nx3B7vmG6k_Cjg6n8/edit?hl=en_US)
| 0.22.0 | 20110708 | DR | Made resource doc type an open vocabulary. Added trust weight. Added requirement that a service document exist for a service. [Archived copy (V 0.22.0)](https://docs.google.com/document/d/1SW3ILArsGOOp1MmMzUnRuHw8R-JZfj7j79-w5sHDzT0/edit?hl=en_US)
| 0.23.0 | 20110921 | DR | Added k-v pair to mark documents as non distributable and process to block publication and distribution (take down process is policy, not part of the specification. Added checks on max doc size. Indicated that node time stamp is to be depricated. Indicated services to be deprecated. Documented obtain get interface. [Archived copy (V 0.23.0)](https://docs.google.com/document/d/1fRbDpM0BKvNc4WzDzX0pNUpfPtFAsKpKGnOyRhRok-8/edit?hl=en_US)
| 0.24.0 | 20110921 | DR | Remove deprecated servcies (query, SRW, Sitemap). [Archived copy (V 0.24.0)](https://docs.google.com/document/d/1Yi9QEBztGRzLrFNmFiphfIa5EF9pbV5B6i9Tk4XQEXs/edit?hl=en_US)
| NA     | 20110921 | DR | This document extracted from the monolithic V 0.24.0 document.Archived copy NA
| 0.49.0 | 20110927 | DR | Changed license from OWA CLA 0.9 to OWA CLA 1.0. Added GM section on versioning.Archived copy location TBD (V 0.49.0)
| Future | TBD      |    | Add service code version to service documents (extracted from code on install). Renumber all documentmodels and service documents. Added node policy to control storage of attachments (default is stored). Add page size as service doc setting with flow control.Archived copy location TBD (V x.xx.x)
| Future | TBD      |    | ToS attribution output to OAI. Harvest flow control. Flow control to OAI. Logging/tracking emit as paradata to services. Assertion (relation/sameas) and trust documents. Deduplication service. RESTful APIs. Details of attachments on publish, obtain, harvest. Depricate node\_timestampArchived copy location TBD (V x.xx.x)
| Future | TBD      |    | XXXArchived copy location TBD (V x.xx.x)
| 0.50.1 | 20130312 | JK | Converted spec source format to RestructuredText. node\_timestamp removed from deprecation. [Archive copy (V 0.5x.x)](https://docs.google.com/document/d/191BTary350To_4JokBUFZLFRMOEfGYrl_EHE6QZxUr8/edit)
| 0.51.0 | 20140219 | jH | Updated version number and shading of changes only. Updates to the spec are in the [Resource Data Data Model](/Resource\_Data\_Data\_Model/index)

## Working Notes and Placeholder Text
