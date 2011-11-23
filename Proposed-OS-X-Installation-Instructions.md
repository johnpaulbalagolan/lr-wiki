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
```


