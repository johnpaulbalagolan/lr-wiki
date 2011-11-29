Have you built a utility for Learning Registry? List it on this page.  Have you extended core Learning Registry? List it on this page.  Have you done something cool with Learning Registry? List it on this page.

We are using Apache 2: http://www.apache.org/licenses/LICENSE-2.0.html to license code, we prefer if community contributions used that too. We understand there may be situations where this might not be possible, and we will take that into account if your contribution needs to be merged into core code.

# Demonstrations
Here are some demonstration projects that either extend or augment Learning Registry in some manner.

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


### Learning Registry Drupal Module
This project is a module to plug into the content management capabilities of Drupal and publish/consume resources from the Learning Registry.

> License: GPL

> Tech Info: PHP and Drupal 6

> Authors: [Ali Lotia](https://github.com/lotia) and [Jason Hoekstra](https://github.com/jasonhoekstra)

> * [Source Code](https://github.com/openmichigan/lr_publish)



# External Utilities
The following projects are designed to work with the Learning Registry services and are not part of the node installation.

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

> Author: [Antoni Bertran] /http://sourceforge.net/users/antonib) [Universitat Oberta de Catalunya](http://www.uoc.edu)

> * Project page: http://sourceforge.net/projects/learningapps

> * Wiki: https://sourceforge.net/apps/mediawiki/learningapps/index.php?title=Moodle4BLTI_LR_English#Learning_Registry_Integration

> * [Source Code](https://sourceforge.net/scm/?type=svn&group_id=388815) SVN