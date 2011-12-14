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

There are two recommended approaches to get a new Learning Registry node running using the latest stable code (0.23.3): 1) via an Amazon Machine Instance (AMI) or 2) via installing the code.  

Instructions for using an existing AMI are available from http://goo.gl/fhdg3.  

The installation instructions below describe eight steps to get a new Learning Registry node running using the latest stable code.  These instructions are provided for Linux and have been tested with Ubuntu 10.04 LTS and Ubuntu 11.10.

## Linux

### Prerequisites

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

### Installation

#### 1. Install CouchDB

* If you have Ubuntu 10.04 installed, copy the download link for Couchbase Single Server Community 1.1.x, which is a binary distribution of CouchDB 1.0.x from http://www.couchbase.com/downloads (NOTE: this is a "Previous Release"). If you have Ubuntu 11.10 installed, copy the download link for Couchbase Single Server Community 1.2.x, which is a binary distribution of CouchDB 1.1.x (NOTE: this is a "Latest Release"). 


* Remove Couchdb-bin

>     sudo apt-get remove couchdb-bin

* Install Couchbase

>     cd ~/
>     curl "<download url>" -o couchbase-server.deb
>     sudo dpkg -i couchbase-server.deb

* Verify you have CouchDB running:

>     curl -X GET http://localhost:5984

> Should return {"couchdb":"Welcome","version":"1.X.X", "vendor":{"url":"http://www.couchbase.com/","name":"Couchbase",:"version":"1.X.X}}

* If you are not receiving a response, please run the following commands:

>     sudo chown -R couchbase:couchbase /opt/couchbase-server

>     sudo apt-get install libssl0.9.8

>     sudo service couchbase-server restart
 
#### 2. Install Python (2.x) and associated tools

* This guide assumes Python is installed on Linux operating system. If Python is not installed, run the following command

>     sudo apt-get install python

* Install Python setup tools

>     sudo apt-get install python-pkg-resources python-setuptools

* Install required library dependencies

>     sudo apt-get install python-dev python-libxml2 python-libxslt1 libxml2-dev libxslt1-dev

* Install pip and virtualenv

>     sudo easy_install pip 
>     sudo easy_install virtualenv

#### 3. Install Nginx (1.0.4+)

>     sudo apt-get install nginx

#### 4. Install uWSGI (latest stable)

>     sudo pip install uwsgi

#### 5. Install Yajl (1.0.12)

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

#### 6. Checkout Learning Registry Source Code

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
>     git clone -b 0.23.3 https://github.com/LearningRegistry/LearningRegistry.git

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

#### 7. Configure Nginx

NOTE: Run the commands below as a user that is in the sudoers file

* Backup your original nginx directory

>     sudo cp -R /etc/nginx /etc/nginx.bak

* Copy the ngnix directory from repository

>     sudo cp -R /home/learningregistry/gitrepos/LearningRegistry/etc/nginx /etc/

* Create symbolic link

>     sudo ln -s /etc/nginx/sites-available/learningregistry /etc/nginx/sites-enabled/learningregistry


_* NOTE: If you receive a **ln: creating symbolic link /etc/nginx/sites-enabled/learningregistry: No such file or directory** message, follow these tasks then start nginx normally:_

>     cd /etc/nginx
>     sudo mkdir sites-enabled
>     sudo ln -s /etc/nginx/sites-available/learningregistry /etc/nginx/sites-enabled/learningregistry 

> Open the learningregistry config file and check what address the CouchDB server is listening to. If it is not your IP address using port 5984, replace whatever address is listed after **listen** (located on line 79) with your IP address and port 5984

>     sudo vim sites-available/learningregistry

> Open the default config file and make sure the port the default server is listening to on line 2 is different than the port you wish to run the LR node on (simply change the port number after **listen** on line 2 if you need to)

>     sudo vim conf.d/default.conf
  
> You must stop nginx completely after changing the configuration files

>     sudo service nginx stop

* Start nginx    

>     sudo service nginx start

#### 8. Start LR Code

NOTE: Run the command below as the learningregistry user

>     uwsgi --ini-paste ~/gitrepos/LearningRegistry/LR/development.ini --virtualenv ~/virtualenv/lr/