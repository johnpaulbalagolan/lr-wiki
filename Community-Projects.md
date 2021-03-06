Have you built a utility for Learning Registry? Have you extended core Learning Registry? Have you done something cool with Learning Registry? Please list it on this page.

We are using Apache 2: http://www.apache.org/licenses/LICENSE-2.0.html to license code.  We prefer if community contributions used that as well.  However, we understand there may be situations where this might not be possible and we will take that into account if your contribution needs to be merged into core code.

### EasyPublish
EasyPublish is a streamlined publishing tool that permits publication of new and edited metadata using the LRMI and Schema.org vocabularies. EasyPublish is installed on [sandbox](https://sandbox.learningregistry.org/apps/EasyPublish) and [node01](https://node01.public.learningregistry.net/apps/EasyPublish).

> License: Apache 2

> Author: [SRI International](https://github.com/easypublish/)

> Tech Info: Javascript, Node.js, Data Services

> * [Interface Source Code](https://github.com/easypublish/EasyPublish/)

> * [Data Service Source Code](https://github.com/easypublish/EasyPublish-DataServices)


### LRMI Publish
LRMI Publish is a modification to the Learning Registry node software that enhances the publish service to optionally validate HTML Microdata JSON encoded content against Schema.org and LRMI vocabularies to permit discovery by InBloom's Learning Registry Index.

> License: Apache 2

> Author: [SRI International](https://github.com/easypublish/)

> Tech Info: Python

> * [LRMIPublish Source Code](https://github.com/easypublish/LearningRegistry/tree/LRMIPublish)

> * [JSON Schema Generator for Schema.org + LRMI](https://github.com/easypublish/schema-dot-org-json-schema-generator)

### AMPlified Search for Chrome™ (AMPS)
AMPS is a Chrome browser extension that examines your Google™ search results and uses Learning Registry metadata and paradata to identify Learning Resources with the resource's alignment to standards information and social activity data.
Additional standards information is located via Jes&Co. Identified resources will have the additional data displayed inline, but beneath each search result.

> License: Apache 2

> Author: [Jim Klo](https://github.com/jimklo/) (SRI International)

> Tech Info: Javascript

> * [Source Code](https://github.com/jimklo/AMPS-Chrome/)

> Type: Demonstration

### LearningRegistrar (Plugfest 2)
LearningRegistrar is a few-click solution to placing any internet accessible document into the Learning Registry. It uses Eduworks' 3rd party service, Metaglance, to extract and generate metadata about the document you are currently viewing, and provides a simple solution to placing new entries into the Learning Registry.

> Download: [Google Web Store](https://chrome.google.com/webstore/detail/dgmkkepjoajjfkdjkjbonbiidcbegiio?hl=en&gl=US)

> License: Apache 2

> Author: Fritz Ray @ [Eduworks](http://www.eduworks.com)

> Tech Info: Javascript

> * [Source Code](https://github.com/Lomilar/LearningRegistrar)

### Plugfest 1 Hackday - Browser Plugin
A prototype that injects learning registry resource data into internet search results.

> Author: [Pat Lockley](https://github.com/patlockley/)

> Tech Info: Javascript

> * [Project Information](http://blogs.cetis.ac.uk/othervoices/2011/08/11/learning-registry-plugfest-report-and-developments/)

> * [Chrome Plugin Source](https://github.com/patlockley/learning_registry_chrome)

> * [Firefox Plugin Source](https://github.com/patlockley/learning_registry_firefox)

> Type: Demonstration

### Educational Resources Discoverer
ERD (Educational Resources Discoverer) is a Chrome™ browser extension that injects custom-rich-snippets in Google™ results pages, containing  "transparent" expansion functionalities to (or suggestions for) "similar" resources (in addition to LRMI metadata). It is "transparent", in the sense that it makes use of (sometimes large numbers of) standards alignments without the need for users to be aware of them. "Similar" resources are identified and ranked according to a similarity metrics, defined as the number of shared alignments to educational standards.

The objective of this first prototype / proof of concept, is to share one of the ideas being developed in the context of an analysis of strategies employed by educators to discover educational resources: any feedback welcome!

The current implementation relies on the powerful [Extract Data Services](https://github.com/LearningRegistry/LearningRegistry/tree/master/data_services) of the Learning Registry (many thanks to [Steve Midgley](https://github.com/science), [Joe Hobson](https://github.com/joehobson), [Jim Klo](https://github.com/jimklo) and [Douglas McAuliffe](https://github.com/douglasmcauliffe)). Metadata about learning resources, again obtained from the Learning Registry, are injected in the snippets via an extension content script, along the lines of the "[Browser Plugin](Community-Projects#plugfest-1-hackday---browser-plugin)" ([Pat Lockley](https://github.com/patlockley/)) and "[AMPS](Community-Projects#amplified-search-for-chrome-amps)" ([Jim Klo](https://github.com/jimklo)) demonstrations reported in this page.

> License: Apache 2

> Author: [Renato Cortinovis](https://github.com/renatomario) (The Open University - KMi)

> Tech Info: Javascript

> * [Documentation including representative screen shots](https://github.com/renatomario/ERD/blob/master/README.md)

> * [Source Code](https://github.com/renatomario/ERD)

> Type: prototype / proof of concept


### Repofringe 2011 Hackday - Visual Browser
Built against a modified version of the node distribution, provides a very simple visual interface to search a
node for specific terms and identify resources that have been tagged with common keys.

> License: Apache 2

> Author: [Jim Klo](https://github.com/jimklo/) (SRI International)

> Tech Info: Javascript and HTML5

> * [Source Code](https://github.com/jimklo/LearningRegistry/tree/RepoFringe)

> Type: Demonstration

### Learning Registry Browser
Adapted from Jim Klo's Visual Browser - allows users to perform a search using a key or identity. Results are displayed both as a list of documents and as a graph of related terms found in those documents. The graph can be used to explore further related terms, allowing the user to explore the semantic landscape of the Learning Registry. Document display summarizes Learning Registry entries for discovered documents, links to full Learning Registry documents, to described Learning Resources, and to related paradata.

The Browser is running here:
http://demolearningregistry.sri.com/browse/

> License: Apache 2

> Author: [John Brecht](https://github.com/jbrecht/) (SRI International)

> Tech Info: Javascript and HTML5

> * [Source Code](https://github.com/jbrecht/lrbrowser)

> Type: Demonstration

### Learning Registry Drupal Module
This project is a module to plug into the content management capabilities of Drupal and publish/consume resources from the Learning Registry.

> License: GPL

> Tech Info: PHP and Drupal 6

> Authors: [Ali Lotia](https://github.com/lotia), [Kevin Coffman](http://drupal.org/user/1016508) and [Jason Hoekstra](http://drupal.org/user/589254)

> * [Source Code](http://drupal.org/sandbox/jasonh/1342822)

### LRphpLib

A modern library for accessing the core LR services in php, [following http://www.php-fig.org/psr/psr-4/](PSR-4) coding standards to allow autoloading, and configured to be installed with dependencies via composer. Several examples are included to demonstrate a variety of options accessing LR services.


> License: Apache 2

> Authors: [Pat Lockley](https://github.com/patlockley/) and [Navigation North](http://navigationnorth.com)

> Tech Info: Requires PHP 5.4+

> [Source Code](https://github.com/navnorth/LRphpLib)


### LRPHP - legacy LR php library
A drop-in client-side library and programming interface for a Learning Registry node.  Currently supporting slice, obtain and publish services.

> License: Apache 2

> Authors: [Jeffrey Hill](https://github.com/jeffreyhill/) (Tennessee Curriculum Center), [Jason Hoekstra](https://github.com/jasonhoekstra)

> Tech Info: Requires PHP 5.2+ and PEAR Crypt_GPG library for resource signing

> * [Source Code](https://github.com/jeffreyhill/LRPHP)

### LRJavaLib
Java library for accessing core services for a node, including publishing and consuming data. Base classes are in place and functions are being expanded incrementally. Data consumption will be expanded to support a variety of data schema.

> Language: Java

> License: Apache 2

> Author: [Navigation North](http://www.navigationnorth.com/)

> * [Source Code](https://github.com/navnorth/LRJavaLib)

### LR.Net
LR.Net is a client library for the Learning Registry project. It is written in C# and provides basic access to a Learning Registry node. Currently, obtain, publish, and harvest are supported, with plans to implement slice in the near future.

> Language: C# .Net

> License: Apache 2

> Author: [Rob Chadwick](robert.chadwick.ctr@adlnet.gov), [ADL](https://github.com/adlnet/), Austin Montoya, [ADL](https://github.com/adlnet/)

> * [Source Code](https://github.com/adlnet/LR.Net)

### LR Publisher
LR Publisher is a graphical user interface designed for publishing resource description documents to a Learning Registry node. It is designed to ease with development and testing of the Learning Registry service APIs, as well as to familiarize new users to the data model of the LR.

> Language: C# .Net

> License: Apache 2

> Author: Austin Montoya, [ADL](https://github.com/adlnet/)

> * [Source Code](https://github.com/adlnet/lr-publisher)

### LRDataPump
Harvests an OAI-PMH NSDL_DC repository and publishes as signed LR resource data to a specific node. Originally this utility was designed to work as a differential task, with subsequent execution harvesting from the configured repository since the last successful harvest. NSDL developers have recently updated the tool to synchronize an OAI feed with the LR, updating, deleting and creating documents as necessary. The datapump code also includes the transforms they use to go from NSDL_DC -> LRMI JSON-LD, and COMM_ANNO/COMM_PARA -> LRParadata 1.0. Other features that were added are documented both in the README file and in the code.

> Language: Python

> License: Apache 2

> Current Author: [UCAR / NSDL](http://nsdl.org/)

> Original Author: [Jim Klo](https://github.com/jimklo/) (SRI International)

> * [Source Code](https://github.com/UCAR/DLS_lr-data-pump)

> * [Documentation](https://github.com/UCAR/DLS_lr-data-pump/tree/master/datapump/docs)

> Type: Data Pump

### LRSignature
Extendable Python library and command line tools that can be used to sign LR resource data documents.

> Language: Python

> License: Apache 2

> Author: [Jim Klo](https://github.com/jimklo/) (SRI International)

> * [Source Code](https://github.com/jimklo/LRSignature)

> Type: Signing Library

### LRMonitor
A Python module that can query CouchDB status message and format into a suitable format to be digested by Cacti.

> Language: Python

> License: Apache 2

> Author: [Jim Klo](https://github.com/jimklo/) (SRI International)

> * [Source Code](https://github.com/jimklo/LRMonitor)

> Type: Node Administration

### Moodle4BLTI_LR
Publish/Browse/Use BasicLTI tools from Moodle. The idea is to publish tools in Learning Registry, using BasicLTI (http://www.imsglobal.org/lti/). Then in LR can share not only static content but tools. To launch remote tools the mechanism is BasicLTI.

> Language: PHP

> License: GPL2

> Author: [Antoni Bertran] (http://sourceforge.net/users/antonib) [Universitat Oberta de Catalunya](http://www.uoc.edu)

> * Project page: http://sourceforge.net/projects/learningapps

> * Wiki: https://sourceforge.net/apps/mediawiki/learningapps/index.php?title=Moodle4BLTI_LR_English#Learning_Registry_Integration

> * [Source Code](https://sourceforge.net/scm/?type=svn&group_id=388815) SVN

> * Demo Video http://vimeo.com/32982697


### LR-Data
This is a small utility to help pull the data from the Learning Registry into a datastore of you choice.

> Language: Python, RabbitMQ, Redis, Celery

> License: Apache 2

> Author: [Walt Grata](https://github.com/wegrata) ([ADL](https://github.com/adlnet/))

> * [Source Code](https://github.com/adlnet/lr-data)

> Type: Utility


### LR Node Explorer
This is a utility to explore a Learning Registry node.

Node Explorer is running here:
http://jlern.iriscouch.com/resource_data/_design/explorer/start.html

> License: Apache 2

> Author: [Nick Syrotiuk](https://github.com/sefnyn) ([JLeRN](https://github.com/jlern))

> * [Source Code](https://github.com/jlern)

> Type: Utility

### LRNodeJS / Common Core State Standards Browser
A basic browser of academic content standards, built as an example of accessing couchDB and LR data using Node.js apps. Standards data can be easily imported from [Jes & Co](http://asn.jesandco.org/). Resources aligned to each standard are displayed, as pulled from a LR data service (configurable).

> Language: Node.js

> License: Apache 2

> Author: [Navigation North](http://www.navigationnorth.com/)

> * [Source Code](https://github.com/navnorth/LRNodeJS)
