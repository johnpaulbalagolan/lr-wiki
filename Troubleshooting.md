# Troubleshooting

## CouchDB

* Verify you have CouchDB 1.0.2 running:

>     curl -X GET http://localhost:5984

> Should return {"couchdb":"Welcome","version":"1.0.2"}

## Yajl

* Verify you have yajl properly configured by:

>      python
>      import ijson

> If no error is generated, yajl should be working properly.

## uwsgi

* Starting uwsgi

>     uwsgi --ini-paste development.ini --virtualenv ~/virtualenv/lr/

* Stopping uwsgi

>     killall -9 uwsgi