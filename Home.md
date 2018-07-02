Welcome to the Learning Registry wiki! Here you can find links to documentation intended to help developers working with the Learning Registry.  You can find more information on the Learning Registry project at the [Learning Registry Web Site](http://learningregistry.org).

* [Glossary](Glossary)

* [Common Data Schema Formats in Learning Registry](Common-Data-Schema-Formats-in-Learning-Registry) - Examples of common data schema formats used in Learning Registry. Note: LR is data schema agnostic.

* [Known Nodes](Known-Nodes) - A list of known LR nodes.

## Developer Resources

* [Guide for Consuming Learning Registry Records](Consuming-Learning-Registry-Records) - How to harvest and parse Learning Registry records with code examples.

* [Slice API](http://docs.learningregistry.org/en/latest/slicing/index.html#api) - The Slice API enables users to retrieve a subset of records.

* [Examples](Examples) - A page for sharing examples (metadata, paradata, queries).

* [Learning Registry in 20 Minutes or Less](http://docs.learningregistry.org/en/latest/start/20min.html) - A full walk through of creating, uploading, downloading, verifying, updating, and replacing envelopes.

* [Known Public Keys](https://docs.google.com/spreadsheet/ccc?key=0AvuZnuv2HuPWdEhmNTREcGhRc0NaRUpybnlaN2M5cWc#gid=0) - A list of known Public Keys of publishers in the LR.

## Publishing Resources

* **Publishing using OAuth and Node Signing** - Code samples showing how to publish to a node with Node Signing capabilities enabled.
  * [in Python](https://gist.github.com/3874176)
  * [in Ruby](https://gist.github.com/4708906)

* [Sandbox](http://sandbox.learningregistry.org) - Test applications developed with the Learning Registry API in a simulated environment.

* [Publishing guidance using OAI-PMH](http://goo.gl/yOihy) - A short Google Doc with code examples and links to working code projects to pull data from OAI-PMH repositories and push the data into the Learning Registry.

> If you are publishing data, we recommend publishing documents in batches of 100 documents in each publish post.  Each batch of 100 documents should take less than 10 seconds to publish.

## Installing and Setting Up an LR Node

The code hosted here on GitHub is used to run a Learning Registry node implementing the [Learning Registry Technical Specification v0.50.1] (http://docs.learningregistry.org/en/latest/spec/Technical_Spec/index.html).  Listed below are resources to help install and setup a Learning Registry node on different operating systems.

* [Linux Installation](http://docs.learningregistry.org/en/latest/install/ubuntu.html) - Instructions for setting up a node on Ubuntu 12.04 LTS.

* [AMI Installation](https://docs.google.com/a/adlnet.gov/document/d/1XxEyv1y6Nv2ELTPAoS7l3UHwjuwg7Q981xGbQ-5v6yQ/edit?hl=en_US) - Instructions for setting up a node using an existing Amazon Machine Instance.

* [List of AMIs](Current-AMI-Instances) - List of currently available LR Amazon Machine Instances (AMIs).

* [Windows Installation](Windows-Installation-Guide) - Instructions for setting up a node on a Windows 7 64-bit environment.

* [OS X Installation](Proposed-OS-X-Installation-Instructions) - Instructions for setting up a node on Mac OS X.

* [PlugFest2 Virtual Machine](PlugFest2-Virtual-Machine) - Jim distributed LR Virtual Machines at the PlugFest2 event loaded with an LR node instance and various tools.

* [Node Setup FAQ](Node-Setup-FAQ) - Frequently Asked Questions when setting up or running a node.

## Node Customization and Maintenance

* [Data Services](http://learningregistry.github.com/LearningRegistry/data-services/) - A design pattern to help you quickly develop a solution to extract relevant data from your Learning Registry Node.

* [Upgrading a Node](Upgrading-a-Node) - Instructions for upgrading a node to the latest release.

## Get Involved

Are you interested in making the Learning Registry a faster, better platform?

* [Community Projects](Community-Projects) - Please share here any utilities, demonstrations, or extensions to the core code.

* [Contributing](Contributing-to-the-Learning-Registry) - Information about the easiest way to collaborate with the core development team.

* [Releases](Releases) - Information on software releases.

* [Release procedure](Release-procedure) - Describes general procedure for a new release.

## Getting Help

* Report a bug: https://github.com/LearningRegistry/LearningRegistry/issues

* General questions: info@learningregistry.org

* Learning Registry Developers List: http://groups.google.com/group/learningreg-dev?pli=1

* [Troubleshooting](Troubleshooting) guidance
