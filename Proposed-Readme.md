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

# Introduction

There are two recommended approaches to get a new Learning Registry node running using the latest stable code (0.23.0): 1) via an Amazon Machine Instance (AMI) or 2) via installing the code.  

Instructions for using an existing AMI are available from http://goo.gl/fhdg3.  

The installation instructions below describe eight steps to get a new Learning Registry node running using the latest stable code.  These instructions are provided for Linux and Mac and have been tested with Ubuntu 10.04 LTS and Snow Leopard.

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

* Download (Mac and Windows) or Copy the Download Link (Linux) for Couchbase Single Server Community 1.1.x, which is a binary distribution of CouchDB 1.0.x from http://www.couchbase.com/downloads (NOTE: this is a "Previous Release").  

### Linux
Issue commands below on Linux.

* Remove Couchdb-bin

>     sudo apt-get remove couchdb-bin

* Install Couchbase

>     cd ~/
>     curl "<download url>" -o couchbase-server.deb
>     sudo dpkg -i couchbase-server.deb

### Mac
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

## 3. Install Nginx (1.0.4+)

### Linux

>     sudo apt-get install nginx

### Mac

>     brew install nginx

## 4. Install uWSGI (latest stable)

### Linux

>     sudo pip install uwsgi

### Mac

* TBD

## 5. Install Yajl (1.0.12)

### Linux

* Install Yajl using apt-get


>     sudo apt-get install lib-yajl1


* or you can install from source


* Install Yajl dependencies

>     sudo apt-get install ruby cmake

* Download and install Yajl

>     wget http://github.com/lloyd/yajl/tarball/1.0.12 -O yajl-tarball
>     tar -zxvf yajl-tarball
>     cd lloyd-yajl-17b1790
>     sudo ./configure
>     sudo make
>     sudo make install

* Update your LD_LIBRARY_PATH to include /usr/local/lib. Add the following line to ~learningregisty/.bashrc.d/defaults or /etc/bash.bashrc

>     export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

* Install ijson

>     sudo pip install ijson

### Mac

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

## 7. Configure Nginx

### Linux

NOTE: Run the commands below as a user that is in the sudoers file

* Backup your original nginx directory

>     sudo cp -R /etc/nginx /etc/nginx.bak

* Copy the ngnix directory from repository

>     sudo cp -R /home/learningregistry/gitrepos/LearningRegistry/etc/nginx /etc/

* Create symbolic link

>     sudo ln -s /etc/nginx/site-available/learningregistry /etc/nginx/sites-enabled/learningregistry

* Start nginx

>     sudo service nginx start

### Mac

NOTE: Run the commands below as a user that is in the sudoers file

* Backup your original nginx directory

>     sudo cp -R /etc/nginx /etc/nginx.bak

* Copy the ngnix directory from repository into the /etc/nginx directory

>     sudo cp -R /home/learningregistry/gitrepos/LearningRegistry/etc/nginx /etc/

* Create symbolic link

>     sudo ln -s /etc/nginx/site-available/learningregistry /etc/nginx/sites-enabled/learningregistry

* Start nginx

>     sudo service nginx start

## 8. Start LR Code

NOTE: Run the command below as the learningregistry user

>     uwsgi --ini-paste ~/gitrepos/LearningRegistry/LR/development.ini --virtualenv ~/virtualenv/lr/