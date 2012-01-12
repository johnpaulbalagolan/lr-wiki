LR version 0.23.4 was released on January 11, 2012.  The production and sandbox servers are now running LR version 0.23.4.

This release consists primarily of bug fixes and updates responding to community feedback.  There are no expected changes required for users.  Services should perform as expected.  However, the slice service is temporarily returning 0 results while the index is being rebuilt following the update.  LR v0.23.4 conforms to the LR technical specification v0.23.  These release notes are available from: https://github.com/LearningRegistry/LearningRegistry/wiki/Release-Notes-0.23.4

## Changes

> See https://github.com/LearningRegistry/LearningRegistry/issues?sort=created&direction=desc&state=closed&page=1

Highlighted changes include:

* Added support for OPTIONS calls and cross origin requests (CORS) (#151)
* Slice indexing issue with caps in paradata schema (#127)
* Increased slice accuracy and new slice indexing (#126)
* Ensure same encoding is used for all resource locators (#136)
* OAI-PMH cannot disseminate format when <!DOCTYPE ...> declaration is present in paylod (#37)
* Harvest returns 500 error when no results are found (#128)
* Distribute call not working: distribute_threshold_handler.py lost reference to json (#154)
* "service_type" is missing on startup (#146)
* Service description does not reflect service_https value (#125)
* Service documents "service_endpoint" does not match spec definition (#34)
* Fixed content type for error pages (#152)
* Node admin email address is not correct (#123)
* Missing service_type for access services (#132)
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

* Production 1: http://node01.public.learningregistry.net
* Production 2: http://node02.public.learningregistry.net
* Production 3: http://node03.public.learningregistry.net
* **Sandbox** (http://sandbox.learningregistry.org) replaces **Test01** and is now running 0.23.4
* **Alpha** (http://alpha.learningregistry.org) replaces **Test02** and is from now on running the latest stable master.

## Updated development process

> See https://github.com/LearningRegistry/LearningRegistry/wiki/Contributing-to-the-Learning-Registry

## Issues

An issues list is maintained on Github along with the source code. If you discover an issue, please add it to: https://github.com/LearningRegistry/LearningRegistry/issues