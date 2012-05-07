# DRAFT: Upgrading to 0.23.6 from previous release

## Overview

LR Node software improvements in 0.23.6 fix a spec-compatibility issue that existed in prior releases as part of the distribute implementation. Unfortunately this change will cause 0.23.6 to no longer be able to distribute to nodes running a version below 0.23.6.  However 0.23.5 nodes should be able to still distribute to 0.23.6 nodes with a minor configuration update of the distribution endpoint url.

Because of the backwards compatibility condition this creates, 0.23.6 is strongly encouraged by all node operators. The benefits introduced by 0.23.6 through lower disc utilization will significantly reduce storage requirements.  Details of the release can be found [here](https://github.com/LearningRegistry/LearningRegistry/wiki/Release-Notes-0.23.6).


## Recommended Requirements

CouchDB 1.2.0 (version 1.1.1 works but not recommended, upgrade if possible)
Python 2.7.3 (if are not going to be using complex discriminators for data services, you can still use 2.6; if you don't know what this means, upgrade to 2.7.3)


## Upgrade Process Overview

1. Backup Installation
2. Install CouchDB 1.2.0 and migrate old resource_data to 1.2.0 and remove resource_data_distribute documents
3. If not already using Python 2.7.3, install and create new 2.7.4 virtualenv
4. Pull updated LearningRegistry Code from GitHub.
5. Execute LearningRegistry Node Configuration and verify startup.
6. Update LearningRegistry start/stop scripts.
7. Launch LearningRegistry process.
8. (Optional) Install Data Service views


## Upgrade Process Detail

### Step 1. Backup Installation

Use your desired method for backing up the following within your existing install:
+ The following CouchDB files:
  * /[path to couchdb config]/local.ini
    - *Linux*: usually ```/etc/couchdb/local.ini``` but possibly elsewhere check ```/etc/init.d/couchdb```
    - *Windows*: TODO
  * /[path to couchdb db files]/resource_data.couch

### Step 2. Install CouchDB 1.2 and Migrate Data
+ Install CouchDB 1.2 to a different location. If upgrading, do not install to the same location as a previous version.
  * Recommended build solution: https://github.com/iriscouch/build-couchdb
    - @jimklo has a variation that is fixed for Ubuntu https://github.com/jimklo/build-couchdb
+ Migrate data
  * We have found through trial and error that the fastest way migrate data is to:
    1. stop your existing CouchDB (and LearningRegistry node instance).
    2. rename the resource_data.couch to resource_data_big.couch.
    3. install the following replication filter *POST GIST of resource_only filter and link here*
    4. using curl, begin a replication from resource_data_big to resource_data
    5. wait until complete, could take several hours depending upon size of resource_data_big.
    6. once replication is delete you can delete resource_data_big.

### Step 3. Install Python 2.7.3
You can do this while waiting for data migration to complete in step 2.
* First, check to see that you aren't already running 2.7.3.
  - *Linux*: use ```locate python2.7``` or ```python2.7 --version``` to determine if installed and which version.
  - *Windows*: TODO - I need this info.
* 