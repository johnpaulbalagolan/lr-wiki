# To bootstrap a new node

* First download https://s3.amazonaws.com/lr.backups/node01/daily/mnt2/couchzip/resource_data.couch.tar.bz2

* Extract the content into your CouchDB data directory, this can be found by looking in /etc/couchdb/default.ini or 
in /etc/couchdb/local.ini if you've customized your CouchDB install

* Now restart CouchDB using sudo service couchdb restart
