The Learning Registry makes digital learning resources easier to find, easier to access and easier to integrate into learning environments wherever they are stored -- around the country and the world. This will enable teachers, students, parents, schools, governments, corporations and non-profits to build and access better, more interconnected and personalized learning solutions needed for a 21st-century education.

This software is used to setup a new Learning Registry (LR) node.  For system specific installation guidance, see: 

> https://github.com/LearningRegistry/LearningRegistry/wiki/Installation

1\. License & Copyright
--------------------

Copyright 2011 SRI International

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

2\. Overview of Contents
---------------------

* config
    * setup_node.py - simple script to configure a couch instance for an lr use.
* couchdb/apps
    * stemx - NSDL STEM Exchange Demo couch application
* couchdb/tests
    * stemx - scripts for testing STEM Exchange couch app
    * generate-json-evelope-data.py - OBSOLETE
* data-pumps
    * del-contents.py - simple script to delete contents of a couchdb minus design documents.
    * nsdl-to-lr-data-pump.py - OAI-PMH harvester; data pump script from NDSL-DC -> LR RDDDM
    * sample-pump-oaipmh-lib.py - OBSOLETE; here for reference.
* install
    * setup_lr.bash - a script to set up a development Learning
      Registry node on Ubuntu 10.04 and MacOS 10.6.x onwards.
    * install_pydeps.bash - a script to create a virtualenv and
      install the Learning Registry Pylons application in that
      virtualenv.
* LR - Pylons LR application that is used to interface w/ CouchDB.
* search - ??? A simple search UI to be installed in a design document.  _TODO: move into a couchapp._