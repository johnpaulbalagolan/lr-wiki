The general release process is:

1. Run smoke screens on alpha
1. Define the version number for the release based on the version of the spec the code best aligns with and the current iteration of code WRT that spec
1. Create a new tag for the release in github based on the assigned version number
1. Release to production nodes
1. Release to sandbox node
1. Send email describing release to all LR Google groups
1. Update Linux, Windows, Mac, and AMI install guides to reference new tag
1. Update or create a new AMI to include the new LR code (For instructions on doing so, please refer to this [document](http://goo.gl/PM9cR). When creating or updating an AMI, please be sure to include the date at the beginning of the name. For example, if you were creating a new AMI on January 23rd 2012 with the production sprint 3 code, you would name it 2012-01-23_Production Sprint 3)