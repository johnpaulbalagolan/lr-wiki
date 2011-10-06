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

#### 1. Install Supporting Applications

* curl

>     sudo apt-get install curl

* vim

>     sudo apt-get install vim

#### 2. Configure apt sources

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

### Mac
* Install homebrew:

>     /usr/bin/ruby -e "$(curl -fsSL https://raw.github.com/gist/323731)"

# Installation

## 1. Install CouchDB (1.0.2)

* Download (Mac and Windows) or Copy the Download Link (Linux) for Couchbase Single Server Community 1.1 (1.1.1 on Mac OS X), which is a binary distribution of CouchDB 1.0.2 from http://www.couchbase.com/downloads (NOTE: this is a "Previous Release").  

###Linux
Issue commands below on Linux.

* Remove Couchdb-bin

>     sudo apt-get remove couchdb-bin

* Install Couchbase

>     cd ~/
>     curl "<download url>" -o couchbase-server.deb
>     sudo dpkg -i couchbase-server.deb

###Windows 
Simply download and run the installer.

###Mac
Download the .zip file, extract, and double-click the .app file to start couchDB.
 
## 2. Install Python (2.x) and associated tools

### Linux

* This guide assumes python is installed on Linux operating system.

* Install Python setup tools

>     sudo apt-get install python-pkg-resources python-setuptools

* Install required library dependencies

>     sudo apt-get install python-dev python-libxml2 python-libxslt1 libxml2-dev libxslt1-dev

* Install pip and virtualenv

>     sudo easy_install pip 
>     sudo easy_install virtualenv

### Mac

* Install Python 2.7.x, easy_install, and pip via homebrew

>     brew install python

* Install virtualenv via easy_install

>     sudo easy_install virtualenv

### Windows (2.7.x)

* Download and install Python 2.7.x from http://python.org/.

* Download and Install Python setuptools (ez_setup.py) from http://peak.telecommunity.com/dist/ez_setup.py (NOTE: the provided .exe installer does not support 64-bit versions of Python for Windows due to a distutils installer compatibility issue, so use the install command below)

>     python ez_setup.py install

* Install virtualenv

>     easy_install virtualenv

## 3. Install Nginx (1.0.4+)

### Linux

>     sudo apt-get install nginx

### Mac

>     brew install nginx

### Windows

* Download and install from http://www.kevinworthington.com/nginx-for-windows-archives/

>     start-nginx.bat

## 4. Install uWSGI (latest stable)

### Linux

>     sudo pip install uwsgi

### Mac

* TBD

### Windows

* TBD

## 5. Install Yajl (1.0.12)

### Linux

* Install Yajl dependencies

>     sudo apt-get install ruby cmake

* Download and install Yajl

>     wget http://github.com/lloyd/yajl/tarball/1.0.12 -O yajl-tarball
>     tar -zxvf yajl-tarball
>     cd yajl-tarball
>     sudo ./configure
>     sudo make
>     sudo make install

* Update your LD_LIBRARY_PATH to include /usr/local/lib. Add the following line to ~learningregisty/.bashrc.d/defaults or /etc/bach.bashrc

>     export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

### Mac

* TBD

### Windows

* TBD

## 6. Checkout Learning Registry Source Code

### Linux

* Create learningregistry user account

>     sudo useradd -c "Learning Registry System" -m -s "/bin/bash" learningregistry

* Set learningregistry user password

>     sudo passwd learningregistry

* Install Git

>     sudo apt-get install git-core

* Login as learningregistry user

>     su learningregistry

* Create directory for Git sources

>     mkdir ~/gitrepos

* Checkout the source code

>     cd ~/gitrepos
>     git clone -b Sprint3Release https://github.com/LearningRegistry/LearningRegistry.git

* Create Python virtual environment and activate

>     cd ~
>     mkdir ~/virtualenv
>     virtualenv ~/virtualenv/lr
>     source ./virtualenv/lr/bin/activate

> At this point your prompt should be preceded with the name of the virtualenv “(lr)”.

* Install LearningRegistry as a package:

>     cd ~/gitrepos/LearningRegistry/LR
>     pip install –e ./

* Run the setup script

>     cd ../config
>     python setup_node.py –d

* Answer the questions as prompted.

### Mac

* TBD

### Windows

* TBD

## 7. Configure CouchDB log rotation

These steps are only necessary if you installed from source.

* Open logrotate.conf.

* Uncomment the the compress option, this will allow logrotate to compress old log files into a gzip file.

* run ln -s /usr/local/etc/logrotate.d/couch /etc/logrotate.d/couchdb as root or using sudo to create the couchdb entry for logrotate

## 8. Configure Nginx


### Linux

* Backup your original nginx.conf file

>     sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak

* Copy the ngnix.conf file from repository

>     sudo cp nginx.conf /etc/nginx/nginx.conf
>     sudo service nginx start

## 9. Start LR Code

>     uwsgi --ini-paste development.ini --virtualenv ~/virtualenv/lr/