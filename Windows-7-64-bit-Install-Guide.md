All commands executed to create this guide were run as administrator (type “cmd” and hit CTRL+SHIFT+ENTER).  This may not be necessary or appropriate in all situations.

### 1\. Install IIS 7.5
### 2\. Install FastCGI module for IIS

* Run the command below:

>      dism /online /enable-feature /featurename:IIS-CGI

* Thanks to http://blogs.msdn.com/b/philpenn/archive/2009/07/19/deploying-iis-7-5-fastcgi-php-on-server-core.aspx

### 3\. Install CouchDB

* Windows Binary Installer: https://github.com/dch/couchdb/downloads
* I installed setup-couchdb-1.1.0+COUCHDB-1152_otp_R14B03.exe.  I chose to run CouchDB as a Windows Service.

### 4\. Install Python 2.7.x

* http://python.org/.
* Newer releases have not yet been tested to date.
* I installed Windows X86-64 MSI Installer (2.7.2).  Use default installation preferences.

### 5\. Install Python setuptools

* http://pypi.python.org/pypi/setuptools#files
* Download ez_setup.py from http://peak.telecommunity.com/dist/ez_setup.py and run it; it will download the appropriate .egg file and install it for you.

>      python ez_setup.py install”

* Currently, the provided .exe installer does not support 64-bit versions of Python for Windows, due to a distutils installer compatibility issue.
    
### 6\. Install PIP

* http://pypi.python.org/pypi/pip#downloads
* I installed pip-1.0.1.tar.gz then used 7-Zip to extract the .py files

>     python setup.py install

### 7\. Install Pylons for Python 

* https://github.com/Pylons/pylons
* Go to Downloads and download .zip.

>      python setup.py install

### 8\. Install couchapp

* http://couchapp.org/page/installing
* I installed the Standalone Executable for Windows

### 9\. Install CouchDB-Python

* http://pypi.python.org/pypi/CouchDB
* You can probably use PIP here or…
* I downloaded the CouchDB-0.8.tar.gz and then used 7-zip to extract the .py file.

>     python setup.py install

### 10\. Get the LR source code

* http://git.learningregistry.org

### 11\. Run config/setup_node.py from the LR source code

* Point to http://localhost:5984
* Name: test
* Defaults for the rest of the options
    
### 12\. Manually run the following couchapp commands

* Change directory to LR source directory \couchdb\apps\filter and run:

>       couchapp push http://localhost:5984/resource_data

* Change directory to LR source directory \couchdb\apps\learningregistry and run:

>       couchapp push http://localhost:5984/resource_data

* Change directory to LR source directory \couchdb\apps\oai-pmh and run:

>       couchapp push http://localhost:5984/resource_data

* Change directory to LR source directory \couchdb\apps\stemx and run:

>       couchapp push http://localhost:5984/resource_data

### 13\. Install FLUP

* Change director to the Python directory \Scripts

>      pip install flup
    
### 14\. Install pyparsing using pip

* Change director to the Python directory \Scripts
        
>     pip install pyparsing

### 15\. Install 8601 using pip
        
* Change director to the Python directory \Scripts

>       pip install 8601

### 16\. Run the development web server
        
* Change director to the Python directory \Scripts

>       paster server development.ini