Full example in the Learning Registry of using LR Paradata 1.0 to align a resource to an academic standard: 

> http://node01.public.learningregistry.net/obtain?request_id=02ba2b367e8b407f900fed2df0061fb5&by_doc_ID=T

This example is based on a recipe from the [Paradata Cookbook](https://docs.google.com/document/d/1lggCnowWsDgQxrNjYRAgh2KNwKfq-MV8vLJzRXbAaos/edit?hl=en_US), which shows paradata for an educator matching a resource to an academic content standard. Information about the standard, including ASN id, is included in the related object space. The verb used here was chosen by the Brokers of Expertise portal to indicate based on their own agreed upon levels of alignment: recommended, matched, and aligned. At some point we should consider a system of listing synonyms for verbs, actors, objectTypes, etc.

```javascript
{
    "activity": {
        "actor": {
            "description": [
                "9",
                "10",
                "English Language Arts"
            ],
            "objectType": "educator"
        },
        "verb": {
            "action": "matched",
            "date": "2011-11-07",
            "context": {
                "id": "http://www.myboe.org/go/resource/7238",
                "description": "Brokers of Expertise resource management page",
                "objectType": "LMS"
            }
        },
        "object": {
            "id": "http://www.readwritethink.org/lessons/lesson_view.asp?id=131"
        },
        "related": [
            {
                "objectType": "academic standard",
                "id": "http://purl.org/ASN/resources/S101282A",
                "content": "Select a focus when writing."
            }
        ],
        "content": "A resource found at http://www.myboe.org/go/resource/7238 was matched to the academic content standard with ID http://purl.org/ASN/resources/S101282A by an educator of multiple grades and English Language Arts on November 7, 2011"
    }
}
```