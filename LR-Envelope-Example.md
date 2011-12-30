Below is an excerpt describing the resource data description model (envelope) from the [Learning Registry Technical Specification v0.23.0](https://docs.google.com/document/d/1fRbDpM0BKvNc4WzDzX0pNUpfPtFAsKpKGnOyRhRok-8/edit?hl=en_US):

```javascript
{
 "doc_type":		"resource_data",	// the literal "resource_data"
						// required, immutable
 "doc_version":		"0.23.0",		// the literal for the current spec version -- "0.23.0"
						// required, immutable

 // general elements about the submission
 "doc_ID":		"string",		// unique ID for this resource data description document
						// unique within scope of the LR
						// immutable
						// user optional, required for storage
						// system generated when publishing
						// the document if not provided
 "resource_data_type":	"string",		// open (best practices) vocabulary
						// ["metadata", "paradata", "resource", "assertion", ...]
						// required, immutable
 "active":		boolean,		// is the resource data description document active
						// required, mutable from T to F only

 // information about the submission, independent of the resource data
 "identity": {					// identity and curation
  "submitter_type":	"string",		// fixed vocabulary ["anonymous", "user", "agent"]
						// required, immutable
						// "anonymous" -- submitter is unknown
						// "user" -- submitter is a user or has a user identity
						// "agent" -- submitter is an agent, e.g., a repository, LMS
						// or an organization
  "submitter":		"string",		// identity of the submitter of the resource data
						// required, immutable
						// use "anonymous" for type "anonymous"
  "curator":		"string",		// identity of the curator of the resource data description
						// who manages the resource data description
						// optional
  "owner":		"string",		// identity of the owner of the resource
						// who owns what is referenced in the resource locator
						// optional
  "signer":		"string"		// identity of key owner used to sign the submission
						// optional
	},

// submission and distribution workflow information
 "submitter_timestamp":	"string",		// submitter-created timestamp
						// time/date encoding
						// optional
 "submitter_TTL":	"string",		// submitter statement of TTL of validity of submission
						// time/date encoding
						// optional
 "publishing_node":	"string",		// node_id of node where injected into the network
						// required
						// provided by the initial publish node (not distribution)
 "create_timestamp":	"string",		// timestamp of when first published to the network
						// independent of updates
						// time/date encoding
						// required, immutable
						// provided by the initial publishing node on first publish
						// not by a distribution node or not an update
"TOS": {					// terms of service
  "submission_TOS":	"string",		// agreed terms of service by submitter
						// required
 "submission_attribution":"string"		// attribution statement from submitter
						// optional
 },

 "do_not_distribute":	"string",		// system provided key-value pair
						// optional

 "weight":		"integer",		// submitter assigned weight (strength)
						// -100:100
						// optional
"digital_signature": { 				// digital signature of the submission, optional
  "signature":		"string",		// signature string, required
   "key_location":	["string"],		// array of public key locations,, required
  "signing_method":	"string"		// fixed vocabulary ["LR-PGP.1.0"]
						// required
  },

 // information about the resource, independent of the resource data
 "resource_locator":	"string",		// unique locator for the resource described
						// SHALL resolve to a single unique resource
						// required
 "keys":		["string"],		// array of hashtag, keyword value list used for filtering
						// optional
 "resource_TTL":	integer,		// TTL from resource owner for the resource itself, in days
						// optional

// the actual resource data description elements
// these elements are optional as a block if the submission is a resource
 "payload_placement":	"string",		// fixed vocabulary ["inline", "linked", "attached"]
						// "inline" -- resource data is in an object that follows
						// "linked" -- resource data is at the link provided
						// "attached" -- resource data is in an attachment
						// required
 "payload_schema":	["string"],		// array of  schema description/keywords
						// for the resource data
						// required
						// defined metadata schema values
						// defined paradata schema values
 "payload_schema_locator":"string",		// schema locator for the resource data
						// optional
 "payload_schema_format":"string",		// schema MIME type
						// optional
 "payload_locator":	"string",		// locator if payload_placement value  is "linked"
						// required if "linked", otherwise ignored
 "resource_data":				// the actual inline resource data
 <the resource data object>,	 		// the resource data itself (resource. metadata, paradata)
						// maybe a JSON object, or
						// a string encoding XML or some other format, or
						// a string encoding binary
						// required if "inline" otherwise ignored
 "X_xxx":		?????			// placeholder for extensibility, optional
}
```

Here is a link to an envelope in the LR where the metadata is NSDL_DC and it is located inline: https://node01.public.learningregistry.net/harvest/getrecord?by_doc_ID=t&request_ID=00031c9545e5430aaf407889c98de376

Captured below is resource_data fragment from the link above.

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