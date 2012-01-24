To upgrade a node to the latest release, please follow the recommended steps below:

## 1. Pull the most recent tag from git

>      cd <your path to git repository>/LearningRegistry
>      git checkout origin master
>      git pull 
>      git tag -l
>      git checkout [latest tag version]

## 2. Run the setup node python script

>      python setup_node.py -d

NOTE: Please keep remember your configuration settings as this process will overwrite them.  It is important to run the setup node script as a new version of the code may change configuration files.