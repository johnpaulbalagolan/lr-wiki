The Learning Registry provides [RESTful services](http://docs.learningregistry.org/en/latest/spec/Services_and_APIs/index.html#services-and-apis) to access metadata and paradata about educational resources.  The guidance below is intended to help you write software that will use the Learning Registry’s services to consume metadata and paradata.

## Harvesting Records

The [harvest service](http://docs.learningregistry.org/en/latest/spec/Access_Services/index.html#basic-harvest-service) is the recommended service to use when getting started (other services that can be used are [obtain](http://docs.learningregistry.org/en/latest/spec/Access_Services/index.html#basic-obtain-service) and [slice](http://docs.learningregistry.org/en/latest/slicing/index.html)).  The harvest [listrecords](http://docs.learningregistry.org/en/latest/spec/Access_Services/index.html#list-records) verb returns (in batches of 100 documents) records within an optional specific time/date range.  Both GET and POST methods are supported.  The GET method is shown below.

```
GET <node url>/harvest/listrecords[?from=<date>&until=<date>&resumption_token=<token>]
```

Example: https://node01.public.learningregistry.net/harvest/listrecords

> NOTE: If clicking the example in a browser, an extension like jsonview is recommended.

Results are returned as an array of JSON.  The main elements of the [result object](http://docs.learningregistry.org/en/latest/spec/Access_Services/index.html#id5) are:
* “OK”: boolean // T if successful
* “error”: “string” // only present if NOT OK describing error
* “responseDate”: “string” // timestamp
* “request”: {} // object containing request
* “listrecords”: [] // array of records
* “resumption_token”: “string” // flow control resumption token, NULL if end

Below is a python code example that harvests records using resumption tokens:
```
def harvest(start_url):
    #start by adding the root URL to the list of urls to harvest from
    urls = [start_url]
    #while we have url to harvest from continue
    while len(urls) > 0:        
        #remove the first URL to pull the LR documents from
        lr_url = urls.pop()
        # make an HTTP GET request to the LR harvest interface
        resp = urllib2.urlopen(lr_url)
        try:
            #parse json from the response body
            data = json.loads(resp.read())
            # iterate over the results
            for i in data['listrecords']:
                #for the rest of this code we only care about the LR envelope portion of the harvest result
                envelope = i['record']['resource_data']
                # process the envelope
                process_envelope(envelope)
                # if there is a resumption token
                if "resumption_token" in data and \
                        data['resumption_token'] is not None and \
                        data['resumption_token'] != "null":
                    #parse the origional URL and update the query string to contain the resumption_token
                    url_parts = urlparse.urlparse(lr_url)
                    new_query = urllib.urlencode({"resumption_token": data['resumption_token']})
                    next_url = urlparse.urlunparse((url_parts.scheme,
                                                    url_parts.netloc,
                                                    url_parts.path,
                                                    url_parts.params,
                                                    new_query,
                                                    url_parts.fragment))
                    #add the URL for the next page of results to the urls array
                    urls.append(next_url)
        except Exception as ex:
            print(ex)
            print(lr_url)
```

## Parsing Records

Each record in the Learning Registry is based on the [resource data description data model](http://docs.learningregistry.org/en/latest/spec/Resource_Data_Data_Model/index.html#resource-data-description-data-model).  The primary elements in the data model are:
* “resource_data”: “string” // describes the resource itself (metadata or paradata).
* “resource_locator”: “string” // URL of the resource

The “resource_data” comes in different forms that are described by the following elements of the resource data description data model:
* “resource_data_type”: “string” // vocabulary of types [“metadata”, “paradata”, …]
* “payload_schema_format”: “string” // schema MIME type

While there are many payload_schema_formats that could be encountered, it is important to be familiar with the [common data schema formats](https://github.com/LearningRegistry/LearningRegistry/wiki/Common-Data-Schema-Formats-in-Learning-Registry) that are found in the Learning Registry.

Below is a python code example that parses records based on payload_schema_formats:
```
def process_envelope(envelope):
    print(envelope['doc_ID'])
    schemas = {schema.lower() for schema in envelope.get('payload_schema', [])}
    try:
        if 'lom' in schemas:
            process_lom(envelope)
        elif 'nsdl_dc' in schemas:
            process_nsdl_dc(envelope)
        elif 'lrmi' in schemas:
            process_lrmi(envelope)
        elif 'comm_para 1.0' in schemas:
            process_comm_para(envelope)
    except Exception as ex:
        print(ex)
        print("Error In Payload")
```

See https://gist.github.com/wegrata/6295401 for the full python code example.