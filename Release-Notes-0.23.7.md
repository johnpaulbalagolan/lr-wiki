# Release Notes 0.23.7 - DRAFT

## Overview

Release 0.23.7 is a maintenance release to 0.23.6. That is primarily a bug fix. It is a recommended upgrade for anyone performing distribution to remote nodes requiring credentials.

## Features

* Enhancements to Distribute Registration Form aka ```/register```:
  - Added BrowserID registration to capture valid emails for contact purposes.
  - Added ability to specify distribution endpoint username/password when registering a distribution endpoint.

* Bug Fix:
  - When distributing to an endpoint that required credentials, an error was thrown due to a malformed function call when creating the CouchDB replication document with access credentials.

## Changelog

* TBD

