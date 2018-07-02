The following resource data description document accurately models a "same as" relationship using the new LR Paradata Specification 1.0:

> http://sandbox.learningregistry.org/harvest/getrecord?request_ID=87949045ae2c4cbfb40cb408ac65b558&by_doc_ID=true

For convenience, the inline `resource_data` is replicated here:

```javascript
{
    "activity": {
        "actor": "Austin Montoya",
        "object": {
            "id": "http://www.google.com",
            "objectType": "resource"
        },
        "content": "Austin Montoya asserts http://www.google.com is identical to http://www.yahoo.com",
        "verb": "same as",
        "related": [
            {
                "object": {
                    "id": "http://www.yahoo.com",
                    "objectType": "resource"
                }
            }
        ]
    }
}
```

A small python app illustrating how to construct an assertion document will be provided soon.