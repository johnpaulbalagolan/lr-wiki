Visit the [Resource Data Description Model (envelope) section](https://docs.google.com/document/d/1fRbDpM0BKvNc4WzDzX0pNUpfPtFAsKpKGnOyRhRok-8/edit?hl=en_US&pli=1#heading=h.kdtam7-568cce) of the [Learning Registry Technical Specification v0.23.0](https://docs.google.com/document/d/1fRbDpM0BKvNc4WzDzX0pNUpfPtFAsKpKGnOyRhRok-8/edit?hl=en_US) to get a sense for the LR envelope requirements.

Here is a link to a resource data description document (envelope) in the Learning Registry where the metadata uses the NSDL_DC format located inline: 

> http://sandbox.learningregistry.org/obtain?request_id=77d1e7a401da4dd7b00806d37ac7d81a&by_doc_ID=T

This document is shown below 1) before it was signed, 2) after it was signed, and 3) after the published document was downloaded.

Here is the resource data description document (envelope) before it was signed:

```javascript
{
    "TOS": {
        "submission_TOS": "http://www.learningregistry.org/tos/cc0/v0-5/"
    },
    "active": true,
    "doc_type": "resource_data",
    "doc_version": "0.23.0",
    "identity": {
        "curator": "Damon Regan",
        "owner": "Khan Academy",
        "submitter": "Damon Regan",
        "signer": "Damon Regan",
        "submitter_type": "user"
    },
    "keys": [
        "khan academy",
        "math",
        "subtracting fractions"
    ],
    "resource_locator": "http://www.khanacademy.org/video/subtracting--fractions?topic=developmental-math-1",
    "resource_data_type": "metadata",
    "payload_placement": "inline",
    "payload_schema_locator": "http://ns.nsdl.org/nsdl_dc_v1.02/ http://ns.nsdl.org/schemas/nsdl_dc/nsdl_dc_v1.02.xsd",
    "payload_schema": [
        "nsdl_dc"
    ],
    "resource_data": "<nsdl_dc:nsdl_dc xmlns:nsdl_dc=\"http://ns.nsdl.org/nsdl_dc_v1.02/\" xmlns:dc=\"http://purl.org/dc/elements/1.1/\" xmlns:dct=\"http://purl.org/dc/terms/\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://www.openarchives.org/OAI/2.0/\" schemaVersion=\"1.02.000\" xsi:schemaLocation=\"http://ns.nsdl.org/nsdl_dc_v1.02/ http://ns.nsdl.org/schemas/nsdl_dc/nsdl_dc_v1.02.xsd\">  <dc:title>Subtracting Fractions</dc:title><dc:identifier xsi:type=\"dct:URI\">http://www.khanacademy.org/video/subtracting--fractions?topic=developmental-math-1</dc:identifier><dc:subject>Developmental Math</dc:subject><dct:educationLevel xsi:type=\"nsdl_dc:NSDLEdLevel\">Informal Education</dct:educationLevel><dc:description>A 2 minute video from Salman Khan explaining how to subtract fractions.</dc:description><dc:type xsi:type=\"nsdl_dc:NSDLType\"\">Lecture/Presentation</dc:type><dc:type xsi:type=\"nsdl_dc:NSDLType\">Tutorial</dc:type><dc:type xsi:type=\"nsdl_dc:NSDLType\">Audio/Visual</dc:type><dc:type>Video</dc:type><dc:rights>http://www.khanacademy.org/about/tos</dc:rights><dc:format xsi:type=\"dct:IMT\">video/x-flv</dc:format><dc:language xsi:type=\"dct:RFC3066\">en</dc:language><dc:publisher>Khan Academy</dc:publisher></nsdl_dc:nsdl_dc>"
}
```

Here is the same document envelope after it has been signed:

