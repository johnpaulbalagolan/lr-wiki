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

# Prerequisites

### Linux

#### Configure apt sources

* Edit the sources list.  If the file doesn't exist, create it.

>     sudo vim /etc/apt/sources.list.d/sources.list

* Add deb restricted and multiverse, add deb-src, and nginx:

>     deb http://us.archive.ubuntu.com/ubuntu lucid main universe restricted multiverse
>     deb http://us.archive.ubuntu.com/ubuntu lucid-updates main universe restricted multiverse
>     deb-src http://us.archive.ubuntu.com/ubuntu lucid main universe restricted multiverse
>     deb-src http://us.archive.ubuntu.com/ubuntu lucid-updates main universe restricted multiverse
>     deb http://nginx.org/packages/ubuntu/ lucid nginx
>     deb-src http://nginx.org/packages/ubuntu/ lucid nginx

* Update apt sources

>     sudo apt-get update  

#### Install Supporting Applications

* curl

>     sudo apt-get install curl

* vim

>     sudo apt-get install vim


# Installation

## 1. Install CouchDB (1.0.2)

* Download (Mac and Windows) or Copy the Download Link (Linux) for Couchbase Single Server Community 1.1 (1.1.1 on Mac OS X), which is a binary distribution of CouchDB 1.0.2 from http://www.couchbase.com/downloads (NOTE: this is a "Previous Release").  

* Simply install on Mac and Windows.  Issue commands below on Linux.

* Remove Couchdb-bin

>     sudo apt-get remove couchdb-bin

* Install Couchbase

>     cd ~/
>     curl "<download url>" -o couchbase-server.deb
>     sudo dpkg -i couchbase-server.deb

## 2. Install Python (2.x) and associated tools

### Linux

* This guide assumes python is installed on Linux operating system.

* Install Python setup tools

>     sudo apt-get install python-pkg-resources python-setuptools

* Install required library dependencies

>     sudo apt-get install python-dev python-libxml2 python-libxslt1 libxml2-dev libxslt1-dev

* Install and activate virtualenv

>     sudo easy_install virtualenv
>     cd ~
>     mkdir ~/virtualenv
>     virtualenv ~/virtualenv/lr
>     source ./virtualenv/lr/bin/activate

### Mac

* TBD

### Windows (2.7.x)

* Download and install Python 2.7.x from http://python.org/.

* Download and Install Python setuptools (ez_setup.py) from http://peak.telecommunity.com/dist/ez_setup.py (NOTE: the provided .exe installer does not support 64-bit versions of Python for Windows due to a distutils installer compatibility issue, so use the install command below)

>     python ez_setup.py install

* Install virtualenv

>     sudo easy_install virtualenv

## 3. Install uWSGI (latest stable)

>     pip install uwsgi

## 4. Install Nginx (1.0.5)

### Linux

>     sudo apt-get install nginx

### Mac

* TBD

### Windows

* Download and install from http://www.kevinworthington.com/nginx-for-windows-archives/

>     start-nginx.bat

## 5. Install Yajl (1.0.12)

### Linux

* Install Yajl dependencies

>     sudo apt-get install ruby cmake

* Download, extract, and build http://github.com/lloyd/yajl/tarball/1.0.12

>     sudo make
>     sudo make install

* Update your LD_LIBRARY_PATH to include /usr/local/lib. Add the following line to ~learningregisty/.bashrc.d/defaults or /etc/bach.bashrc

>     export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

### Mac

* TBD

### Windows

* TBD

## 7. Checkout Learning Registry Source Code

### Linux

* Create learningregistry user account

>     sudo useradd -c "Learning Registry System" -m -s "/bin/bash" learningregistry

* Set learningregistry user password

>     sudo passwd learningregistry

* Install Git

>     sudo apt-get install git-core

* Login as learningregistry user

>     su  - learningregistry

* Create directory for Git sources

>     mkdir ~/gitrepos
>     cd ~/gitrepos

* Checkout the source code

>     cd ~/gitrepos
>     git clone -b Sprint3Release https://github.com/LearningRegistry/LearningRegistry.git

* Create Python virtual environment and activate

>     cd ~
>     mkdir ~/virtualenv
>     virtualenv ~/virtualenv/lr
>     source ./virtualenv/lr/bin/activate

At this point your prompt should be preceded with the name of the virtualenv “(lr)”.

* Install LearningRegistry as a package:

>     cd ~/gitrepos/LearningRegistry/LR
>     pip install –e ./

* Run the setup script

>     cd ../config
>     python setup_node.py –d

* Answer the questions as prompted.

### Mac

### Windows

## 8. Configure CouchDB log rotation

## 9. Configure Nginx

### Linux

* Backup your original nginx.conf file

>     sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak

* Copy the ngnix.conf file from repository

>     sudo cp nginx.conf /etc/nginx/nginx.conf
>     sudo service nginx start

## 10. Start LR Code

>     uwsgi --ini-paste development.ini --virtualenv ~/virtualenv/lr/