# Troubleshooting
## Linux Installation

### CouchDB

* Verify you have CouchDB 1.0.2 running:

>     curl -X GET http://localhost:5984

> Should return {"couchdb":"Welcome","version":"1.0.2"}

* Verify you have the appropriate CouchDB databases:

>     curl -X http://localhost:5984/_all_dbs

> Should return ["community","node","resource_data","_users","network"]

### Yajl

* Verify you have yajl properly configured by:

>      python
>      import ijson

> If no error is generated, yajl should be working properly.

### uwsgi

* Starting uwsgi

>     uwsgi --ini-paste development.ini --virtualenv ~/virtualenv/lr/

* Stopping uwsgi

>     killall -9 uwsgi

### apt-get update

* If you receive this error, **GPG error: http://nginx.org lucid Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY XXXXXXXXXXXXXXXX**, while attempting to update apt-get, run these commands (replace XXXXXXXX with the last 8 digits of the PUBKEY):

>     gpg --keyserver keyserver.ubuntu.com --recv XXXXXXXX 

>     gpg --export --armor XXXXXXXX | sudo apt-key add -

>     sudo apt-get update

### Nginx
* If you receive this error, **WARNING: the following packages cannot be authenticated! nginx**, run the following command

>     sudo apt-get update && sudo apt-get install nginx

### Running the LR code
* If you receive a **lr.lib.model_parser.SpecValidationException: Invalid value for'service_type'expecting one of: 
 '('publish', 'access', 'distribute', 'broker', 'administrative')' instead of ''** error or **pkg_resources.DistributionNotFound: LR** error, be sure to checkout the latest code (0.23.3 as of December 2011)
* Navigate to your LearningRegistry repository and run the following command

>     git checkout 0.23.3

## Windows Installation
### Visual C++ 2008 Express
1. If you are receiving a message displaying **An earlier version of Microsoft Visual Studio 2008 has been detected on the system that must be updated to SP1 before installation can proceed.  Please update all other versions of Visual Studio 2008 to SP1 level by visiting Microsoft Update, and then install Visual Studio 2008 Express SP1.**, follow these instructions:
     * Click the associated **Visual Studio 2008 Service Pack 1** link
     * Click **Download**
     * Click **Run** and follow setup instructions
          * Click **Next**
          * Check the **I have read and accept the license terms** box and click **Next**

### YAJL
1. If you are receiving a **CMake Error at CMakeLists.txt:58 (SET_TARGET_PROPERTIES):set_target_properties called with incorrect number of arguments** message, follow these instructions:
     * In **Windows Explorer** navigate to your YAJL source folder: **[Directory]/Python27/Lib/lloyd-yajl-17b1790/src**
     * Right click **CMakeLists.txt**, hover over **Open With** and choose your version of **Visual Studio**
     * Hit **enter** after the line **#### setup shared library version number** to start a new line
     * Type:
          * **cmake_minimum_required(VERSION 2.8)** (Enter)
          * **SET(YAJL_MAJOR 1)** (Enter)
          * **SET(YAJL_MINOR 0)** (Enter)
          * **SET(YAJL_MICRO 12)** (Enter)
     * Click **File** -> click **Save CMakeLists.txt** and close the window
     * Hit the **Up** arrow key in the **Visual Studio Command Prompt** to retrieve the previous command then hit **Enter**
     * You should now receive the message **Build files have been written to [Directory]**     