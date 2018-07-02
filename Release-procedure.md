The general release process is:

1. Run smoke screens on alpha
1. Define the version number for the release based on the version of the spec the code best aligns with and the current iteration of code WRT that spec
1. Create a new tag for the release in github based on the assigned version number
1. Download the .zip and tar.gz tags and upload each as a new Latest Stable Release download with the release date in parentheses
1. Remove the previous Latest Stable Release download links
1. Release to production nodes
1. Release to sandbox node
1. Update the list of [known nodes](known-nodes) to reflect the release each node is running
1. Send email describing release to all LR Google groups
1. Update Linux, Windows, Mac, and AMI install guides to reference new tag
1. Update or create a new AMI to include the new LR code (For instructions on doing so, please refer to this [document](http://goo.gl/PM9cR). When creating or updating an AMI, please use the current tag as the AMI name.)
1. Update the list of [Current AMI Instances](Current-AMI-Instances)
