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

* Download and install https://github.com/downloads/dch/couchdb/setup-couchdb-1.0.2+COUCHDB-963_otp_R14B01+OTP-9139.exe

## 2.2. Python (2.x) and associated tools

### Linux (2.6.x)

* This guide assumes python is installed on Linux operating system.

* Install Python setup tools

>     sudo apt-get install python-pkg-resources python-setuptools

* Install required library dependencies

>     sudo apt-get install python-dev pythong-libxml2 python-libxslt1 libxml2-dev libxslt1-dev

* Install virtualenv

>     sudo easy_install virtualenv

### Mac

* TBD

### Windows (2.7.x)

* Download and install Python 2.7.x from http://python.org/.

* Download and Install Python setuptools (ez_setup.py) from http://peak.telecommunity.com/dist/ez_setup.py (NOTE: the provided .exe installer does not support 64-bit versions of Python for Windows due to a distutils installer compatibility issue, so use the install command below)

>     python ez_setup.py install

* Install virtualenv

>     easy_install virtualenv

## 2.3. Install uwsgi (latest stable)

>     pip install uwsgi

## 2.4. nginx (1.0.5)

### Linux

>     sudo apt-get install nginx

>     sudo service nginx start

### Mac

* TBD

### Windows 64-bit

>     http://www.box.net/shared/cei9z3799ga6oy92neec

>     start-nginx.bat

### Windows 32-bit

>     http://www.box.net/shared/iamlv5n5i3zr4gofu10s

>     start-nginx.bat

## 2.5. yajl (1.0.12)

### Linux

* Install Yajl dependencies

>     sudo apt-get install ruby cmake

* Download, extract, and build http://github.com/lloyd/yajl/tarball/1.0.12

> sudo make
> sudo make install

* Update your LD_LIBRARY_PATH to include /usr/local/lib. Add the following line to ~learningregisty/.bashrc.d/defaults or /etc/bach.bashrc

>     export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

### Mac

* TBD

### Windows

* TBD

## 2.6. Install Git

### Linux

>     sudo apt-get install git-core

### Mac

* TBD

### Windows

* TBD

## 2.6. Download latest stable tagged release and run setup.py

* Login as learningregistry user

>     su  - learningregistry

* Create directory for Git sources

>      mkdir ~/gitrepos

* Clone the sources from GitHub:

>     cd ~/gitrepos
>     git clone githttps://github.com/LearningRegistry/LearningRegistry.git

* Create Python virtual environment and activate

>     cd ~
>     mkdir ~/virtualenv
>     virtualenv ~/virtualenv/lr
>     source ./virtualenv/lr/bin/activate

At this point your prompt should be preceded with the name of the virtualenv “(lr)”.

* Install LearningRegistry as a package:

>     cd ~/gitrepos/LearningRegistry/LR
>     pip install –e ./

f.     Install flup

>     pip install flup

g.     Install couchapp

>     pip install couchapp

h.     Run the setup script

>     cd ../config
>     python setup_node.py –d

* Answer the questions as prompted.

### Mac

### Windows

## 2.7. Start LR Code

>     uwsgi --ini-paste development.ini --virtualenv ~/virtualenv/lr/