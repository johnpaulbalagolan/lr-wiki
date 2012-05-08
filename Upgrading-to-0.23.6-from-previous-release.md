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
3. Update NGINX configuration.
4. If not already using Python 2.7.3, install and create new 2.7.4 virtualenv
5. Pull updated LearningRegistry Code from GitHub.
6. Execute LearningRegistry Node Configuration and verify startup.
7. Update LearningRegistry start/stop scripts.
8. Launch LearningRegistry process.
9. (Optional) Install Data Service views


## Upgrade Process Detail

### Step 1. Backup Installation
+ Stop any learning registry running process.
  - *Linux*: ```sudo service learningregistry stop``` or ```sudo /etc/init.d/learningregistry stop```.
    * Verify no stray processes are running; stop/stop script is known to fail sometimes: ```ps aux | grep uwsgi```.  If still running ```sudo killall -9 uwsgi``` will kill all leftover zombies. 
Use your desired method for backing up the following within your existing install:
+ The following CouchDB files:
  * /[path to couchdb config]/local.ini
    - *Linux*: usually ```/etc/couchdb/local.ini``` but possibly elsewhere check ```/etc/init.d/couchdb```
    - *Windows*: The default directory is C:\Program Files (x86)\Apache Software Foundation\CouchDB\etc\couchdb
  * /[path to couchdb db files]/resource_data.couch
    - *Linux*: usually ```[couch install path]/var/lib/couchdb```
    - *Windows*: The default directory is C:\Program Files (x86)\Apache Software Foundation\CouchDB\var\lib\couchdb
+ Your Learning Registry ```development.ini``` or ```production.ini``` file which you may have custom log settings.
  * The upgrade will destroy the previous LR configuration, be sure to back up the configuration file in case you wish to restore customized settings.


