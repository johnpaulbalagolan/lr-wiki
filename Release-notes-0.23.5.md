LR version 0.23.5 was released on February 7, 2012.  The production and sandbox servers are now running LR version 0.23.5.

This release consists primarily of bug fixes and updates responding to community feedback.  There are no expected changes required for users.  Services should perform as expected.  LR v0.23.5 conforms to the LR technical specification v0.23.  These release notes are available from: https://github.com/LearningRegistry/LearningRegistry/wiki/Release-Notes-0.23.5

## Changes

> See https://github.com/LearningRegistry/LearningRegistry/issues?milestone=4&state=closed

Highlighted changes:

* Fixed view update handler. The issue was that slice views were not being updated correctly
* Update to publish to support the creation and validation of documents with different 'doc_version' values
* Reject empty string values for required fields
* Fixed bug where obtain was returning invalid json if documents have empty resource locators
* Fixed issue where change monitor was flooding the logs with error messages

## Servers Updated

> See https://github.com/LearningRegistry/LearningRegistry/wiki/nodes

* Production 1: http://node01.public.learningregistry.net
* Production 2: http://node02.public.learningregistry.net
* Production 3: http://node03.public.learningregistry.net
* Sandbox: http://sandbox.learningregistry.org

## Issues

An issues list is maintained on Github along with the source code. If you discover an issue, please add it to: https://github.com/LearningRegistry/LearningRegistry/issues