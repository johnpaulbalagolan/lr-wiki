Welcome to the Learning Registry wiki! The Learning Registry makes digital learning resources easier to **find**, easier to **access** and easier to **integrate** into learning environments _wherever_ they are stored -- around the country and the world. This will enable teachers, students, parents, schools, governments, corporations and non-profits to **build** and **access** better, more interconnected and **personalized learning solutions** needed for a 21st-century education. You can find more information on the Learning Registry project at the [Learning Registry Web Site](http://learningregistry.org).

## Getting Started

The [Learning Registry in 20 Minutes or Less](https://docs.google.com/document/d/12nvvm5ClvLxSWptlo52rTwIDvobiFylYhWLVPbVcesU/edit?hl=en_US) guide will get you rolling with creating, uploading, downloading, and verifying envelopes in and out of Learning Registry servers whether you're using Windows, Linux, or Mac OS X.

* Slice (tags) - http://lrtest01.learningregistry.org/slice?any_tags=science

* Slice (identity) - http://lrtest01.learningregistry.org/slice?identity=ADL

* Slice (from, [until]) - http://lrtest01.learningregistry.org/slice?any_tags=science&from=2011-05-11&until=2011-10-31

* Harvest - http://lrtest01.learningregistry.org/harvest/getrecord?request_ID=0e67e2195d9d45348c00a4b36ab1cfac&by_doc_ID=true

* Status - http://lrtest01.learningregistry.org/status

* Obtain - http://lrtest01.learningregistry.org/obtain

* Services - http://lrtest01.learningregistry.org/services

## Developer Basics

* The [Learning Registry Quick Reference Guide](https://docs.google.com/document/d/1Bq_69wnnQJ56O6jyLK2C_fcp-Ovb7MYxXUXD0Rl1Mag/edit?authkey=CK7k5r8F&hl=en_US&authkey=CK7k5r8F) provides a brief reference to the principal data structures and services with which typical developers using the Learning Registry will most frequently interact.

* The Learning Registry Project maintains a node at [lrtest01](http://lrtest01.learningregistry.org) for users trying to integrate with the LR service APIs. LR web services can be accessed by software clients written in any programming language and [lrtest01](http://lrtest01.learningregistry.org) can be used to publish and access resource data using the LR service APIs from the client.  

* For the latest status on what code test servers are running, please consult the [server status spreadsheet](https://docs.google.com/spreadsheet/ccc?key=0AtOSW7g7E8Y5dFRsSW5HRFlSalFpZjFvMmVKNGdpd2c&hl=en_US#gid=0).

* If you are publishing data, we recommend publishing documents in batches of 100 documents in each publish post.  Each batch of 100 documents should take less than 10 seconds to publish.

* Publishing guidance using OAI-PMH: http://goo.gl/yOihy

## Setting Up an LR Node

There are two recommended approaches to get a new Learning Registry node running using the latest stable code.  The current version of the code implements the [Learning Registry Technical Specification v0.23.0](https://docs.google.com/document/d/1fRbDpM0BKvNc4WzDzX0pNUpfPtFAsKpKGnOyRhRok-8/edit?hl=en_US).  The first approach is to setup an LR node using an Amazon Machine Instance (AMI).  The second approach is to install a new node LR node on a Windows, Linux, or Mac OS X machine following installation instructions.

* Instructions for using an existing AMI are available from http://goo.gl/fhdg3.  

* Instructions for setting up an LR Node on Ubuntu 10.04 onwards and MacOS 10.6.x (Snow Leopard) can be found at <https://github.com/LearningRegistry/LearningRegistry/blob/master/README.md>. The instructions are for manually setting up a node as well as for automatically installing all software necessary for node setup. The [Sprint3Release branch](https://github.com/LearningRegistry/LearningRegistry/tree/Sprint3Release) of the source tree is the most stable version and should be used if you are trying to setup a node for the first time.

## Getting Help

* Report a bug: https://github.com/LearningRegistry/LearningRegistry/issues

* General questions: info@learningregistry.org

* Learning Registry Developers List: http://groups.google.com/group/learningreg-dev?pli=1

* [Troubleshooting](https://github.com/LearningRegistry/LearningRegistry/wiki/Troubleshooting) guidance