### Step 2. Install CouchDB 1.2 and Migrate Data
+ Install CouchDB 1.2 to a different location. If upgrading, do not install to the same location as a previous version.
  * Recommended build solution: https://github.com/iriscouch/build-couchdb
  * *Windows*: Download the setup-couchdb-1.2.0_otp_R15B.exe installer from [here](https://github.com/dch/couchdb/downloads)
    - @jimklo has a variation that is fixed for Ubuntu if the above build fails https://github.com/jimklo/build-couchdb
+ Be sure to make note of any settings old local.ini and migrate those settings to the local.ini of the new version.  Specifically take note of locations for databases and views.
  * If you made any INI file changes, be sure to restart CouchDB.
+ Migrate data - we have found through trial and error that the fastest way migrate data is to:
    1. stop your existing CouchDB (and LearningRegistry node instance).
    2. rename the resource_data.couch to resource_data_big.couch.
    3. start the new CouchDB 1.2.0 (don't start LearningRegistry)
    4. Follow the instructions in the [LR Upgrade Filter Gist](https://gist.github.com/2638166) to upgrade resource_data_big to the smaller resource_data used in the v 0.23.6 release.
    5. Wait until complete, could take several hours depending upon size of resource_data_big.
    6. Once replication is complete, you can delete resource_data_big.


### Step 3: Update NGINX configuration
* Edit the site configuration for learningregistry in NGINX:
  - /etc/nginx/sites-enabled/learningregistry
* *Modify* the ```server``` section for ```location /resource_data```:
  - change ```location /resource_data``` to ```location /incoming```
  - change ```proxy_pass http://localhost:5984/resource_data``` to ```proxy_pass http://localhost:5984/incoming```
  - optionally update any basic authentication settings.
  - save changes.
  - changed section should resemble:
     ```
        # Proxy incoming CouchDB DB to port 80.
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
* Restart NGINX using ```sudo service nginx restart```.


### Step 4. Install Python 2.7.3
You can do this while waiting for data migration to complete in step 2.
* First, check to see that you aren't already running 2.7.3.
  - *Linux*: use ```locate python2.7``` or ```python2.7 --version``` to determine if installed and which version.
  - *Windows*: use ```python --version```
* If you don't have Python 2.7.3, then install according to instructions found [here](http://www.python.org/download/releases/2.7.3/).
  - *Linux*: most Linux installations recommend that you do not upgrade the existing Python version, instead use [```make altinstall```](http://docs.python.org/using/unix.html#building-python) instead.
  - *Windows*: Download and run the Windows x86 MSI Installer (2.7.3) (sig) from the Python link above. When running the installation if you're already running Python 2.7.x make sure you overwrite your current Python installation. If you have an older installation you'll have to remember to edit your PATH variable to use the new Python installation. Also be sure to install Python for all users
* Install setuptools.
  - Follow instructions provided [here](http://pypi.python.org/pypi/setuptools#installation-instructions) http://pypi.python.org/pypi/setuptools#installation-instructions
    + *Linux*: recommendation is to download [setuptools-0.6c11-py2.7.egg](http://pypi.python.org/packages/2.7/s/setuptools/setuptools-0.6c11-py2.7.egg#md5=fe1f997bc722265116870bc7919059ea) and use ```sudo sh setuptools-0.6c9-py2.7.egg``` to install.
    + *Windows*: download setuptools-0.6c11.win32-py2.7.exe [here](http://pypi.python.org/pypi/setuptools#downloads)
* Install virtualenv.
  - *Linux*: Once setuptools is installed, you can use ```sudo easy_install2.7 virtualenv```.
  - *Windows*: Once setuptools is installed, you can use ```easy_install virtualenv```. 
* Create new 2.7 virtualenv:
  - Switch to the account that will execute learningregistry service.
    - *Linux*: The default instructions use a user named learningregistry; ```sudo su - learningregistry```
    - *Windows*: Login as the learningregistry user (or whichever account executing the learning registry)
  - Create the new virtualenv:
    - *Linux*: ```virtualenv -p python2.7 ~/env/lr27```
    - *Windows*: ```virtualenv lr27```
  - Activate virtualenv:
    - *Linux*: ```. ~/env/lr27/bin/activate``` _NOTE:_ the command there is `.`; on some Linux shells this is also the ```source``` command.
    - *Windows*: In the initial setup instructions you were to create a virtualenv directory. Navigate to that directory and run the ```lr27\Scripts\activate``` command
     
* Install uwsgi:
  - ```pip install uwsgi```
* Additional dependencies will be installed in the next step.


### Step 5: Pull updated code for LearningRegistry.
* Upgrade LearningRegistry source and install dependencies:
  - If you originally installed via GitHub clone:
    1. ```cd``` to the base of the LearningRegistry checkout.
    2. ```git fetch origin/master```
    3. ```git checkout 0.23.6```
  - If you are pulling fresh:
    1. ```cd ~```
    2. ```git clone git://github.com/LearningRegistry/LearningRegistry.git```
    3. ```cd ./LearningRegistry```
    3. ```git checkout 0.23.6```
* Install LearningRegistry modules and dependencies:
    3. ```pip install -e ./LR/```
       + lots of stuff should download and install, this could take a bit of time.


### Step 6: Execute LearningRegistry Node Configuration and verify startup
* Run the configuration:
    1. ```cd ./config/```
    2. ```python2.7 ./setup_node.py```
       + answer the questions as prompted.
* Verify LearningRegistry starts:
  + *Linux*
    1. ```uwsgi --ini-paste /path/to/LearningRegistry/LR/development.ini start -H /path/to/env/lr27 --pidfile /var/run/learningregistry/uwsgi.pid --daemonize /var/log/learningregistry/uwsgi.log```
    2. check the ```/var/log/learningregistry/uwsgi.log``` for errors, if no errors you should stop the process.
       - ```ps aux | grep uwsgi``` to locate the process
       - ```killall -9 uwsgi``` to kill all relevant uwsgi processes; there should be multiple.


### Step 7: Update LearningRegistry start/stop scripts
* Update start/stop scripts with python2.7 and new virtualenv (skip if you didn't upgrade your python and virtualenv).
  - Locate and edit learning registry start/stop scripts
    + *Linux*: /etc/init.d/learningregistry
  - Update the following variables to reflect new locations:
    + ```LR_VIRTUALENV``` The absolute path to your Python 2.7.3 virtualenv environment (```/home/learningregistry/env/lr27``` in this example).
    + ```LR_HOME``` The absolute path to the ```LR`` directory within the checked-out git project.


### Step 8: Launch LearningRegistry process

*Linux*: ```service learningregistry start```

*Windows*: Navigate to the LR directory in the LearningRegistry and run ```paster serve development.ini```


### Step 9: Install Data Service Views (optional)

If you want to use the included Standards Alignment Data service views:

   1. Activate the Python virtual environment: ```/home/learningregistry/env/lr27/bin/activate```
   2. ```cd /path/to/LearningRegistry/data_services```
   3. ```couchapp push standards-alignment-dct-conformsTo http://locahost:5984/resource_data```
   4. ```couchapp push standards-alignment-lr-paradata http://locahost:5984/resource_data```
   5. ```couchapp push standards-alignment-related http://locahost:5984/resource_data```