```javascript
{
    "documents": [
        {
            "doc_type": "resource_data",
            "digital_signature": {
                "key_location": [
                    "http://www.damonregan.com/gpg/public-key.txt"
                ],
                "key_owner": "Damon Regan <damon.regan.ctr@adlnet.gov>",
                "signing_method": "LR-PGP.1.0",
                "signature": "-----BEGIN PGP SIGNED MESSAGE-----\r\nHash: SHA1\r\n\r\n592858196e94f6b6b03d29f3ed566a95018275fdaa311133c8bd24e48657c960\r\n-----BEGIN PGP SIGNATURE-----\r\nVersion: GnuPG v2.0.17 (MingW32)\r\n\r\niQEcBAEBAgAGBQJPOT9rAAoJEHSrmNzJkYrV3CcIAK77voixvNpgPm2a/vQdj7zF\r\nZRUeqez3nqPVw09/yNB/ZKhsx7DrjShESiuqZU+JO4IaRa2CdXnp+rVrLBMad2Kg\r\n82EYFGbVi0TG4OLpMSd/rYvx3QtGrfyL5cyOHElKAeIlYDb6cbTO/yP7CQ9gRo36\r\nEQndAQceGeg64wtQGrcFHIk8L1rEQ8k2KWezBEh+gLQCckiOSjn2DUIPDBwwT5vA\r\nwyjT02pH9nZTsR3zbBxw9Oii7vNZDYPj1iok4cFR2/uZhpON3DfQCKAhiKvhvErI\r\nDStEQb4Ou9qn0Du+gIe8K9SeRXYRTEq3SDcuMAug0F8I5b9x3RfVHR33fLnr0Yw=\r\n=okni\r\n-----END PGP SIGNATURE-----\r\n"
            },
            "resource_data": "<nsdl_dc:nsdl_dc xmlns:nsdl_dc=\"http://ns.nsdl.org/nsdl_dc_v1.02/\" xmlns:dc=\"http://purl.org/dc/elements/1.1/\" xmlns:dct=\"http://purl.org/dc/terms/\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://www.openarchives.org/OAI/2.0/\" schemaVersion=\"1.02.000\" xsi:schemaLocation=\"http://ns.nsdl.org/nsdl_dc_v1.02/ http://ns.nsdl.org/schemas/nsdl_dc/nsdl_dc_v1.02.xsd\">  <dc:title>Subtracting Fractions</dc:title><dc:identifier xsi:type=\"dct:URI\">http://www.khanacademy.org/video/subtracting--fractions?topic=developmental-math-1</dc:identifier><dc:subject>Developmental Math</dc:subject><dct:educationLevel xsi:type=\"nsdl_dc:NSDLEdLevel\">Informal Education</dct:educationLevel><dc:description>A 2 minute video from Salman Khan explaining how to subtract fractions.</dc:description><dc:type xsi:type=\"nsdl_dc:NSDLType\"\">Lecture/Presentation</dc:type><dc:type xsi:type=\"nsdl_dc:NSDLType\">Tutorial</dc:type><dc:type xsi:type=\"nsdl_dc:NSDLType\">Audio/Visual</dc:type><dc:type>Video</dc:type><dc:rights>http://www.khanacademy.org/about/tos</dc:rights><dc:format xsi:type=\"dct:IMT\">video/x-flv</dc:format><dc:language xsi:type=\"dct:RFC3066\">en</dc:language><dc:publisher>Khan Academy</dc:publisher></nsdl_dc:nsdl_dc>",
            "keys": [
                "khan academy",
                "math",
                "subtracting fractions",
                "lr-test-data"
            ],
            "TOS": {
                "submission_TOS": "http://www.learningregistry.org/tos/cc0/v0-5/"
            },
            "resource_data_type": "metadata",
            "payload_schema_locator": "http://ns.nsdl.org/nsdl_dc_v1.02/ http://ns.nsdl.org/schemas/nsdl_dc/nsdl_dc_v1.02.xsd",
            "payload_placement": "inline",
            "payload_schema": [
                "nsdl_dc"
            ],
            "doc_version": "0.23.0",
            "active": true,
            "resource_locator": "http://www.khanacademy.org/video/subtracting--fractions?topic=developmental-math-1",
            "identity": {
                "owner": "Khan Academy",
                "submitter": "Damon Regan",
                "submitter_type": "user",
                "signer": "Damon Regan",
                "curator": "Damon Regan"
            }
        }
    ]
}
```

Finally, here is document envelope after it has been published and downloaded via the Basic Obtain service:

