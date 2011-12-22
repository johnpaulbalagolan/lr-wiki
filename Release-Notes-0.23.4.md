The plan below is for the upcoming new year 2012 release scheduled for Friday, 1/6/2012.  Last release was LR v0.23.3 on October 27.

## Proposed process

1.  Run smoke screen tests on alpha
2.  Define the version number for the release based on the version of the spec the code best aligns with
3.  Create a new tag for the release in github based on the assigned version number
4.  Release to production
5.  Send email describing release to all LR Google Groups

## Pending pull requests

1.  Fix for issue #152
2.  Fixed OPTIONS method bug
3.  Jmeter Functional Tests (Service Description and Policy Data Model)

## Pending bugs

> See https://github.com/LearningRegistry/LearningRegistry/issues

* Open #152 - 404 page returned as plaintext
* Open #151 - Fixed OPTIONS method bug
* Open #143 - Incorrect service_endpoint for SWORD Publish, Resource Distribution Network Policy (sword is fixed on alpha, but not policy)
* Open #142 - "service_authz" is null for SWORD Publish, Resource Distribution Network Policy
* Open #119 - "keycount" needs to be removed (JB says it has been fixed, but doesn't appear so on alpha)
* Open #118 - Slice returns wrong resultCount (What is the explanation?  Jim's explanation about flow control doesn't seem to fit.)
* Open #94 - Status does not support last_in_sync and sync_in_node (is this a bug or a feature request?)
* Open #81 - TypeError for 'use_cookies' when accessing /harvest

## Closed bugs since last release 

> See https://github.com/LearningRegistry/LearningRegistry/issues?sort=created&direction=desc&state=closed&page=1

* Fixed #152 in Merge #155 - 404 page returned as plaintext
* Fixed #108 in Merge #109 - Proposed fix for issue #37 causes OAI-PMH to fail
* Fixed #140 in Merge #141 - OAI-PMH test suite failing
* Fixed #37 - OAI-PMH cannot disseminate format when <!DOCTYPE ...> declaration is present in payload.

## Documentation

> See https://github.com/LearningRegistry/LearningRegistry/wiki

* Windows install guide updated
* Linux install guide updated
* Mac OSX install guide updated
* Examples for paradata, assertions, and queries

## Servers Updated

> See https://github.com/LearningRegistry/LearningRegistry/wiki/nodes

* http://sandbox.learningregistry.org replaces http://test01.learningregistry.org and is now running 0.23.4
* http://alpha.learningregistry.org replaces http://test02.learningregistry.org and is from now on running the latest stable master.