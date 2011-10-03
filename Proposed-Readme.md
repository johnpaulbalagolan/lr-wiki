Thoughts?

# 1\. License & Copyright

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

# 2\. Installation

## 2.1. CouchDB (1.0.2)

### Linux

* Install CouchDB and other Dependencies

>     sudo apt-get install ruby1.8 rubygems1.8
>     sudo apt-get -f install

* Install CouchDB 1.0.2

Use Couchbase's Single Server community 1.1. distribution, which is a binary distribution of 1.0.2 that includes GeoCouch.
The informational download page is here: http://www.couchbase.com/downloads/couchbase-single-server/community.  Copy the download link for the distribution you need, which should be either the 32-bit or 64-bit Linux (DEB).  Then issue the following commands:

>     cd ~/
>     curl "<download url>" -o couchbase-server.deb
>     chmod -X couchbase-server.deb
>     sudo dpkg -i couchbase-server.deb

### Mac

* TBD

### Windows

* Download installer from: https://github.com/downloads/dch/couchdb/setup-couchdb-1.0.2+COUCHDB-963_otp_R14B01+OTP-9139.exe

## 2.2. Python (2.x)

### Linux (2.6.x)

* This guide assumes python is installed

* Install Python setup tools

>     sudo apt-get install python-pkg-resources python-setuptools

* Install virtualenv

>     sudo easy_install virtualenv

* Install required library dependencies

>     sudo apt-get install python-dev pythong-libxml2 python-libxslt1 libxml2-dev libxslt1-dev

### Windows (2.7.x)

* Download and install Python 2.7.x from http://python.org/.

* Download and Install Python setuptools (ez_setup.py) from http://peak.telecommunity.com/dist/ez_setup.py (NOTE: the provided .exe installer does not support 64-bit versions of Python for Windows due to a distutils installer compatibility issue, so use the install command below)

>     python ez_setup.py install

## 2.3. uwsgi (latest stable)

>     pip install uwsgi

## 2.4. nginx (1.0.5)

## 2.5. yajl (1.0.12)



### Linux

### Mac

### Windows


## 2.6. Download latest stable tagged release and run setup.py

## 2.7. Start service: uwsgi --ini-paste development.ini --virtualenv ~/virtualenv/lr/