```javascript
{
    "documents": [
        {
            "document": [
                {
                    "doc_type": "resource_data",
                    "resource_locator": "http://www.khanacademy.org/video/subtracting--fractions?topic=developmental-math-1",
                    "resource_data": "<nsdl_dc:nsdl_dc xmlns:nsdl_dc=\"http://ns.nsdl.org/nsdl_dc_v1.02/\" xmlns:dc=\"http://purl.org/dc/elements/1.1/\" xmlns:dct=\"http://purl.org/dc/terms/\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://www.openarchives.org/OAI/2.0/\" schemaVersion=\"1.02.000\" xsi:schemaLocation=\"http://ns.nsdl.org/nsdl_dc_v1.02/ http://ns.nsdl.org/schemas/nsdl_dc/nsdl_dc_v1.02.xsd\">  <dc:title>Subtracting Fractions</dc:title><dc:identifier xsi:type=\"dct:URI\">http://www.khanacademy.org/video/subtracting--fractions?topic=developmental-math-1</dc:identifier><dc:subject>Developmental Math</dc:subject><dct:educationLevel xsi:type=\"nsdl_dc:NSDLEdLevel\">Informal Education</dct:educationLevel><dc:description>A 2 minute video from Salman Khan explaining how to subtract fractions.</dc:description><dc:type xsi:type=\"nsdl_dc:NSDLType\"\">Lecture/Presentation</dc:type><dc:type xsi:type=\"nsdl_dc:NSDLType\">Tutorial</dc:type><dc:type xsi:type=\"nsdl_dc:NSDLType\">Audio/Visual</dc:type><dc:type>Video</dc:type><dc:rights>http://www.khanacademy.org/about/tos</dc:rights><dc:format xsi:type=\"dct:IMT\">video/x-flv</dc:format><dc:language xsi:type=\"dct:RFC3066\">en</dc:language><dc:publisher>Khan Academy</dc:publisher></nsdl_dc:nsdl_dc>",
                    "digital_signature": {
                        "key_location": [
                            "http://www.damonregan.com/gpg/public-key.txt"
                        ],
                        "key_owner": "Damon Regan <damon.regan.ctr@adlnet.gov>",
                        "signing_method": "LR-PGP.1.0",
                        "signature": "-----BEGIN PGP SIGNED MESSAGE-----\r\nHash: SHA1\r\n\r\n592858196e94f6b6b03d29f3ed566a95018275fdaa311133c8bd24e48657c960\r\n-----BEGIN PGP SIGNATURE-----\r\nVersion: GnuPG v2.0.17 (MingW32)\r\n\r\niQEcBAEBAgAGBQJPOWzFAAoJEHSrmNzJkYrVgg0IAMFTh2Vi0JVjfTXxEriqMHRG\r\n9SQmn6qfKK7xLrW38p/RFu1RY0Mo+acET8QWwSDS88gncsXTMS4uRyc4ik9DSl3F\r\nZh8hxLRyxTVuDtLMrZ6cUaq2aazqfD4sN/W3eaL7IZOnWTsRCv1b43/cOVG8TOEC\r\n/X+MQ0+51/bH5LPkKOHsN/HnIbHvKu7+C8sa/JN98Qr2B/TskH9e/27NJSdhfN92\r\n5B2t9TWJNViuOT6NCmuy/M/+l+UHqH2Wd0TE76IuFrH6tZ5WzHLBmzRugk6upqI0\r\nTIqN1fdoR2REh6YioKocQ4SbjYFOhAfrQqJBvvN0nB/35o0IO4MjsHlzNgXEEwU=\r\n=mRsN\r\n-----END PGP SIGNATURE-----\r\n"
                    },
                    "keys": [
                        "khan academy",
                        "math",
                        "subtracting fractions",
                        "lr-test-data"
                    ],
                    "TOS": {
                        "submission_TOS": "http://www.learningregistry.org/tos/cc0/v0-5/"
                    },
                    "_rev": "1-06dd558e8d508b4a2dc2c262f1952e63",
                    "resource_data_type": "metadata",
                    "payload_schema_locator": "http://ns.nsdl.org/nsdl_dc_v1.02/ http://ns.nsdl.org/schemas/nsdl_dc/nsdl_dc_v1.02.xsd",
                    "payload_placement": "inline",
                    "payload_schema": [
                        "nsdl_dc"
                    ],
                    "node_timestamp": "2012-02-13T20:04:18.158773Z",
                    "doc_version": "0.23.0",
                    "create_timestamp": "2012-02-13T20:04:18.158773Z",
                    "update_timestamp": "2012-02-13T20:04:18.158773Z",
                    "active": true,
                    "publishing_node": "f8dc25337708420ca1991d1e8d7d3a05",
                    "_id": "77d1e7a401da4dd7b00806d37ac7d81a",
                    "doc_ID": "77d1e7a401da4dd7b00806d37ac7d81a",
                    "identity": {
                        "owner": "Khan Academy",
                        "submitter": "Damon Regan",
                        "submitter_type": "user",
                        "signer": "Damon Regan",
                        "curator": "Damon Regan"
                    }
                }
            ],
            "doc_ID": "77d1e7a401da4dd7b00806d37ac7d81a"
        }
    ],
    "resumption_token": null
}
```