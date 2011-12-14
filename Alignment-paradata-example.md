Recipe for Standards Alignment/Matching
This recipe shows paradata for an educator matching a resource to an academic content standard. Information about the standard, including ASN id, is included in the related object space. The verb used here was chosen by the Brokers of Expertise portal to indicate based on their own agreed upon levels of alignment: recommended, matched, and aligned. At some point we should consider a system of listing synonyms for verbs, actors, objectTypes, etc.

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