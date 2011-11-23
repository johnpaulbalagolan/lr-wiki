# Installation on Mac OS X

## Prerequisites

### Homebrew
This can be done with a single line:

`/usr/bin/ruby -e "$(curl -fsSL https://raw.github.com/gist/323731)"`

### Python
Using homebrew:

`brew install python`

**Note that if you have XCode installed, you should already have a version of python that will work, and this step can be omitted. However, you will need to install easy_install and pip manually.**

### CouchDB
The most stable and reliable way of building the latest CouchDB is to use the iriscouch installer scripts. It is to be mentioned that this method requires XCode, however, so those looking to avoid this dependency may opt to download the latest 1.1.x from http://www.couchbase.com/downloads.

The iriscouch method is replicated here for convenience:

`git clone git://github.com/iriscouch/build-couchdb
cd build-couchdb
git submodule init
git submodule update`

