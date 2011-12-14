This example is based on a recipe from the [Paradata Cookbook](https://docs.google.com/document/d/1lggCnowWsDgQxrNjYRAgh2KNwKfq-MV8vLJzRXbAaos/edit?hl=en_US), which shows an assertion from a Learning Management System (LMS) endorsing a group. Assertions like this can be particularly helpful when creating trust relationships between systems, especially in the realm of standards alignments and other expert opinions. Information about the group, including id/url, is included in the object space.

Other terms that may be considered valid synonyms for similar actions: vouch, certify, affirm.

```javascript
{
    "activity": {
        "actor": {
            "displayName": "Brokers of Expertise", 
            "id": "http://myboe.org", 
            "objectType": "LMS"
        }, 
        "object": {
            "id": "http://myboe.org/go/groups/standards_matchers",
            "displayName":"Brokers of Expertise Standards Matchers",
            "objectType":"group"
        },
        "verb": {
            "action": "endorse",
            "date": "2011-12-14",
            "content": "The Brokers of Expertise Standards Matchers group found at http://myboe.org/go/groups/standards_matchers was endorsed by the administrators of the Brokers of Expertise Learning Management System."
        }
    }
}
```
