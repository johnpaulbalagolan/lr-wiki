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
6. Update LearningRegistry start/stop scripts and NGINX config.
7. Launch LearningRegistry process.
8. (Optional) Install Data Service views


## Upgrade Process Detail

### Step 1. Backup Installation
+ Stop any learning registry running process.
  - *Linux*: ```sudo service learningregistry stop``` or ```sudo /etc/init.d/learningregistry stop```.
    * Verify no stray processes are running; stop/stop script is known to fail sometimes: ```ps aux | grep uwsgi```.  If still running ```sudo kill -9 [PID] [ [PID] ... ]``` will kill all leftover zombies. 
Use your desired method for backing up the following within your existing install:
+ The following CouchDB files:
  * /[path to couchdb config]/local.ini
    - *Linux*: usually ```/etc/couchdb/local.ini``` but possibly elsewhere check ```/etc/init.d/couchdb```
    - *Windows*: TODO - someone please contribute!
  * /[path to couchdb db files]/resource_data.couch
+ Your Learning Registry ```development.ini``` or ```production.ini``` file which you may have custom log settings.
  * The upgrade will destroy the previous LR configuration, be sure to back up the configuration file in case you wish to restore customized settings.


### Step 2. Install CouchDB 1.2 and Migrate Data
+ Install CouchDB 1.2 to a different location. If upgrading, do not install to the same location as a previous version.
  * Recommended build solution: https://github.com/iriscouch/build-couchdb
    - @jimklo has a variation that is fixed for Ubuntu if the above build fails https://github.com/jimklo/build-couchdb
+ Be sure to make note of any settings old local.ini and migrate those settings to the local.ini of the new version.  Specifically take note of locations for databases and views.
  * If you made any INI file changes, be sure to restart CouchDB.
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
  - *Windows*: TODO - someone please contribute!
* If you don't have Python 2.7.3, then install according to instructions found [here](http://www.python.org/download/releases/2.7.3/).
  - *Linux*: most Linux installations recommend that you do not upgrade the existing Python version, instead use [```make altinstall```](http://docs.python.org/using/unix.html#building-python) instead.
  - *Windows*: TODO - someone please contribute!
* Install setuptools.
  - Follow instructions provided [here](http://pypi.python.org/pypi/setuptools#installation-instructions) http://pypi.python.org/pypi/setuptools#installation-instructions
    + *Linux*: recommendation is to download [setuptools-0.6c11-py2.7.egg](http://pypi.python.org/packages/2.7/s/setuptools/setuptools-0.6c11-py2.7.egg#md5=fe1f997bc722265116870bc7919059ea) and use ```sudo sh setuptools-0.6c9-py2.7.egg``` to install.
* Install virtualenv.
  - *Linux*: Once setuptools is installed, you can use ```sudo easy_install2.7 virtualenv```.
* Create new 2.7 virtualenv:
  - Switch to the account that will execute learningregistry service.
    - *Linux*: The default instructions use a user named learningregistry; ```sudo su - learningregistry```
    - *Windows*: TODO - someone please contribute!
  - Create the new virtualenv:
    - ```virtualenv -p python2.7 ~/env/lr27```
  - Activate virtualenv:
    - *Linux*: ```. ~/env/lr27/bin/activate``` _NOTE:_ the command there is `.`; on some Linux shells this is also the ```source``` command.
    - *Windows*: TODO - someone please contribute!
* Install uwsgi:
  - ```pip install uwsgi```
* Additional dependencies will be installed in the next step.


### Step 4: Pull updated code for LearningRegistry.
* Upgrade LearningRegistry source and install dependencies:
  - If you originally installed via GitHub clone:
    1. ```cd``` to the base of the LearningRegistry checkout.
    2. ```git pull origin/master```
  - If you are pulling fresh:
    1. ```cd ~```
    2. ```git clone git://github.com/LearningRegistry/LearningRegistry.git```
    3. ```cd ./LearningRegistry```
    3. ```git checkout 0.23.6```
* Install LearningRegistry modules and dependencies:
    3. ```pip install -e ./LR/```
       + lots of stuff should download and install, this could take a bit of time.


### Step 5: Execute LearningRegistry Node Configuration and verify startup
* Run the configuration:
    1. ```cd ./config/```
    2. ```python2.7 ./setup_node.py```
       + answer the questions as prompted.
* Verify LearningRegistry starts:
  + *Linux*
    1. ```uwsgi --ini-paste /path/to/LearningRegistry/LR/development.ini start -H /path/to/env/lr27 --pidfile /var/run/learningregistry/uwsgi.pid --daemonize /var/log/learningregistry/uwsgi.log```
    2. check the ```/var/log/learningregistry/uwsgi.log``` for errors, if no errors you should stop the process.
       - ```ps aux | grep uwsgi``` to locate the process
       - ```kill -9 [PID] [ [PID] ... ]``` to kill all relevant uwsgi processes; there should be multiple.


### Step 6: Update LearningRegistry start/stop scripts and NGINX config
* Update start/stop scripts with python2.7 and new virtualenv (skip if you didn't upgrade your python and virtualenv).
  - Locate and edit learning registry start/stop scripts
    + *Linux*: /etc/init.d/learningregistry
  - Update the following variables to reflect new locations:
    + ```LR_VIRTUALENV``` The absolute path to your Python 2.7.3 virtualenv environment (```/home/learningregistry/env/lr27``` in this example).
    + ```LR_HOME``` The absolute path to the ```LR`` directory within the checked-out git project.
* Edit the site configuration for learningregistry in NGINX:
  - /etc/nginx/sites-enabled/learningregistry
* Add the following section at the end of the ```server``` section:
  ```
     # Proxy access the the resource_data database 
        location /incoming{

                # For resource_data access don't log the data.
                access_log   /var/log/nginx/learningregistry.access.log lr_log_no_query;

                # Uncomment to following two lines to enable http basic auth for
                # couchdb incoming access.
                #auth_basic "Learning Registry Resource Data Authentication";
                #auth_basic_user_file  httpasswd/lr_resource_data.passwd;

                proxy_pass http://localhost:5984/incoming;
                proxy_redirect off;
                proxy_redirect off;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Authorization "";
        }
   ```

