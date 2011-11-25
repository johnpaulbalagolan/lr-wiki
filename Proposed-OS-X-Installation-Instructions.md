# Installation on Mac OS X

## Prerequisites

### Homebrew
This can be done with a single line:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.github.com/gist/323731)"
```

### Python, easy_install, pip
Using homebrew:

```bash
brew install python
```

**Note that if you have XCode installed, you should already have a version of python that will work, and this step can be omitted. However, you will need to install easy_install and pip manually.**

### Python Packages
You will need virtualenv
```bash
pip install virtualenv
```

### CouchDB
The most stable and reliable way of building the latest CouchDB is to use the iriscouch installer scripts. It is to be mentioned that this method requires XCode, however, so those looking to avoid this dependency may opt to download the latest 1.1.x from http://www.couchbase.com/downloads.

The iriscouch method is replicated here for convenience:

```bash
git clone git://github.com/iriscouch/build-couchdb
cd build-couchdb
git submodule init
git submodule update
rake
```

Go get some coffee or something. It's gonna be a little while.

To start couch, run
```bash
build/bin/couchdb
```

### nginx

Again, this is easiest to do with Homebrew:
```bash
brew install nginx
```

### Yajl JSON Library
First, download and install yajl:

```bash
wget http://github.com/lloyd/yajl/tarball/1.0.12 -O yajl-tarball
tar -zxvf yajl-tarball
cd lloyd-yajl-17b1790
sudo ./configure
sudo make
sudo make install
```

Then you will need to add a new environment variable that loads every time you start a new terminal session. I used the global `/etc/bashrc`, but others may opt to use the user-specific bashrc or profile files. Either way, append the following line: 

```bash
export DYLD_LIBRARY_PATH=/usr/local/lib
```

If you are planning on continuing the installation now, **it is recommended that you also run that as a command so that you don't have to start a new terminal session for the variable to load.**

## Installation

### Configure virtualenv

This is useful for sandboxing your development environment. Any dependencies you install will be local to the virtualenv you installed them in.

```bash
cd ~
mkdir virtualenv
virtualenv virtualenv/lr
. virtualenv/lr/bin/activate
```

You should see your prompt preceded by `(lr)`, indicating you have successfully activated your virtual environment.

### Get the Source Code

Run the following commands to grab the master branch from this GitHub repository:

```bash
cd ~
mkdir gitrepos; cd gitrepos
git clone https://github.com/LearningRegistry/LearningRegistry.git
```

### Install dependencies

This step will fetch all of the necessary dependencies and install them into your virtualenv, assuming you have followed this guide in sequence and are currently in the virtualenv previously created:

```bash
cd ~/gitrepos/LearningRegistry/LR
pip install -e ./
pip install uwsgi
pip install ijson
```

### Setup New Learning Registry Node
This part is very easy. Just run

```bash
python ~/gitrepos/LearningRegistry/config/setup_node.py
```

Follow the prompts. The default values should be OK, though you may opt to turn flow control on for each service, which is NOT enabled by default.

### Configure nginx
Assuming you installed with Homebrew, you should have a folder at `/usr/local/etc/nginx`. Back this folder up in case you need to use the default nginx configuration later. Then, copy the nginx configuration folder found in the git repository cloned earlier:

```bash
#optional
cp -R /usr/local/etc/nginx /usr/local/etc/nginx.bak 

#required
cp -R ~/gitrepos/LearningRegistry/etc/nginx /usr/local/etc/nginx
mkdir /usr/local/etc/nginx/sites-enabled
ln -s /usr/local/etc/nginx/sites-available/learningregistry /usr/local/etc/nginx/sites-enabled/learningregistry
```

If you installed with Homebrew, you will have to change a couple nginx global and LR-specific configuration files. 

Inside `/usr/local/etc/nginx/nginx.conf`, comment out `use epoll`, and prepend `/usr/local` to anything beginning with `/etc` or `/var`. 

Inside `/usr/local/etc/nginx/sites-enabled/learningregistry`, first repeat the `/usr/local` prepend step as above. Then, change line 79 from `listen <ip_address>:5984` to just `listen 5984`.

### Start Learning Registry Node

These may or may not require sudo:

```bash
/usr/local/sbin/nginx
uwsgi --ini-paste ~/gitrepos/LearningRegistry/LR/development.ini
```

If both of these steps execute without error, you now have a LR node successfully set up! To verify, visit `http://localhost/services` with curl or in the browser and you should see a JSON document that describes all of the available services the LR offers. If you would like to further verify your application is working correctly, run some of the `nosetests` individually and ensure that any errors are consistent with those reported as issues in the master branch.