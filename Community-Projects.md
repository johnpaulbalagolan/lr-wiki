Have you built a utility for Learning Registry? List it on this page.  Have you extended core Learning Registry? List it on this page.  Have you done something cool with Learning Registry? List it on this page.

We are using Apache 2: http://www.apache.org/licenses/LICENSE-2.0.html to license code, we prefer if community contributions used that too. We understand there may be situations where this might not be possible, and we will take that into account if your contribution needs to be merged into core code.

# Demonstrations
Here are some demonstration projects that either extend or augment Learning Registry in some manner.

### AMPlified Search for Chrome™ (AMPS)
AMPS is a Chrome browser extension that examines your Google™ search results and uses Learning Registry metadata and paradata to identify Learning Resources with the resource's alignment to standards information and social activity data. 
Additional standards information is located via Jes&Co. Identified resources will have the additional data displayed inline, but beneath each search result.

> License: Apache 2

> Author: [Jim Klo](https://github.com/jimklo/) (SRI International) 

> Tech Info: Javascript

> * [Source Code](https://github.com/jimklo/AMPS-Chrome/)

### LearningRegistrar (Plugfest 2)
LearningRegistrar is a few-click solution to placing any internet accessible document into the Learning Registry. It uses Eduworks' 3rd party service, Metaglance, to extract and generate metadata about the document you are currently viewing, and provides a simple solution to placing information into the Learning Registry.

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


### Repofringe 2011 Hackday - Visual Browser
Built against a modified version of the node distribution, provides a very simple visual interface to search a
node for specific terms and identify resources that have been tagged with common keys.

> License: Apache 2

> Author: [Jim Klo](https://github.com/jimklo/) (SRI International) 

> Tech Info: Javascript and HTML5

> * [Source Code](https://github.com/jimklo/LearningRegistry/tree/RepoFringe)

### Learning Registry Browser
Adapted from Jim Klo's Visual Browser - allows users to perform a search using a key or identity. Results are displayed both as a list of documents and as a graph of related terms found in those documents. The graph can be used to explore further related terms, allowing the user to explore the semantic landscape of the Learning Registry. Document display summarizes Learning Registry entries for discovered documents, links to full Learning Registry documents, to described Learning Resources, and to related paradata.

The Browser is running here:
http://demolearningregistry.sri.com/browse/

> License: Apache 2

> Author: [John Brecht](https://github.com/jbrecht/) (SRI International) 

> Tech Info: Javascript and HTML5

> * [Source Code](https://github.com/jbrecht/lrbrowser)

### Learning Registry Drupal Module
This project is a module to plug into the content management capabilities of Drupal and publish/consume resources from the Learning Registry.

> License: GPL

> Tech Info: PHP and Drupal 6

> Authors: [Ali Lotia](https://github.com/lotia), [Kevin Coffman](http://drupal.org/user/1016508) and [Jason Hoekstra](http://drupal.org/user/589254)

> * [Source Code](http://drupal.org/sandbox/jasonh/1342822)



# External Utilities
The following projects are designed to work with the Learning Registry services and are not part of the node installation.

## Code Libraries
These are libraries created for specific programming languages or frameworks to make it easier to access Learning Registry node services.

### LRJavaLib
Java library for accessing core services for a node, including publishing and consuming data. Base classes are in place and functions are being expanded incrementally. Data consumption will be expanded to support a variety of data schema. 

> Language: Java

> License: Apache 2

> Author: [Navigation North](http://www.navigationnorth.com/)

> * [Source Code](https://github.com/navnorth/LRJavaLib)

### .Net LR Submit tool
A .Net library with classes and functions to build and publish Resource Data Description Documents. Includes an example of writing paradata to the LR test nodes. Uses credentials in a .config files to sign and upload documents. 

> Language: C# .Net

> License: Apache 2

> Author: [Rob Chadwick, ADL] robert.chadwick.ctr@adlnet.gov (http://www.adlnet.gov/)

> * [Source Code](https://github.com/rchadwic/.Net-Learning-Registry-Submit)

## Data Pumps
These are scripts, programs, and applications that extract data from one source and publish it onto a Learning Registry node.

### LRDataPump
Harvests an OAI-PMH NSDL_DC repository and publishes as signed LR resource data to a specific node. Utility is designed to work as a differential task. Subsequent execution will harvest from the configured repository since the last successful harvest. Tool is also resumable, if for some reason a failure occurs, the next run will pick up harvesting where it left off, and not republish.

> Language: Python

> License: Apache 2

> Author: [Jim Klo](https://github.com/jimklo/) (SRI International)

> * [Source Code](https://github.com/jimklo/LRDataPump)



## Resource Document Signing
These are solutions to help get your resource data signed with your own PGP key.

### LRSignature
Extendable Python library and command line tools that can be used to sign LR resource data documents.

> Language: Python

> License: Apache 2

> Author: [Jim Klo](https://github.com/jimklo/) (SRI International)

> * [Source Code](https://github.com/jimklo/LRSignature)



## Node Administration
Anything that may be useful in setting up, monitoring, or administering your own Learning Registry Node

### LRMonitor
A Python module that can query CouchDB status message and format into a suitable format to be digested by Cacti.

> Language: Python

> License: Apache 2

> Author: [Jim Klo](https://github.com/jimklo/) (SRI International)

> * [Source Code](https://github.com/jimklo/LRMonitor)

### Moodle4BLTI_LR
Publish/Browse/Use BasicLTI tools from Moodle. The idea is to publish tools in Learning Registry, using BasicLTI (http://www.imsglobal.org/lti/). Then in LR can share not only static content but tools. To launch remote tools the mechanism is BasicLTI.

> Language: PHP

> License: GPL2

> Author: [Antoni Bertran] (http://sourceforge.net/users/antonib) [Universitat Oberta de Catalunya](http://www.uoc.edu)

> * Project page: http://sourceforge.net/projects/learningapps

> * Wiki: https://sourceforge.net/apps/mediawiki/learningapps/index.php?title=Moodle4BLTI_LR_English#Learning_Registry_Integration

> * [Source Code](https://sourceforge.net/scm/?type=svn&group_id=388815) SVN

> * Demo Video http://vimeo.com/32982697