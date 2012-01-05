The plan below is for the upcoming new year 2012 release scheduled for Wednesday, 1/11/2012.  The previous release was LR v0.23.3 on October 27, 2011.

## New Features

1.  Support for CouchDB 1.1
2.  Support for uwsgi

## Bug Fixes

> See https://github.com/LearningRegistry/LearningRegistry/issues?sort=created&direction=desc&state=closed&page=1

* Distribute call not working: distribute_threshold_handler.py lost reference to json (#154)
* "service_type" is missing on startup (#146)
* Service description does not reflect service_https value (#125)
* Service documents "service_endpoint" does not match spec definition (#34)
* Node admin email address is not correct (#123)
* Ensure same encoding is used for all resource locators (#136)
* OAI-PMH cannot disseminate format when <!DOCTYPE ...> declaration is present in paylod (#37)
* Missing service_type for access services (#132)
* Harvest returns 500 error when no results are found (#128)
* Slice indexing issue with caps in paradata schema (#127)
* Increased slice accuracy and new slice indexing (#126)
* COUCH_DOWN_URL variable in setup script for x86 systems (#121)
* Publish service allowing create_timestamp and update_timestamp values (#120)
* "keycount" field should be removed from slice result object (#119)
* Missing publish service data in setup_node.py (#116)

## Documentation

> See https://github.com/LearningRegistry/LearningRegistry/wiki

* Windows install guide updated
* Linux install guide updated
* Mac OSX install guide updated
* Examples for paradata, assertions, and queries

## Servers Updated

> See https://github.com/LearningRegistry/LearningRegistry/wiki/nodes

* **Sandbox** (http://sandbox.learningregistry.org) replaces **Test01** and is now running 0.23.4
* **Alpha** (http://alpha.learningregistry.org) replaces **Test02** and is from now on running the latest stable master.

## Updated development process and improved testing

Updated development process is documented here: 

> https://github.com/LearningRegistry/LearningRegistry/wiki/Contributing-to-the-Learning-Registry

New tests added for sword publish, distribute, OAI-PMH, service descriptions, and service policies.