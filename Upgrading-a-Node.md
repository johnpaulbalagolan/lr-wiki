To upgrade a node to the latest release, please follow the recommended steps below:
(For more detailed instructions to update to the 0.23.6 release please click [here] (https://github.com/LearningRegistry/LearningRegistry/wiki/Upgrading-to-0.23.6-from-previous-release).
There is also a bug fix for 0.23.6 that's been released in 0.23.7 [here](https://github.com/LearningRegistry/LearningRegistry/wiki/Release-Notes-0.23.7).)

## 1. Pull the most recent tag from git

>      cd <your path to git repository>/LearningRegistry
>      git checkout master
>      git pull 
>      git tag -l
>      git checkout [latest tag version]

## 2. Run the setup node python script

>      python setup_node.py -d

NOTE: Please keep remember your configuration settings as this process will overwrite them.  It is important to run the setup node script as a new version of the code may change configuration files. By default, your configuration file will be `/LearningRegistry/LR/development.ini`