In much the same way that the original developers of the Internet chose not to specify which data should flow through their networks, the Learning Registry has taken a similar approach to the format of data that resides on its nodes. The Learning Registry is **schema agnostic**. Data schema and formats change over time based on the needs of the users and applications, so it is not our place to determine which should be supported or how you can make use of them. The LR focuses on the services and infrastructure for sharing that data, leaving the implementation specifics to those closest to the data itself. By encapsulating resource information in a data envelope with specific elements describing only the fields necessary for transport and trust (publisher identity, keywords, schema, etc.), the LR focuses on moving that data between publishers and nodes, leaving the implementation specifics to be determined by the consumer.

Below are some of the **more common schema** in use currently within the Learning Registry.

NOTE: Examples are links to JSON records found in the Learning Registry.  Using a viewer such as jsonview is recommended if examples are clicked in a browser.

## Learning Resource Metadata Initiative (LRMI)

Co-led by the Association of Educational Publishers–the 501(c)(3) division of the Association of American Publishers–and Creative Commons, and funded by the Bill & Melinda Gates Foundation and the William and Flora Hewlett Foundation, the LRMI has developed a common metadata framework for describing or “tagging” learning resources on the web.  LRMI is represented as microdata.  LRMI found in the Learning Registry is in the form of [JSON formatted HTML Microdata](http://www.w3.org/TR/microdata/#json) and [JSON Linked Data (JSON-LD)](http://json-ld.org/).

> More information on LRMI: http://www.lrmi.net/the-specification

> Example: https://node02.public.learningregistry.net/obtain?request_id=http://www.einstein.caltech.edu/

## Dublin Core (NSDL Variant)

A very flexible metadata standard for describing a full range of web resources. Within the LR, the nsdl_dc variant is a very popular schema extension for describing the educational aspects of resources, including standards alignment data.

> More information on nsdl_dc: http://nsdl.org/contribute/metadata-guide

> Example: http://goo.gl/jYpgY

## Learning Object Metadata (LOM)

LOM is a common method for exchanging metadata about learning resources, with the aim towards supporting reusability. One data variant that uses LOM as a base for its metadata is the Learning Resource Exchange (LRE). With over 500,000 records in the Learning Registry using this schema,

> More information on LRE: http://lreforschools.eun.org/web/guest/metadata

> Example: http://goo.gl/mkyGI


## NSDL comm_para

The comm_para XML schema was developed by NSDL as a means of capturing the use of a resource (e.g. downloadd, favorited, rated, etc). It is particularly useful in reporting aggregate usage information across a date range using a controlled vocabulary.

> More information on comm_para: https://wiki.ucar.edu/x/86qrB

> Example: http://goo.gl/f0q1Y

## LR Paradata

Based on the Activity Streams specification, the Learning Registry core team developed the LR Paradata JSON-based schema for sharing usage information about resources. The flexibility of this approach allows for an open vocabulary and lends itself well to reporting on single user actions in real-time. This format is also being used to publish assertions about people and resources in the system to establish, trust, similarity, and resource updates.

> More information: http://goo.gl/Cq6im

> Example usage data: http://goo.gl/L1hyl

> Example assertion data: http://goo.gl/6unRi