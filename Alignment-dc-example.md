Full example in the Learning Registry of using DC conformsTo element based on [NSDL_DC guidelines](http://nsdl.org/contribute/metadata-guide) to align a resource to an academic standard:

> https://node01.public.learningregistry.net/harvest/getrecord?by_doc_ID=t&request_ID=00031c9545e5430aaf407889c98de376

Below is a snippet from this record highlighting the alignment (i.e., conformsTo) elements.

```xml

<nsdl_dc:nsdl_dc xmlns:nsdl_dc="http://ns.nsdl.org/nsdl_dc_v1.02/" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:dct="http://purl.org/dc/terms/" xmlns:ieee="http://www.ieee.org/xsd/LOMv1p0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" schemaVersion="1.02.020" xsi:schemaLocation="http://ns.nsdl.org/nsdl_dc_v1.02/ http://ns.nsdl.org/schemas/nsdl_dc/nsdl_dc_v1.02.xsd">

...

<dct:conformsTo xsi:type="dct:URI">http://purl.org/ASN/resources/S1143426</dct:conformsTo>
<dct:conformsTo xsi:type="dct:URI">http://purl.org/ASN/resources/S1143460</dct:conformsTo>
<dct:conformsTo xsi:type="dct:URI">http://purl.org/ASN/resources/S1143462</dct:conformsTo>

```