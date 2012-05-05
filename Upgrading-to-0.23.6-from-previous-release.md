# DRAFT: Upgrading to 0.23.6 from previous release

## Overview

LR Node software improvements in 0.23.6 fix a spec-compatibility issue that existed in prior releases as part of the distribute implementation. Unfortunately this change will cause 0.23.6 to no longer be able to distribute to nodes running a version below 0.23.6.  However 0.23.5 nodes should be able to still distribute to 0.23.6 nodes with a minor configuration update of the distribution endpoint url.

Because of the backwards compatibility condition this creates, 0.23.6 is strongly encouraged by all node operators. The benefits introduced by 0.23.6 through lower disc utilization will significantly reduce storage requirements.  Details of the release can be found [here](https://github.com/LearningRegistry/LearningRegistry/wiki/Release-Notes-0.23.6).


## Recommended Requirements

CouchDB 1.2.0 (version 1.1.1 works but not recommended, upgrade if possible)
Python 2.7.3 (if are not going to be using complex discriminators for data services, you can still use 2.6; if you don't know what this means, upgrade to 2.7.3)


## Upgrade Process Overview

0. Backup Installation
1. Install CouchDB 1.2.0 and migrate old resource_data to 1.2.0 and remove resource_data_distribute documents
2. If not already using Python 2.7.3, install and create new 2.7.4 virtualenv
3. Pull updated LearningRegistry Code from GitHub.
4. Execute LearningRegistry Node Configuration and verify startup.
5. Update LearningRegistry start/stop scripts.
6. Launch LearningRegistry process.
7. (Optional) Install Data Service views


## Upgrade Process Detail

### Step 0. Backup Installation

Use your desired method for backing up the following within your existing install:
+ The following CouchDB files:
  * /[path to couchdb config]/local.ini
    - *Linux*: usually ```/etc/couchdb/local.ini``` but possibly elsewhere check ```/etc/init.d/couchdb```
    - *Windows*: TODO
  * /[path to couchdb db files]/resource_data.couch

