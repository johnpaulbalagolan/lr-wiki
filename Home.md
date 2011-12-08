Welcome to the Learning Registry wiki! The Learning Registry makes digital learning resources easier to **find**, easier to **access** and easier to **integrate** into learning environments _wherever_ they are stored -- around the country and the world. This will enable teachers, students, parents, schools, governments, corporations and non-profits to **build** and **access** better, more interconnected and **personalized learning solutions** needed for a 21st-century education. You can find more information on the Learning Registry project at the [Learning Registry Web Site](http://learningregistry.org).

## Getting Started

The [Learning Registry in 20 Minutes or Less](https://docs.google.com/document/d/12nvvm5ClvLxSWptlo52rTwIDvobiFylYhWLVPbVcesU/edit?hl=en_US) guide will get you rolling with creating, uploading, downloading, and verifying envelopes in and out of Learning Registry servers whether you're using Windows, Linux, or Mac OS X.

* Slice (tags) - https://node01.public.learningregistry.net/slice?any_tags=science

* Slice (identity) - https://node01.public.learningregistry.net/slice?identity=ADL

* Slice (from, [until]) - https://node01.public.learningregistry.net/slice?any_tags=science&from=2011-05-11&until=2011-10-31

## Developer Basics

The [Learning Registry Quick Reference Guide](https://docs.google.com/document/d/1Bq_69wnnQJ56O6jyLK2C_fcp-Ovb7MYxXUXD0Rl1Mag/edit?authkey=CK7k5r8F&hl=en_US&authkey=CK7k5r8F) provides a brief reference to the principal data structures and services with which typical developers using the Learning Registry will most frequently interact.

* The Learning Registry Project maintains a node at [lrtest02](http://lrtest02.learningregistry.org) for users trying to integrate with the LR service APIs.

* For the latest status on what code and configuration servers are running, please consult the list of [currently running LR nodes](https://github.com/LearningRegistry/LearningRegistry/wiki/nodes).

* If you are publishing data, we recommend publishing documents in batches of 100 documents in each publish post.  Each batch of 100 documents should take less than 10 seconds to publish.

* [Publishing guidance using OAI-PMH](http://goo.gl/yOihy)

* Harvest (by ID) - https://node01.public.learningregistry.net/harvest/getrecord?request_ID=4ebf25ff043841f48f5c0d61ffdf5d81&by_doc_ID=true

* Harvest (metadata formats) - https://node01.public.learningregistry.net/harvest/listmetadataformats

* Harvest (harvest endpoint) - https://node01.public.learningregistry.net/harvest/identify

* Obtain - https://node01.public.learningregistry.net/obtain

* Services - https://node01.public.learningregistry.net/services

* Status - https://node01.public.learningregistry.net/status

* Description - https://node01.public.learningregistry.net/description


## Setting Up an LR Node

There are two recommended approaches to get a new Learning Registry node running using the latest stable code.  The current version of the code implements the [Learning Registry Technical Specification v0.23.0](https://docs.google.com/document/d/1fRbDpM0BKvNc4WzDzX0pNUpfPtFAsKpKGnOyRhRok-8/edit?hl=en_US).  The first approach is to setup an LR node using an Amazon Machine Instance (AMI).  The second approach is to install a new node LR node on a Windows, Linux, or Mac OS X machine following installation instructions.

* [AMI Installation](http://goo.gl/fhdg3) - Instructions for setting up a node using an existing Amazon Machine Instance.  

* [Linux Installation](https://github.com/LearningRegistry/LearningRegistry/wiki/Proposed-Readme) - Instructions for setting up a node on Ubuntu 10.04 LTS onwards.

* [Windows Installation](https://github.com/LearningRegistry/LearningRegistry/wiki/Windows-Installation-Guide) - Instructions for setting up a node on a Windows 7 64-bit environment.

* [OS X Installation](https://github.com/LearningRegistry/LearningRegistry/wiki/Proposed-OS-X-Installation-Instructions)

## Get Involved

Are you interested in making the Learning Registry a faster, better platform? Check out our [Contributing](Contributing) page for information about the easiest way to collaborate with the core development team.

Do you have some solution where you have either built utilities or extended the core code to do something interesting? Please share it here:

* [Community Projects](https://github.com/LearningRegistry/LearningRegistry/wiki/Community-Projects)

## Getting Help

* Report a bug: https://github.com/LearningRegistry/LearningRegistry/issues

* General questions: info@learningregistry.org

* Learning Registry Developers List: http://groups.google.com/group/learningreg-dev?pli=1

* [Troubleshooting](https://github.com/LearningRegistry/LearningRegistry/wiki/Troubleshooting) guidance


