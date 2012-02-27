# The following python script will update all design documents in the specified CouchDB database
    #!/usr/bin/env python
    import couchdb
    import json
    import urllib2
    import threading
    import time
    import sys
    def updateView(designDoc,database):
        try:
            viewName = "{0}/_view/{1}".format(designDoc.id,designDoc.doc['views'].keys()[0])
            print(viewName)
            print(len(database.view(viewName,limit=1)))
        except Exception as ex: 
            print ex.message    
    def updateDatabaseViews(databaseURL):
        try:
            database = couchdb.Database(databaseURL)
            designDocs = database.view('_all_docs',include_docs=True,
                                                            startkey='_design%2F',endkey='_design0')
            for designDoc in designDocs:                        
                if designDoc.doc.has_key('views') and len(designDoc.doc['views']) > 0:
                    db = couchdb.Database(databaseURL)
                    t = threading.Thread(target=updateView,args=(designDoc,db))
                    t.start()
        except Exception as e:
            print e.message
    def main():
        updateDatabaseViews('http://localhost:5984/resource_data')
        while threading.active_count() > 1:
            sys.stdout.flush()
            time.sleep(1)
    if __name__ == '__main__':
        main()
# Cron Job

To Run the above script as a crob job run 

    sudo crontab -e

and add
       
    @hourly /path/to/script.py
