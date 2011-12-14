The following resource data description document accurately models a "same as" relationship using RDF instead of the LR Paradata 1.0 format. The full document can be found here:

> http://sandbox.learningregistry.org/harvest/getrecord?request_ID=3c648ac64b2f44e9a9e07d4e65356698&by_doc_ID=true

The most relevant part of the document, the inline `resource_data`, has been replicated here for convenience. 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF xmlns:lr="http://qedev.dyndns.org/lr#"
         xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#">
   <rdf:Description rdf:about="http://google.com">   
      <lr:similarResource rdf:resource="http://yahoo.com"/>
   </rdf:Description>
</rdf:RDF>
```

The `lr` namespace is defined in a simple schema file and contains only one definition for `similarResource`, again replicated here for simplification:

```xml
<?xml version="1.0" ?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:element name="similarResource" type="xs:string" />
</xs:schema>
```