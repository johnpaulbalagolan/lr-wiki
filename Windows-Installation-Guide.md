Copyright 2011 SRI International

Licensed under the Apache License, Version 2.0 (the &quot;License&quot;); you may not use this file except in compliance with the License. You may obtain a copy of the License at

>     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an &quot;AS IS&quot; BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

# Introduction

There are two recommended approaches to get a new Learning Registry node running using the latest stable code: 1) via an Amazon Machine Instance (AMI) or 2) via installing the code.

Instructions for using an existing AMI are available from http://goo.gl/fhdg3.

The installation instructions below the steps to get a new Learning Registry node running using the latest stable code. These instructions are provided for Windows and have been tested with the Windows 7 64-bit environment. 

_NOTE: Some code changes had to be made for Windows' machines. Once these have been fully tested and published the doc will be updated to grab the changes to ensure a successful installation._

# Prerequisites 

_**A pre-existing C/C++ compiler must exist on your machine. We recommend Visual C++ 2008 Express since it is available for everyone: If you already have full versions of either Visual Studio 2008 or Visual Studio 2010 you can skip the installation step of Visual C++ 2008 Express.**_

#### 1. Install Git
* Install **Git** [here](http://code.google.com/p/msysgit/downloads/detail?name=Git-1.7.7.1-preview20111027.exe&amp;can=2&amp;q=)
* Click **Run** and follow setup instructions
     * Click **Next**
     * Click **Next**
     * If you would like to select a different folder for installation click **Browse...** else just click **Next**
     * Keep the default **selected components** and click **Next**
     * If you would like to select a different folder for the shortcuts click **Browse..** else click **Next**
     * Select **Use Git Bash Only** and click **Next**
     * Select **Checkout Windows-style, commit Unix-style line endings** and click **Next**
     * Click **Finish**

#### 2. CMake
* Go [here](http://www.cmake.org/cmake/resources/software.html) and download the **cmake-2.8.6-win32-x86.exe** file
* Click **Run** and follow setup instructions
     * Click **Next**
     * Click **I Agree**
     * Choose **Add CMake to the system PATH for all users** and click **Next**
     * If you would like to change the **Destination Folder** for installation click **Browse...** else just click Next
     * Type a new name for the **Start Menu folder** if you'd like, else just click **Install**
     * Click **Finish**
     * Click **I have read and accept the license terms** and click **Next**

#### 3. Visual C++ 2008 Express Edition (C/C++ Compiler)
* Go [here](http://www.microsoft.com/visualstudio/en-us/products/2008-editions/express) and click **Visual C++ Express Edition with SP1**
* Select your language and click **Free Download**
* Click **Run** and follow setup instructions
     * Click **Next**
     * Click **Install**
     
# Python
## Python 2.7.2 32-bit
1. Download the **Windows x86 MSI Installer(2.7.2)(sig)** [here](http://www.python.org/getit/releases/2.7.2/)
2. Click **Run** and follow setup instructions
     * Choose **Install for all users** and click **Next**
     * Choose your **Destination Directory** (default is C:\Python27) then click **Next**
     * Click **Next** when asked to **Customize Python 2.7.2**
     * Click **Finish**
3. Once installation is complete, add Python to your system path
     * Click **Start** -> Right click **Computer** -> click **Properties** -> click **Advanced system settings** -> click  **Environment Variables...**
     * Highlight the **Path** variable under **System variables** and click **Edit...**
     * Add **[Directory]\Python27;[Directory]\Python27\Scripts;** to the end of **Variable value** (ex: if Python was downloaded in your C:\ root, you would add **C:\Python27;C:\Python27\Scripts;**)

## Python Setuptools
1. Download the Windows executable, **setuptools-0.6c11.win32-py2.7.exe**, [here](http://pypi.python.org/pypi/setuptools#downloads)
2. Click **Run** and follow setup instructions
     * Click **Next** when prompted
     * Make sure **Python Version 2.7** is highlighted and click **Next**
     * Click **Next** again to being the install
     * Click **Finish** when done

## Pip
1. Open the Windows command prompt (**Start** -> search for **cmd**)
2. In the command prompt, enter the command `easy_install pip` and it will load pip on your machine, then you can proceed to install the other necessary modules:
3. virtualenv `pip install virtualenv`
     * Create a **virtual environment** to sandbox your development environment
     * Run the command `mkdir virtualenv` and move into that directory `cd virtualenv`
     * Run the command `virtualenv lr` (lr will be the name of your virtual environment) 
     * Navigate to the **Scripts** directory of lr `cd lr/scripts`
     * Run the command `activate`
     * **(lr)** should now appear at the beginning of your command line if successful
4. pylons `pip install pylons`
5. ijson `pip install ijson`
6. flup `pip install flup`
7. pyparsing `pip install pyparsing`
8. iso8604plus `pip install iso8601plus`
9. Go [here](http://pypi.python.org/pypi/lxml/2.3 ) and download, **lxml-2.3.win32-py2.7.exe**
10. Click **Run** and follow setup instructions
     * Click **Next** when prompted
     * Make sure **Python Version 2.7** is highlighted and click **Next**
     * Click **Next** again to begin the install
     * Click **Finish**

## YAJL
1. Visit [here](http://lloyd.github.com/yajl/) and download **yajl-1.0.12.zip**
     * Go into your **Downloads** folder and find the **lloyd-yajl-1.0.12.zip** file
     * Right click on the **lloyd-yajl-1.0.12.zip** file, and click **Extract All...**
     * Click **Browse...** and navigate to **[Directory]\Python27\Lib** then click **OK**
     * Click **Extract**
2. Open your Visual C++ (or Studio) Command Prompt (**Start** -> search for **Visual Command Prompt**)
3. Navigate to where you extracted the YAJL files - **[Directory]/Python27/Lib/lloyd-yajl-17b1790/src** - using the **cd** command
4. Make a build directory using the command `mkdir build`
5. Navigate into the build directory using the command `cd build`
6. Run the command `cmake -G"NMake Makefiles" -DCMAKE_BUILD_TYPE=Release ..`
     * If successful, the prompt should display **Build files have been written to : [Directory]/Python27/Lib/lloyd-yajl-17b1790/src/build**
     * If you receive an error please review the Troubleshooting [page](https://github.com/LearningRegistry/LearningRegistry/wiki/Troubleshooting)
7. Run the command `nmake` to build all of the YAJL files
     * If successful, you will not get any error messages
8. Open your **Windows Explorer** and navigate to **[Directory]\Python27\Lib\lloyd-yajl-17b1790\build\src\lib**
9. Copy the **yajl.dll** file and paste it into **C:\Windows\SysWOW64**-for 32 bits windows XP into **C:\Windows\system32**
     * To check if successful, open the Windows Command Prompt
     * Run the command `python`, then `import ijson`
     * If there are no errors YAJL has been successfully installed
     
## Py2exe
1. Go [here](http://sourceforge.net/projects/py2exe/files/py2exe/0.6.9/) and download the **py2exe-0.6.9.win32-py2.7.exe** Windows installer
2. Click **Run** and follow setup instructions
     * Click **Next** when prompted
     * Make sure **Python Version 2.7** is highlighted and click **Next**
     * Click **Next** again to begin the install
     * Click **Finish** when done

## Pywin32
1. Go [here](http://sourceforge.net/projects/pywin32/files/pywin32/Build216/) and download the **pywin32-216.win32-py2.7.exe** Windows installer
2. Click **Run** and follow setup instructions
     * Click **Next** when prompted
     * Make sure **Python Version 2.7** is highlighted and click **Next**
     * Click **Next** again to begin the install
     * Click **Finish** when done

# CouchDB
## CouchDB 1.1.1
1. Go [here](https://github.com/dch/couchdb/downloads) and download the **setup-couchdb-1.1.1_js185_otp_R14B03+fix-win32-crypto.exe** file
     * Click **Run** and follow setup instructions
     * Click **Next**
     * Accept the agreement and click **Next**
     * If you would like to select a different folder for installation click **Browse...** else just click **Next**
     * If you would like to create the program's shortcuts click **Browse..** else just click **Next**
     * Make sure **Install couchdb as a Windows service** and **Start the service after installation** boxes are checked and click **Next**
     * Click **Install**
2. Make sure CouchDB is running correctly by going [here](http://localhost:5984), you should see **{"couchdb":"Welcome","version":"1.1.1"}**

## CouchApp
1.  Enter the command `pip install couchapp`

# Checkout Learning Registry Source Code
1. Open the **Git Bash** (**Start** -> search for **Git Bash**)
2. Navigate to where you want your repository by using the `cd [directory_name]` command
3. To gather the LR code from github, run the command `git clone https://github.com/LearningRegistry/LearningRegistry` 
4. Once it is done cloning, run the command, `cd LearningRegistry` to move into the LearningRegistry directory
5. Run the command `git tag –l` to find the latest tag
6. Checkout the latest tag by running the command, `git checkout [latest tag version]` (0.23.5 as of Feb. 7th, 2012)  

## Nginx
1. Go [here](http://nginx.org/en/download.html) and download the **nginx/Windows-1.1.11** zip file
     * Go into your **Downloads** folder and find the **nginx-1.1.11.zip** file
     * Right click on the **nginx-1.1.11.zip** file, and click **Extract All...**
     * Click **Browse...** and navigate to **C:/** then click **OK**
     * Click **Extract**  
2. Stop Internet Information Services (IIS)
     * Click **Start** then search for **IIS**
     * Open the **IIS Manager** and click **Stop** on the right hand side under **Manage Server**
3. Copy Source Files into Nginx Configuration Directory
     * Browse to **[Directory]\LearningRegistry\etc\nginx**
     * Copy the folders **conf.d**, **learningregistry_cgi**, and **sites-available**
     * Paste them into **C:\nginx-1.1.11\conf**  
4. Include FastCGI_Params in Nginx Configuration File
     * Browse to **C:\nginx-1.1.11\conf** and open **nginx.conf**
     * Inside the **server** braces there is another set of braces for **location**, remove the lines **root    html;** and **index   index.html index.htm;**
     * Add the line **include   learningregistry_cgi/fastcgi_params;** and save the file
5. Start Nginx
     * Open the Windows command prompt and navigate to **C:\nginx-1.1.11**
     * Run the command `start nginx`

# Running the LR Node
## Push the CouchApps
1. Navigate to the **config** folder of your LR repository `cd [directory]/[LR Repository]/config`
2. Run the command `python setup_node.py`
3. When prompted, enter **http://localhost** as your endpoint URL
4. For the rest of the setup, just hit **enter** whenever prompted to input the default parameters
5. When finished you should receive a message displaying, **All CouchApps Pushed**

## Install the LR Node
1. Navigate back to the main LR directory
2. Navigate to the lr directory
3. Run the command `python setup.py install`
4. When finished you should receive a message displaying, **Finished processing dependencies for LR==0.1dev**

## Start Application Server 
1. While still in the LR directory, run the command `paster serve development.ini`