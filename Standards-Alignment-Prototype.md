## Priorities

1. Get data services working (project elements described below) 
   1. Just get alignment data going (Jim and Walt)
   1. All the features discussed (e.g., other languages, restricted access) (Jim, Walt, and Austin)
1. Get a trimmed down node running w/out slice -- ready for development. Install data services on it - show it works. (Lou)
   1. Modify install should map services and associated view dependencies, so that if xyz services are installed, only xyz views are installed
1. Prove out test cases on this work (Joe, Susan, Aaron, Agilix)
1. Get docs in shape for examples and code lib (Damon, Simulator)
1. Get one more example data service going: maybe ratings (Jim)
1. Get replicate working better (Lou/John)
   1. Make replication meet the goals of the spec (security, data integrity) -- clarify anything in the code or spec that is not clear
      1. Consider Jim's idea of using incoming databases and conditional change monitor behavior (address security, data integrity, and duplicate document/disk space issues)
      1. Consider pull replication via Jim's idea to develop a service that allows a node to subscribe for push from a different node
1. Get publish signing on a node working (Austin)

## Development Approach

* Rapid prototyping producing documentation on GitHub wiki
* Separate branch for standards alignment prototyping using pull request model
* Part of the asynchronous development process is writing tests and doing code reviews

### Design Goal: Reduce Server Cost, Improve Performance, Reduce Resource Allocation

Reducing size of data and cost/size of server

* Data results window size needs to be small
* Going to Amazon [Elastic Block Storage (EBS)](http://aws.amazon.com/ebs/) for disk storage

### Design Goal: Simplicity

* Every step can be done with curl

### Tests

* Unit tests for components (may be language specific, using new or existing frameworks - should be callable from our overall test runner)
* Integration/functional tests (use our existing framework)

## Prototype Elements and Associated PT Stories

### Map/Extraction Functions: Standards Alignment

Provide these capabilities (maybe one per view or maybe integrated):

* Give me all standards aligned to URL/resource
* Give me all URLs associated with a standard
* Give me all alignment data
* Give me all aligned resources for a URL pattern / site

> 1.1 Story (Jim): [What defines "alignment data"?](https://www.pivotaltracker.com/story/show/24774751)

* Anything that starts with "http://purl.org/ASN/resources/*"
* XML with dct:conforms_to
* Criteria for relevant paradata (specific verbs for paradata)
* validate with Joe and Brian to identify rules of thumb
* define regex
* wiki article

> 1.1 Story (Jim): [How do we organize (pattern) the data so it can be accessed in a consistent manner](https://www.pivotaltracker.com/story/show/24785323)

* by date
* by sender
* by domain name (identity)
* by url
* by standard
* related to API format definition

> 1a Story (Jim): [How to use the Java View Server to write the map functions?](https://www.pivotaltracker.com/story/show/24785651)

* How to setup Maven
* Java
* not rich query interface
* source code repository for views?
* wiki article

> 1.2 Story: [How to use the JavaScript to write the map functions?](https://www.pivotaltracker.com/story/show/24785905)

* Javascript
* not rich query interface
* wiki article

### Calling / API Format

Use restful-like interface but modified to support parameters

* Call it "extract"
* Parameters include: Which map/extract to run, primary param (URL of resource or whatever), secondary params (provided after "?")
* Security / access
   * Each map/extract design doc needs to hold an arbitrary parameter that describes if the map/extract is permitted to be accessed from the "extract" interface (extract must honor this)
   * Possibly also enable access from "extract" by convention of naming the map/extract view function with a particular prefix like "view-[name]" (e.g., "view-by-standards-url")
* Example:
   * Model: http://lr-node/extract/[view-name]/[primary-parameter]?sender=[value]
   * Live: http://lr-node/extract/view-by-standards-url/http%3A%2F%2Fwww.youtube.com%3Fv%3Dxyzabc?sender=http%3A%2F%2Fpool.sks-keyservers.net%3A11371%2Fpks%2Flookup%3Fop%3Dget%26search%3D0xBFF13965146B1740

> 1.1 Story (Walt/Jim): [What is the API definition?](https://www.pivotaltracker.com/story/show/24775061)

* related to organize (pattern) data story
* leverage CouchDB tools, but abstract the API to use them (e.g., how to use CouchDB List function/view/regex, so we may need abstract a way to pass arbitrary parameters (e.g., domain name regex) through API to a CouchDB List?)
* unrestricted, but obivously no access to internal views

> 6 Story (Austin, LM security): [Define how to restrict access to the API](https://www.pivotaltracker.com/story/show/24786655)

* Define security
   * Each map/extract design doc needs to hold an arbitrary parameter that describes if the map/extract is permitted to be accessed from the "extract" interface (extract must honor this)
   * Possibly also enable access from "extract" by convention of naming the map/extract view function with a particular prefix like "view-[name]" (e.g., "view-by-standards-url")
   * role-based access (single role initially as discriminator)?
* document in wiki

> 6 Story (Austin): [How to restrict access to the API?](https://www.pivotaltracker.com/story/show/24786785)

* Implement security
   * Each map/extract design doc needs to hold an arbitrary parameter that describes if the map/extract is permitted to be accessed from the "extract" interface (extract must honor this)
   * Possibly also enable access from "extract" by convention of naming the map/extract view function with a particular prefix like "view-[name]" (e.g., "view-by-standards-url")
   * role-based access

### Result Formats

* Use obtain result format
   * NOTE: Dan suggests that a new result format is not required/desirable. 
   * Relax certain LR envelope elements for output by creating a new envelope doc_type: "result_data"
   * "result_data" doc_type would have compatibility with "resource_data" but used for returning data which are composites of inputs
* Design goals include:
   * Ability to chain result sets together
   * Optional/bonus: Ability to submit result_data docs back into LR network

> 1.1 Story (Walt, Dan): [What is the result format for the service?](https://www.pivotaltracker.com/story/show/24774765)

* model obtain
* wiki article 

> 1.1 Story (Walt, Dan): [What is the result format for the envelope?](https://www.pivotaltracker.com/story/show/24774019)

* NOTE: Dan suggests new doc_type not a good idea..
* model after resource_data, but with relaxed element definitions
* doc_type="result_data"
* wiki article

### Filter Functions: Standards Alignment and/or General Purpose

* Examine whether performance requires some filters to be map/extractions.
   * Filter by sender
   * Filter by date

> Addressed in above 1a story (organize data, API definition)

### View Server

* Templates for view
   * Helper functions and other templatizing tools
   * How-to examples
* Java view server
   * Performance: make sure >= javascript view server
* Maybe provide javascript view servers templates as learning examples

> 4 Story (Jim): Provide example map functions in simulator

> 4 Story (TBD): Host simulator

## Second Project: Submission Envelopes Signing by Nodes

### Signing Submissions via Node

* Wizard for creating public/private keys and uploading to key servers
* Associate public/private keys to basic_auth login users
* Signing code on submission inside node
   * Could sign all stuff with a single node public/private key and associate basic_auth credentials as "signed on behalf of"