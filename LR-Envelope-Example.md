Visit the [Resource Data Description Model (envelope) section](https://docs.google.com/document/d/1fRbDpM0BKvNc4WzDzX0pNUpfPtFAsKpKGnOyRhRok-8/edit?hl=en_US&pli=1#heading=h.kdtam7-568cce) of the [Learning Registry Technical Specification v0.23.0](https://docs.google.com/document/d/1fRbDpM0BKvNc4WzDzX0pNUpfPtFAsKpKGnOyRhRok-8/edit?hl=en_US) to get a sense for the LR envelope requirements.

Here is a link to an envelope in the LR where the metadata is NSDL_DC and it is located inline: https://node01.public.learningregistry.net/harvest/getrecord?by_doc_ID=t&request_ID=00031c9545e5430aaf407889c98de376

Captured below is the resource_data (envelope) fragment from the link above.

```javascript
{
    "update_timestamp": "2011-10-28T00:24:12.978348Z",
    "keys": [
        "dlese.org",
        "Astronomy",
        "Oceanography",
        "Geology",
        "Science",
        "Middle School",
        "High School",
        "tombolo",
        "en",
        "Physical oceanography",
        "Chemical oceanography",
        "DLESE Community Collection",
        "Physical sciences",
        "Chemistry",
        "Space sciences",
        "History of science",
        "Earth science"
    ],
    "TOS": {
        "submission_attribution": "The National Science Digital Library",
        "submission_TOS": "http://nsdl.org/help/?pager=termsofuse"
    },
    "_rev": "1-e5dcb6f247d0c354e67507b2e3ca3bcd",
    "payload_placement": "inline",
    "node_timestamp": "2011-10-28T00:24:12.978348Z",
    "create_timestamp": "2011-10-28T00:24:12.978348Z",
    "active": true,
    "publishing_node": "cad60ef7493246868f6394fa764397c3",
    "resource_locator": "http://www.amnh.org/nationalcenter/youngnaturalistawards/2001/madeline.html",
    "identity": {
        "signer": "The National Science Digital Library <nsdlsupport@nsdl.ucar.edu>",
        "submitter": "SRI International on behalf of The National Science Digital Library",
        "submitter_type": "agent",
        "curator": "The National Science Digital Library"
    },
    "doc_type": "resource_data",
    "resource_data": [nsdl_dc xml metadata removed from this excerpt],
    "resource_data_type": "metadata",
    "payload_schema_locator": "http://ns.nsdl.org/nsdl_dc_v1.02/ http://ns.nsdl.org/schemas/nsdl_dc/nsdl_dc_v1.02.xsd",
    "payload_schema": [
        "nsdl_dc"
    ],
    "digital_signature": {
        "key_location": [
            "http://pool.sks-keyservers.net:11371/pks/lookup?op=get&search=0xBFF13965146B1740",
            "https://keyserver2.pgp.com/vkd/DownloadKey.event?keyid=0xBFF13965146B1740"
        ],
        "key_owner": "The National Science Digital Library <nsdlsupport@nsdl.ucar.edu>",
        "signing_method": "LR-PGP.1.0",
        "signature": "-----BEGIN PGP SIGNED MESSAGE-----\nHash: SHA1\n\n66eb5b19b0f63339cd6a9370751d327308271ba1691c754c4c3e67b6fbafdeb2\n-----BEGIN PGP SIGNATURE-----\nVersion: GnuPG v1.4.10 (GNU/Linux)\n\niQIcBAEBAgAGBQJOqfYlAAoJEN3QUpzaJ39HgR0QAI0YbjTdQBDl19NKkp+e/fQc\nEopA26Ln7g701jZJht7LVp8/k6XOqTctivK64SRUc9fazpqPclopm1iMexsrRjX0\ncjsqdODAt6zvE2Q4sp+q6y6V+QO2gFzQv0o1uGyjmEd7e1lzbKoNd6M+vMOVXm7+\nu0EhAZES4BuUkv2+5+kK5DBK6uX8ykIfwJqd3n2WuQf9LcS6/BaQ1gdzJPQNw85Y\nIg9GJO/Lcy26ecsRQJbZ5kB24VUNN5jCG7sOA28Q6nrMZnHf3ghCaMk82/I3Wpst\nKaJpxO/LvzLCSWuoTfol4qwUreRtqWyzMcOUaymryinuZxobWKnhW8jRdGZmy5Ww\nuXuLlH/g0qcU+5DcqDzGlpG1HDLA5xKxcwodFa5JzGHoHf5rNKAgxzDY2lheydeu\n+yTCR0ivjIpo13H3juEBRvW8CZyARwMwbR0o+Dh82GWKQ5DnSXVAMf2e+fbjkhKx\nvE/O2OJfRq/cQri7sBcErPHOj0M5oWecrLAAl3aeC+uJBcdG4f3DulQbNI7fv7r5\nWiPI1WZxbLybV33OiASvYQKktcsTesHPUjQfSNCdZjC4wP+WBMyEpxzN+cbM3SFD\nJwXCy4PkXzdvoKpC7lGCZhMBgZ0rBJS1PIjcFscpVM86J9VryH3tr+yKt/M4AZmi\n07GQaOXvyK98UOflMFjV\n=fUkE\n-----END PGP SIGNATURE-----\n"
    },
    "doc_version": "0.23.0",
    "_id": "00031c9545e5430aaf407889c98de376",
    "doc_ID": "00031c9545e5430aaf407889c98de376"
}
```