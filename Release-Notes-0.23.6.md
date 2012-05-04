# DRAFT Release Notes 0.23.6 - FOR REVIEW ONLY.

### Overview

The 0.23.6 release is a strongly recommended upgrade for ALL Learning Registry node deployments, as some internal changes that make distribution more compliant towards the LR Service specification cause distribute functionality to fail when interacting with nodes running versions prior to 0.23.6.

Below find the key features addressed in this release.


### Key Features

* Data Services _**NEW**_
  - The extract API is included and enabled in this distribution. The Extract API brings a "batteries included" interface for tailoring data extraction and query to suit more narrow and varied use case needs without high resource requirements.
  - Data Service views are **NOT** installed by default. Node administrators can install any or all of the 3 standards alignment focused data services using python CouchApp. This is done to prevent unneeded consumption of disk space for data services not utilized.
  - [Interactive documentation](http://learningregistry.github.com/LearningRegistry/data-services/index.html) explaining Data Services and how to roll your own for your use case.
* Resource Data Distribution refactoring _**CHANGED**_
  - Distribute has been significantly refactored to reduce the need for 2x storage for documents. New distribute uses 2 DB's, incoming and resource_data. New _tainted_ documents can be distributed to incoming, and node may impose an internal policy for _untainting_ documents before moving into resource_data.  All harvest services still operate against resource_data.
  - More compatible with Learning Registry 0.23 specification. Document Types of resource_data are distributed, not resource_data_distributable.
  - Upgrade will require some minor configuration changes to NGINX to change or expose incoming endpoint.
  - **IMPORTANT** Legacy nodes can distribute to a 0.23.6 by adjusting service documents to use the incoming endpoint. Legacy cannot be the destination for a 0.23.6 server. 
* Subscription for Distribute _**NEW**_
  - You may now visit http://[node address]/register, enter the URL of your node (use https if SSL required to access).
* Support for CouchDB 1.2.0 _**NEW**_
  - This is a highly recommended upgrade. Significantly improves the storage and resource utilization, as well paves path for  features planned for future releases.
* Many Bug fixes
  - See details on the [0.23.6 Milestone Closed Issues](https://github.com/LearningRegistry/LearningRegistry/issues?milestone=5&state=closed) 

### Minimum Requirements
* Linux/Windows OS
* NGINX w/ uwsgi support
* Python 2.7.3 (+setuptools; +virtualenv)
* CouchDB 1.1.1 (1.2.0 Recommended)

### Commits

* [3368700](https://github.com/LearningRegistry/LearningRegistry/commit/3368700b121161ed4bb6a7464564abcaa8828af9) add a feature to quiet logging during certain operations
* [a756613](https://github.com/LearningRegistry/LearningRegistry/commit/a7566137f64ce828242f82a200be41570f9b7e25) force incoming to rescan all docs on startup
* [5f13ad1](https://github.com/LearningRegistry/LearningRegistry/commit/5f13ad175076653e137caaa3677082b124de688f) updated to delete for spec validation errors or conflicts
* [d832b01](https://github.com/LearningRegistry/LearningRegistry/commit/d832b01b00064b73b9c427c3089d5ad0196b2b12) fixed type of doc -> newDoc
* [a5acb7e](https://github.com/LearningRegistry/LearningRegistry/commit/a5acb7ec41f63e68615225d0f7d68b59350ad52c) fixed type of doc -> newDoc
* [01c408a](https://github.com/LearningRegistry/LearningRegistry/commit/01c408a24a5749eb383030a25704128be1b3bcf1) updated to handle -distributable docs and delete properly
* [d10bf1f](https://github.com/LearningRegistry/LearningRegistry/commit/d10bf1f32cd5af45ffa237d1b948d7b95ed7b589) Adding Compaction Handler since @wegrata probably missed it in a checkin
* [0fe98fc](https://github.com/LearningRegistry/LearningRegistry/commit/0fe98fcc5553da8466306c4497f1c245677bf1cb) updated to run compation in seperate handler, with seperate threshold
* [ba2fecf](https://github.com/LearningRegistry/LearningRegistry/commit/ba2fecf58df8d6dfb4b41fdb194e482af4576e08) Removed filter for -distributable
* [af5d599](https://github.com/LearningRegistry/LearningRegistry/commit/af5d599cfdadfa99d4c788773eb5f00b71956f9a) catch an error on open a url upon startup.
* [861dea9](https://github.com/LearningRegistry/LearningRegistry/commit/861dea959e73d4f7a78e8207a98d778d71d53c57) assumed default couch.url in config
* [76743b6](https://github.com/LearningRegistry/LearningRegistry/commit/76743b648510940fb1803389541f18345cb8d2db) wrong node specified in config.
* [d15f4a0](https://github.com/LearningRegistry/LearningRegistry/commit/d15f4a05469dd31aa6f4c0872b1bfcdaa0b3b11f) added except clause for conflicts to keep from getting logged twice
* [a4b60b2](https://github.com/LearningRegistry/LearningRegistry/commit/a4b60b2f76e43acfd39eb31d4870fff3003336f1) Added reference to SpecValidationError and fixed the expected doc_type
* [829c636](https://github.com/LearningRegistry/LearningRegistry/commit/829c636a6018411fcf2ac82f67f7e300232867c7) fix for reading possibly the wrong config file
* [2acca36](https://github.com/LearningRegistry/LearningRegistry/commit/2acca3609bc6081ef0c4f28a3daff0d25a6e1421) Validates document and cleans up from incomming
* [0720bc2](https://github.com/LearningRegistry/LearningRegistry/commit/0720bc22db6587316e2e0ea7e05783c868f82b54) exclude the couchapp command extension from being considered a test by nose
* [7d317bc](https://github.com/LearningRegistry/LearningRegistry/commit/7d317bc6edceaa978106a5569d43b145231ef3f3) updated to install data_service view for testing
* [8b20a4f](https://github.com/LearningRegistry/LearningRegistry/commit/8b20a4fce28e8384294bf8f7a80cfa9a4486740c) make the test wait longer for updater to catch up.
* [0cf759c](https://github.com/LearningRegistry/LearningRegistry/commit/0cf759c2481b18011e7cddbe3e0b31791c7afc5a) make the test wait longer for updater to catch up.
* [ace426f](https://github.com/LearningRegistry/LearningRegistry/commit/ace426fac97474e7316dbb5025fdd5d73132c7b6) couch not defined early enough
* [b97e660](https://github.com/LearningRegistry/LearningRegistry/commit/b97e6608cb1049c51cb1fba2e1668e303b6901b2) foobar'd syntax error.
* [9fcf328](https://github.com/LearningRegistry/LearningRegistry/commit/9fcf328cbe8a3b478ba4be63dff2f90fc9f6da8c) foobar'd syntax error.
* [ca7e54b](https://github.com/LearningRegistry/LearningRegistry/commit/ca7e54bbaf8a76a18e740a7c7a3d3e27bbc3b8f8) try making test wait until indexer is idle before trying to start
* [409416d](https://github.com/LearningRegistry/LearningRegistry/commit/409416d390b360adaf0ed9b4c63a8db0606a83ea) updated to use deepcopy to store previous config for service
* [5f363b1](https://github.com/LearningRegistry/LearningRegistry/commit/5f363b178b1f07245adb93c2cb867f3d58505138) updated test_obtain_resource_locator so leftover values in DB don't cause an error, as it's pulling all the content from the DB anyway
* [ddadea7](https://github.com/LearningRegistry/LearningRegistry/commit/ddadea76704f33f302ea7cf7454b021ad6a0b93b) updated to work with current config rather than hard coded url
* [5323e1d](https://github.com/LearningRegistry/LearningRegistry/commit/5323e1d271e4bde5521c08e1d93f609646ff5b42) updated tests and decorators so they consistently work together
* [b72559e](https://github.com/LearningRegistry/LearningRegistry/commit/b72559e24c1a0b1a6824a6e8849652ed35abd257) Fixed tests expecting flow control to enable it, also added a decorator to make this easier for future tests
* [41dfbd6](https://github.com/LearningRegistry/LearningRegistry/commit/41dfbd6027ca04f04c4ad6f5375f1129aaf135b6) attempt to fix slice test
* [f4be1bf](https://github.com/LearningRegistry/LearningRegistry/commit/f4be1bf0f7818947c552f3160157fc3b6fbc719e) change destination url to something 'almost' guaranteed.
* [8956db7](https://github.com/LearningRegistry/LearningRegistry/commit/8956db72bd5abd22846c206a9050002272d7d4fd) fixed bug #203
* [e89d98f](https://github.com/LearningRegistry/LearningRegistry/commit/e89d98fd9bb210ae659a48ba57e798af646e0d84) Fixed bug #203
* [4a4191a](https://github.com/LearningRegistry/LearningRegistry/commit/4a4191a6cc8c8ffa99a01c0607b2842467a643e8) added constant in place of magic number
* [1e0fb77](https://github.com/LearningRegistry/LearningRegistry/commit/1e0fb77959ca243f3dcd91780b743999384c0768) fixed array element type checking
* [286434d](https://github.com/LearningRegistry/LearningRegistry/commit/286434d99cfb3bdd61e522558da6aaf9d82de82c) add forgotten template
* [bc9fd8a](https://github.com/LearningRegistry/LearningRegistry/commit/bc9fd8a9ec780121cc40c921d6576cad078bc6c1) added test and code to handle no key being passed in
* [d2784a4](https://github.com/LearningRegistry/LearningRegistry/commit/d2784a496e332694fc37a6535edb4fca904015c1) fixed missing keys bug
* [1e46363](https://github.com/LearningRegistry/LearningRegistry/commit/1e46363d97e21e5c433bbb6ea57604b306dcb9b1) Fixed bug and added tests
* [859c06f](https://github.com/LearningRegistry/LearningRegistry/commit/859c06fe88258517f4722722269326426647a293) add incoming to node config files automatically
* [8edae39](https://github.com/LearningRegistry/LearningRegistry/commit/8edae39a016efb15a26d1b832a37f692e101d745) added incoming values
* [8a9fb84](https://github.com/LearningRegistry/LearningRegistry/commit/8a9fb8489b3a2e2cad084871d6c05007a447c752) added incoming values
* [bb70b46](https://github.com/LearningRegistry/LearningRegistry/commit/bb70b46f95587f9835c1d1eb97f57c40c883d077) reverted back to creating monitors separately
* [c1d0b8e](https://github.com/LearningRegistry/LearningRegistry/commit/c1d0b8ee4fa86042c8a0d8323e2941e2713c4971) forgot to include distribute controller with previous commit
* [6fddc33](https://github.com/LearningRegistry/LearningRegistry/commit/6fddc33dee87f555824bd7c75e6f36d78e7cb801) copies instead of replicate
* [fedfafe](https://github.com/LearningRegistry/LearningRegistry/commit/fedfafe3b4255c6f9e331e1ab72a1815c59a6531) changes to fix partial discriminators
* [97777af](https://github.com/LearningRegistry/LearningRegistry/commit/97777aff0546a081bda077b18e215b26b3deaff8) fix the ddoc name to match folder name
* [67e3e2b](https://github.com/LearningRegistry/LearningRegistry/commit/67e3e2b90f6124b7f254cf96a3511413de640bcc) add new data service that combines the metadata and paradata
* [8912dd8](https://github.com/LearningRegistry/LearningRegistry/commit/8912dd8382ea4fc0c875b2fb4435df14f9bf0826) switched handlers around
* [ab346e9](https://github.com/LearningRegistry/LearningRegistry/commit/ab346e9eb992cdf1406aaaf2bbc964fbca6b79d2) Found a way to get complex discriminators to to work with "starts with"
* [e920c0a](https://github.com/LearningRegistry/LearningRegistry/commit/e920c0a62fd2f8554cbdcab5c68e376b01c856da) Fix issue where when no term is being specified, one was being generated plus adding a generated tstamp, causing over filtering to occur
* [681ea60](https://github.com/LearningRegistry/LearningRegistry/commit/681ea60b83e6d1e3641682c4827bb79e58eaf52e) fix an issue where we have views with timestamps, but no way to display.  Also fix grouping which was grouping more than it should
* [04b538e](https://github.com/LearningRegistry/LearningRegistry/commit/04b538e47b5d74cbd453234bf15d8eee26c2e736) okay made the parameters work with empty result and with starts-with and complex keys for discriminator
* [e36c8c1](https://github.com/LearningRegistry/LearningRegistry/commit/e36c8c16ee445b7ce338c559418292bf0d80978c) fixed unicode encoding
* [ef1916f](https://github.com/LearningRegistry/LearningRegistry/commit/ef1916f2c1576f87a5e632b1a491df3883db6dd5) creates incoming db now
* [15f76ce](https://github.com/LearningRegistry/LearningRegistry/commit/15f76ce8d113d2d158c9410b3f7871ea875b1afb) creates DB in run if not already created
* [ecfdb8f](https://github.com/LearningRegistry/LearningRegistry/commit/ecfdb8f39aaac9ec063c8547eaa0819f0271ac5a) refactored couchMonitor process
* [a7285a7](https://github.com/LearningRegistry/LearningRegistry/commit/a7285a76a6d0cbc2fdadd9e76ebba758d0ec88d7) added try catch for dev.ini value
* [5bca546](https://github.com/LearningRegistry/LearningRegistry/commit/5bca546baa82f926d37dafc728f13631144b7b11) added try statement for obtaining config file value
* [558902d](https://github.com/LearningRegistry/LearningRegistry/commit/558902d84ca832d6eebf444ad1bfaf2435214e7d) added try statement for obtaining value out of config file
* [aa444de](https://github.com/LearningRegistry/LearningRegistry/commit/aa444deafb216313d83845bb782f7b9fb6820f62) incoming db handler added
* [05d08b1](https://github.com/LearningRegistry/LearningRegistry/commit/05d08b1a75bf885d2a49680d7373e78455fd19c9) changes incorporate incoming DB
* [839afbd](https://github.com/LearningRegistry/LearningRegistry/commit/839afbdf94dafdb5ffd695ece70c7bb57da23a92) added view compaction
* [fd43b84](https://github.com/LearningRegistry/LearningRegistry/commit/fd43b841df601f479bac7cd5697b48088c0017a0) updated tests and error responses
* [cb52a4d](https://github.com/LearningRegistry/LearningRegistry/commit/cb52a4dddb62a662f171df72fc710dd84b147453) added basic unit tests
* [c5a7b27](https://github.com/LearningRegistry/LearningRegistry/commit/c5a7b2774d7b3f241f849952f10081da375e78e5) added form to register node for replication
* [31cee58](https://github.com/LearningRegistry/LearningRegistry/commit/31cee58d7d973844f4106a2bd0fdd430a3177abd) Added tests
* [ad9168b](https://github.com/LearningRegistry/LearningRegistry/commit/ad9168b82a861af158bff110ab2c3898c53b0ca9) added check to verify the design doc is part of data services
* [908e844](https://github.com/LearningRegistry/LearningRegistry/commit/908e844097b2f1c8d258efdc906e562c8f48a9f4) fixed some bugs and added some tests
* [4597e1e](https://github.com/LearningRegistry/LearningRegistry/commit/4597e1ea7e98b2686ca07561e84e31e9f7fbb8ae) fixed typo in function call
* [12feb03](https://github.com/LearningRegistry/LearningRegistry/commit/12feb039efb8c4325448b9dc1e47d39c2b31d6fe) fixed so documents don't get emitted more than once
* [f340678](https://github.com/LearningRegistry/LearningRegistry/commit/f34067802463fd9007e9606964cc4a4445bc8d37) updated to use views, assumes the default view is to-json
* [984783d](https://github.com/LearningRegistry/LearningRegistry/commit/984783d6ef9c3e30b810bb5972887f05de6a3a1a) updating the dct_conformsTo and adding a list function
* [3a533b4](https://github.com/LearningRegistry/LearningRegistry/commit/3a533b4e55b25abf6420717b48d6204407a963ae) mixup dct-conformsTo tests
* [e8bf276](https://github.com/LearningRegistry/LearningRegistry/commit/e8bf2768697429ad1518e4258715f6c9613c4ae2) move functions around to make more modular
* [c9bc092](https://github.com/LearningRegistry/LearningRegistry/commit/c9bc0920fa45fb26d6aa582db2f1e8427729dae7) deprecations of some old functions no longer needed.
* [7966e30](https://github.com/LearningRegistry/LearningRegistry/commit/7966e30b723080af35cbf54c35bd0d4207a710d9) Add support for getting Filter function to evaluate
* [7f6b800](https://github.com/LearningRegistry/LearningRegistry/commit/7f6b800f2bdc1fc85feaf0441e71e1bdcc0a0576) Make loading list function more streamlined
* [ef27be8](https://github.com/LearningRegistry/LearningRegistry/commit/ef27be83e986129b9200dcc3d5263891890bcc50) Cleanup and test framework bug fixes
* [cd89f9c](https://github.com/LearningRegistry/LearningRegistry/commit/cd89f9cf88a28d4376b4d0b0afd602e05f7ce66f) Got unit testing working again
* [06627d8](https://github.com/LearningRegistry/LearningRegistry/commit/06627d8dba3231bb0d12e09c0ac1690637d0d722) remove log statement
* [30a0543](https://github.com/LearningRegistry/LearningRegistry/commit/30a05432b00f6de1aefe5d5a62bdc402d45d3820) removing reduce functions and making list function do something useful
* [36a1497](https://github.com/LearningRegistry/LearningRegistry/commit/36a14976dcbbe0f4eb2074145bd64b0eac04c2c6) adding basic to-json list function
* [3c49633](https://github.com/LearningRegistry/LearningRegistry/commit/3c49633fd8db6f986a70294d4a36423ec1a0c1d5) fixed spelling
* [c4f7354](https://github.com/LearningRegistry/LearningRegistry/commit/c4f73542787061849753c89d887ed09f72b049ab) simple test list function
* [daa4290](https://github.com/LearningRegistry/LearningRegistry/commit/daa4290ee8edd303f98996b5664336c924aa13bd) fix typo
* [216ca6c](https://github.com/LearningRegistry/LearningRegistry/commit/216ca6cd0b56a6bd12ba7a641702d711af843a83) Cleaned up logging and added noise level to logging
* [f9425c7](https://github.com/LearningRegistry/LearningRegistry/commit/f9425c754eb17cc637b2ea9c23fc29f50688b886) Updated core test suite, and added tests for paradata
* [e51b5a8](https://github.com/LearningRegistry/LearningRegistry/commit/e51b5a8c4d441ae3e4e0f972a96f8a21c3ddd62e) updated python layer
* [b76a27e](https://github.com/LearningRegistry/LearningRegistry/commit/b76a27e5ef9ec73a3f797923d56d80b5909604a4) Updated to determine param order
* [a2720f9](https://github.com/LearningRegistry/LearningRegistry/commit/a2720f99fc0a9f4f861b96fca4492bb8b313412c) add tests to .couchappignore
* [67a1dad](https://github.com/LearningRegistry/LearningRegistry/commit/67a1dad2d32632517a12a7ad4e8c3f6d75165f11) added some unit testing and working on extracting paradata
* [27a6f44](https://github.com/LearningRegistry/LearningRegistry/commit/27a6f443b9891c415388edabb3891de019bc34ad) fixed self.couchapps
* [8808861](https://github.com/LearningRegistry/LearningRegistry/commit/8808861caf1d2f4b3ca130d80d255aeda2d695e6) Updated data services prototype
* [e8ae06e](https://github.com/LearningRegistry/LearningRegistry/commit/e8ae06e606a270661edc1dfad8949fe5013a1236) Update network diagram
* [52a4ae5](https://github.com/LearningRegistry/LearningRegistry/commit/52a4ae5718c30fc2c2c0f8bf3c03f4be407db94d) Allow distribution gateway to common node on the same network
* [9dcefee](https://github.com/LearningRegistry/LearningRegistry/commit/9dcefee798daaa729d9a3122bdbd4c1d0f555ee6) renamed to standards-alignment-dct-conformsTo
* [d0fa988](https://github.com/LearningRegistry/LearningRegistry/commit/d0fa988cfb641894810f48b851ac1df950a31c80) fixed routing
* [f1ebc4c](https://github.com/LearningRegistry/LearningRegistry/commit/f1ebc4cbf14846da3ed0a9f5e2ece5817ee1372e) Adding skeleton for python layer of data services
* [f6800a8](https://github.com/LearningRegistry/LearningRegistry/commit/f6800a83ec10f85ab970cdc922240056e711707c) ont the fly
* [119c20f](https://github.com/LearningRegistry/LearningRegistry/commit/119c20fab0f90d1cfc6deb0e2a9e7f3de6ad427b) output mockup
* [f1564f2](https://github.com/LearningRegistry/LearningRegistry/commit/f1564f28f5d2322b0ccf6bb5f0d40da7f698dc5e) Revert Array Element Type Restriction
* [8bc1b6b](https://github.com/LearningRegistry/LearningRegistry/commit/8bc1b6b45d522436d17eeb7ee64cffeaf4b307b3) Adding some more documentation to README.
* [c7687dd](https://github.com/LearningRegistry/LearningRegistry/commit/c7687dd59ccad93048e83fc08eb3d2bb9213ed01) Cleanup and verify examples
* [e59619e](https://github.com/LearningRegistry/LearningRegistry/commit/e59619e2dba93df0a5723c44f1ca85094e6a9f7a) fixed bad readme
* [9c645c0](https://github.com/LearningRegistry/LearningRegistry/commit/9c645c044a03e838513090eb53f64990e06f79b3) Checkpoint
* [6a54788](https://github.com/LearningRegistry/LearningRegistry/commit/6a547882470799dd4c606a8be71883838745376e) modified to use a long for the datetime, the long represents seconds since midning jan 1 1970
* [975295a](https://github.com/LearningRegistry/LearningRegistry/commit/975295a5bb32cf878fb44953b5cf1e68af66fd24) changed the work Key to Discriminator
* [a8842e8](https://github.com/LearningRegistry/LearningRegistry/commit/a8842e89ec4725cdfbdefec312dbe0bd94257e1d) Initial working revision
* [0c70f3f](https://github.com/LearningRegistry/LearningRegistry/commit/0c70f3ff6b89995e0f521b7f369b0e660048ba05) removed unnecessary constant in model_parser
* [d668cc3](https://github.com/LearningRegistry/LearningRegistry/commit/d668cc37b56d9b75a7e3de3e0627c22dbec2169f) added more descriptive error codes/conditions on publish
* [d0940dd](https://github.com/LearningRegistry/LearningRegistry/commit/d0940ddb23b22a6c0dace83954013c9d19af431a) cleaned up comment
* [4b0d2ea](https://github.com/LearningRegistry/LearningRegistry/commit/4b0d2eab4b5a866065bb72d585a4814d6f809e80) check for string values inside arrays when parsing model
* [6005cda](https://github.com/LearningRegistry/LearningRegistry/commit/6005cda39d904377752e3be4e05611310a1c9ad3) handled missing/invalid doc version with better error msg
* [749b9a9](https://github.com/LearningRegistry/LearningRegistry/commit/749b9a9e2e4eb2991b07e64cf889d8ee1e41ab23) Fix typo
* [5e11773](https://github.com/LearningRegistry/LearningRegistry/commit/5e1177379e44f2c4a13a911ad811929c3c8737c9) Push couchapps for active services only
* [09f1756](https://github.com/LearningRegistry/LearningRegistry/commit/09f175676b43275a3de23da3dc4d40f0c9e4bd95) Fixed bug #189
* [d611e9d](https://github.com/LearningRegistry/LearningRegistry/commit/d611e9ddaef29f440a35ca58dd188611d26412b5) Remove unsed code
* [ff795a8](https://github.com/LearningRegistry/LearningRegistry/commit/ff795a8bf46f153fe3ca9e47652536a21c10cf36) Minor clean up
* [cafec37](https://github.com/LearningRegistry/LearningRegistry/commit/cafec37c468d1ced4a48858982b319c2b6c5fdf8) Refactor Node Start/Stop
* [733b722](https://github.com/LearningRegistry/LearningRegistry/commit/733b722d9fe71a90bb15243d9af56aa28d1aa1c2) Update to run on Windows
* [e629957](https://github.com/LearningRegistry/LearningRegistry/commit/e6299579f226850347e977c2d526eae57267c652) Use BaseMonintorChange Use BaseChangeMonitor class the is inherits from a thread when run on windows,but from process otherwise.
* [d94ad54](https://github.com/LearningRegistry/LearningRegistry/commit/d94ad54a03d6b80da119249a2ef436ec13f8bf9e) Runs on Windows
* [07003a6](https://github.com/LearningRegistry/LearningRegistry/commit/07003a6a7ab7303af810bc76e58cdc0e5b43e83d) Update for PT story 23705115, add param to slice that says if the view is updated
* [205a4e6](https://github.com/LearningRegistry/LearningRegistry/commit/205a4e6d5a012c8f980f7a9fbca4376cddaa2f69) Fixed to work with newest description doc and with the old incorrect format