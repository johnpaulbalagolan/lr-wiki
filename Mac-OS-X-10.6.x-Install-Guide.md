These instructions are provided for use by developers who may be
interested in running LR on MacOS 10.6.x for development
purposes. MacOS has not been tested for deployment of a production
Learning Registry node.

## Requirements ##
* Xcode developer tools. Downloadable from the Apple Developer site at
  http://developer.apple.com.
* [Homebrew](https://github.com/mxcl/homebrew) package manager. The
  brew command should be in your path.
* Git, which you very likely already have if you have installed
  Homebrew. But can be installed from Homebrew.
* [pip](http://pypi.python.org/pypi/pip).
* [virtualenv](http://pypi.python.org/pypi/virtualenv).
* [virtualenvwrapper](http://www.doughellmann.com/docs/virtualenvwrapper/).

**Note:** There is an issue installing lxml with Xcode 4, which is not
  required to run the Pylons app, but is required to run the
  tests. See https://gist.github.com/963298 for instructions on
  manually installing lxml with Xcode 4.

## Installation ##
* Clone this repository. If you are viewing this page on github, you
  should see the clone URL near the top of the page.

>       git clone <repository URL>

* Install CouchDB using Homebrew.

>       brew install couchdb

* Create a virtualenv for Learning Registry.

>       mkvirtualenv --no-site-packages --distribute learning-registry

* Install the required python packages into the virtualenv. The
  `mkvirtualenv` command will automatically activate the newly created
  virtualenv.

>       pip install pylons pyparsing couchdb restkit lxml iso8601plus

* Change directory to the root of the cloned Learning Registry git repository.

>       cd <path to clone of the git repository>

* Install the Learning Registry pylons app.

>       cd LR
>       pip install -e .

## Setup ##
* Start up couchdb

>       launchctl load -w /usr/local/Cellar/couchdb/1.0.2/Library/LaunchDaemons/org.apache.couchdb.plist

* Change directory to the root of the cloned Learning Registry git repository.

>       cd <path to clone of the git repository>

* Create a development configuration file. You may copy the original
  configuration file in the LR directory.

>       cp LR/development.ini.orig LR/development.ini

* Navigate to the `config` directory within your clone of the Learning
  Registry git repository.

>       cd config

* Load the initial documents for Learning Registry into CouchDB. This
  script will ask a few questions.

>       ./setup_node.py

* Edit the development.ini file and replace the line
  `use = egg:Flup#fcgi_thread` with `use = egg:Paste#http`.

## Start up the node ##
* Run the development web server.

>       paster serve --reload development.ini

* Check to see if all is well by checking the status of the node we
  have just set up. You should receive a response if it's working.

>       curl -i http://127.0.0.1:5000/status