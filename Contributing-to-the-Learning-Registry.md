There are two ways you can contribute to the Learning Registry:

* by fixing/augmenting/improving the LR core code itself 
* modules and extensions for existing systems integration or features not defined by the Technical Specification

We will provide an overview of the former methods, as well as guide you on how to best sync with our current workflow. If you have a module/extension for the LR, or for integration with another software platform, please check out our [Community Projects Page](Community-Projects) for more information.

## LR Core

The LR core codebase on Github is not intended for changes to be pushed to directly. We are currently using the "fork + pull" model for contributing code. If you are not familiar with this way of contribution, we suggest you read this overview before moving forward with serious LR development: http://help.github.com/send-pull-requests/.

### Suggested Workflow:
1. Fork the LearningRegistry/LearningRegistry repository. Make sure that you don't unwatch the original.
2. Clone your fork locally and (optional) add a remote to keep track of changes from the original repo. 
3. For each feature that you are working on, create a branch and do the work in that branch.
4. When you are finished with a feature, issue a pull request from your working branch to the original LearningRegistry repository. The core team will perform a code review and, based on feedback, ignore the request or merge it into the current master branch.
5. If accepted into original master branch, merge your working branch into your own master.

### Releases and Tagging Policy
Official releases will be tagged using the following format `<version#>.<major#>.<minor#>.zip`. These correspond to releases that have been deployed to official Learning Registry production nodes and are considered to be stable. You may access these tags from the 'Code' -> 'Tags' page.