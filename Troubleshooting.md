# Troubleshooting

## CouchDB

* Verify you have CouchDB 1.0.2 running:

>     curl -X GET http://localhost:5984

> Should return {"couchdb":"Welcome","version":"1.0.2"}

* Verify you have the appropriate CouchDB databases:

>     curl -X http://localhost:5984/_all_dbs

> Should return ["community","node","resource_data","_users","network"]

## Yajl

* Verify you have yajl properly configured by:

>      python
>      import ijson

> If no error is generated, yajl should be working properly.

## uwsgi

* Starting uwsgi

>     uwsgi --ini-paste development.ini --virtualenv ~/virtualenv/lr/

* Stopping uwsgi

>     killall -9 uwsgi

## Windows Installation
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