## Configure apt sources ##

* Edit the sources list

>       sudo vim /etc/apt/source.list.d/sources.list

* Add deb restrticted and multiverse, plus add deb-src for all:

>       deb http://us.archive.ubuntu.com/ubuntu lucid main universe restricted multiverse
>       deb http://us.archive.ubuntu.com/ubuntu lucid-updates main universe restricted multiverse
>       deb-src http://us.archive.ubuntu.com/ubuntu lucid main universe restricted multiverse
>       deb-src http://us.archive.ubuntu.com/ubuntu lucid-updates main universe restricted multiverse

* Update apt sources

>       sudo apt-get update


## Install curl ##

* Use apt-get to install curl

>       sudo apt-get install libcurl3 curl


## Install Python setup tools ##

* Install Python easy_setup

>       sudo apt-get install python-pkg-resources python-setuptools


## Install CouchDB ##

* Build CouchDB dependencies

>       sudo apt-get build-dep couchdb

* Install other dependencies

>       sudo apt-get install xulrunner-dev libicu-dev libcurl4-gnutls-dev libtool

* Then create /etc/ld.so.conf.d/xulrunner.conf.

>   a. To check what XULRunner version you have installed:

>       xulrunner -v

>   b. Configure xulrunner

>   >   i. Edit the xulrunner.conf

>   >       sudo vi /etc/ld.so.conf.d/xulrunner.conf

>   >   ii. Add the following edits, replacing the x.x.x.x with your version number.

>   >       /usr/lib/xulrunner-x.x.x.x
>   >       /usr/lib/xulrunner-devel-x.x.x.x

>   c. Update ldconfig

>       sudo /sbin/ldconfig

* Download CouchDB from http://couchdb.apache.org/downloads.html.  At the present time, 1.0.2 has been tested.

* Untar (decompress) the source file:

>       tar -zxvf apache-couchdb-x.x.x.tar.gz

* Change into the expanded directory:

>       cd apache-couchdb-x.x.x

* Install SpiderMonkey (see below)

* Configure the build:

>       LDFLAGS="$(pkg-config mozilla-js --libs-only-L)" CFLAGS="$(pkg-config mozilla-js --cflags)" ./configure

* Build CouchDB:

>       make

* Fix any errors

* Install CouchDB to default location:

>       sudo make install

* Add couchdb user account

* change file ownership from root to couchdb user and adjust permissions

>       sudo chown -R couchdb: /usr/local/var/{lib,log,run}/couchdb /usr/local/etc/couchdb
>       sudo chmod 0770 /usr/local/var/{lib,log,run}/couchdb/
>       sudo chmod 664 /usr/local/etc/couchdb/*.ini
>       sudo chmod 775 /usr/local/etc/couchdb/*.d

* install init script and start couchdb

>       cd /etc/init.d
>       sudo ln -s /usr/local/etc/init.d/couchdb couchdb
>       sudo /etc/init.d/couchdb start

* configure couchdb to start on system start

>       sudo update-rc.d couchdb defaults

* Verify couchdb is running

>       curl http://127.0.0.1:5984/

* To accesses futon remotely and run tests, update the bind address in local.ini:

>       sudo vim /usr/local/etc/couchdb/local.ini
>            [httpd]
>            ; Bind to all addresses
>            bind_address = 0.0.0.0

* Restart couchdb

>       sudo service couchdb restart


## Install SpiderMonkey ##

* Get one of the source tarballs from http://ftp.mozilla.org/pub/mozilla.org/js/ (1.7.0 or 1.8.0-rc1 will do).

* Unpack the tarball. Note that once extracted the source are in the directory "js", without the expected version suffix.

* Go to the js/src directory.

>       cd js/src

* Build SpiderMonkey. There is no default Makefile, use Makefile.ref. The default build is debug, use BUILD_OPT=1 for an optimized build.

>       make BUILD_OPT=1 -f Makefile.ref

* Install SpiderMonkey. Instead of "install" the target to use is "export". Instead of PREFIX the target directory is specified with JS_DIST.

>       sudo make BUILD_OPT=1 JS_DIST=/usr/local -f Makefile.ref export

## Configure logrotate to rotate and compress CouchDB log files

* These steps are only necessary if you installed from source.

* Open logrotate.conf.

* Uncomment the the compress option, this will allow logrotate to compress old log files into a gzip file.

* run ln -s /usr/local/etc/logrotate.d/couch /etc/logrotate.d/couchdb as root or using sudo to create the couchdb entry for logrotate


## Install Yajl 1.0.12 ##

* Install Yajl dependencies

>       sudo apt-get install ruby cmake

* Download and extract and build Yajl 1.0.12 from here http://lloyd.github.com/yajl/

>       sudo make
>       sudo make install

* Update your LD_LIBRARY_PATH to include /usr/local/lib. Add the following line to ~learningregisty/.bashrc.d/defaults or /etc/bach.bashrc

>       export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH


## Install Python virtualenv and Pylons ##

* Install virtualenv

>       sudo easy_install virtualenv

* Install required library dependencies

>       sudo apt-get install python-dev python-libxml2 python-libxslt1 libxml2-dev libxslt1-dev

* Create a user for learningregistry and su to user

>       su learningregistry

* Create a directory for the virtualenv

>       mkdir virtualenv
>       cd virtualenv

* Create virtualenv for LR

>       virtualenv --distribute lr
>       cd lr/bin/

* Install LR Python deps

>       ./pip install pylons
>       ./pip install flup
>       ./pip install pyparsing
>       ./pip install --upgrade couchdb
>       ./pip install restkit
>       ./pip install cython
>       ./pip install lxml
>       ./pip install iso8601plus
>       ./pip install ijson


## Configure Nginx - Should be preinstalled on Ubuntu ##

* Backup your original nginx.conf file

>       sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak

* Copy the ngnix.conf file from repository

>       sudo cp nginx.conf /etc/nginx/nginx.conf
## Configure Pylons logging level

* Edit the production.ini found at LearningRegistry/LR

* Modify the level value under the logger_lr section

* For production is is set to only log error messages, for more verbose logging it can be set to info

## Start LR code ##

* From your virtualenv directory start paster where */home/learningregistry/virtualenv/lr* is my path to virtualenv.

>       /home/learningregistry/virtualenv/lr/bin/paster serve --daemon production.ini start