# DRAFT Release Notes 0.23.7 

## Overview

Release 0.23.7 is a maintenance release to 0.23.6. That is primarily a bug fix. It is a recommended upgrade for anyone performing distribution to remote nodes requiring credentials.

## Features

* Enhancements to Distribute Registration Form aka ```/register```:
  - Added BrowserID registration to capture valid emails for contact purposes.
  - Added ability to specify distribution endpoint username/password when registering a distribution endpoint.

* Bug Fix:
  - When distributing to an endpoint that required credentials, an error was thrown due to a malformed function call when creating the CouchDB replication document with access credentials.

## Upgrading from 0.23.6

### Ubuntu

0. Install swig

    ```sudo apt-get install swig```

0. Activate your Learning Registry Virtualenv

    ```. /path/to/virtualenv/lr27/bin/activate```

0. Stop running instances of Learning Registry

    ```sudo service learningregistry stop; sudo killall -9 uwsgi```

0. Update your Learning Registry code base

    ```cd /path/to/checked/out/LearningRegistry; git fetch origin master; git checkout 0.23.7```

0. Update LR module to install new dependencies

    `pip uninstall LR; pip install -e ./LR/`

    **Note** some versions of Ubuntu (>=11.10) my fail installing M2Crypto due to an `undefined symbol: SSLv2_method` error.  If you encounter this issue install M2Crypto separately then follow by install LR again:

        pip install -e bzr+http://bazaar.launchpad.net/~ubuntu-branches/ubuntu/precise/m2crypto/precise/#egg=M2Crypto
        pip install -e ./LR/

0. Start Learning Registry

    ```sudo service learningregistry start```


### Windows

0. Open cmd.exe from Start Menu

0. Activate your virtualenv

    `c:\path\to\virtualenv\Scripts\activate.bat`

0. Install m2crypto

    `easy_install m2crypto`

0. Stop Learning Registry process

0. Update source code, launch Git Shell from Start Menu then:

         cd c:\path\to\src\LearningRegistry
         git fetch origin master
         git checkout 0.23.7

0. Install LR

     `pip install -e .\LR\`

0. Start Learning Registry process
     
     `cd LR` then `paster serve development.ini`
    

## Changelog

* [d33fe42](https://github.com/LearningRegistry/LearningRegistry/commit/d33fe42) Fix distribution credentials
* [209e4fc](https://github.com/LearningRegistry/LearningRegistry/commit/209e4fc) Fix distribution credentials
* [0ec7307](https://github.com/LearningRegistry/LearningRegistry/commit/0ec7307) Adding BrowserID gateway to Register for Distribute
* [206680d](https://github.com/LearningRegistry/LearningRegistry/commit/206680d) Adding BrowserID gateway to Register for Distribute
* [6976b1e](https://github.com/LearningRegistry/LearningRegistry/commit/6976b1e) updated to allow username/password for distribute
