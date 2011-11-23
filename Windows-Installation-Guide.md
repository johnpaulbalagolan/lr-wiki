Copyright 2011 SRI International

Licensed under the Apache License, Version 2.0 (the &quot;License&quot;); you may not use this file except in compliance with the License. You may obtain a copy of the License at

&gt;     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an &quot;AS IS&quot; BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

_Guide created for **Windows 7 64-bit** environment; different tools may be required for different Windows environments._

#Prerequisites 

#### 1. Install Git
* Install **Git** [here](http://code.google.com/p/msysgit/downloads/detail?name=Git-1.7.7.1-preview20111027.exe&amp;can=2&amp;q=)
* Click **Run** and follow setup instructions
     * Click **Next**
     * Click **Next**
     * Choose the path where you want to install it by clicking **Browse...**
     * Click **Next**
     * Keep the default **selected components** and click **Next**
     * If you would like to select a different folder for the shortcuts click **Browse..**
     * Click **Next**
     * Select **Use Git Bash Only** and click **Next**
     * Select **Checkout Windows-style, commit Unix-style line endings** and click **Next**
     * Click **Finish**

#### 2. CMake
* Go [here](http://www.cmake.org/cmake/resources/software.html) and download the **cmake-2.8.6-win32-x86.exe** file
* Click **Run** and follow setup instructions
     * Click **Next**
     * Click **I Agree**
     * Choose **Add CMake to the system PATH for all users** and click **Next**
     * Click **Browse...** if you would like to change the **Destination Folder**, else just click **Next**
     * Type a new name for the **Start Menu folder** if you'd like, else just click **Install**
     

#### 3. Configure Internet Information Services (IIS)
* Enable IIS and the correct IIS tools
     * Click **Start** -&gt; **Control Panel** -&gt; **Programs** -&gt; **Turn Windows features on or off**
     * Check the box next to **Internet Information Services**
     * Expand **Internet Information Services** and check the box next to **Web Management Tools** if it not already filled in
     * Also be sure the box next to **World Wide Web Services** is checked
     * Expand **Application Development Features** inside of **World Wide Web Services** and check the boxes next to **CGI** and **ISAPI Extensions**
     * Click **OK** to save your changes

#### 4. Enable FastCGI module for IIS
**NOTE: We are encountering a PicklingError when starting the application and are working on the problem now. Whenever the error has been fixed the appropriate steps for enabling FastCGI will be added.**
     
# Python
## Python 2.7.2 32-bit
1. Install the **Windows x86 MSI Installer(2.7.2)(sig)** [here](http://www.python.org/getit/releases/2.7.2/)
2. Click **Run** and follow setup instructions
     * Choose **Install for all users**
     * Choose your **Destination Directory** (default is C:\Python27)
     * Click **Next** when asked to **Customize Python 2.7.2**
3. Once installation is complete, add Python to your system path
     * Click **Start** -> Right click **Computer** -> click **Properties** -> click **Advanced system settings** -> click  **Environment Variables**
     * Highlight the **Path** variable under **System variables** and click **Edit...**
     * Add **[Directory]\Python27;[Directory]\Python27\Scripts;** to the end of **Variable value** (ex: if Python was downloaded in your C:\ root, you would add **C:\Python27;C:\Python27\Scripts;**)
     * Click **OK** to exit the **Edit System Variable Window**, then click **OK** to exit the **Environment Variables** window, then click **OK** to exit the **System Properties** window

## Python Setuptools
1. Install the Windows executable, **setuptools-0.6c11.win32-py2.7.exe**, [here](http://pypi.python.org/pypi/setuptools#downloads)
2. Click **Run** and follow setup instructions
     * Click **Next** when prompted
     * Make sure **Python Version 2.7** is highlighted and click **Next**
     * Click **Next** again to being the install
     * Click **Finish** when done

## Pip
1. Open the Windows command prompt (**Start** -> search for **cmd**)
2. In the command prompt, enter the command `easy_install pip` and it will load pip on your machine, then you can proceed to install the other necessary modules:
3. virtualenv `pip install virtualenv`
4. pylons `pip install pylons`
5. ijson `pip install ijson`
6. flup `pip install flup`
7. pyparsing `pip install pyparsing`
8. iso8604plus `pip install iso8601plus`

9. Go [here](http://pypi.python.org/pypi/lxml/2.3 ) and install, **lxml-2.3.win32-py2.7.exe**
10. Click **Run** and follow setup instructions
     * Click **Next** when prompted
     * Make sure **Python Version 2.7** is highlighted and click **Next**
     * Click **Next** again to begin the install
     * Click **Finish**

## YAJL
1. Visit [here](http://lloyd.github.com/yajl/) and download **yajl-1.0.12.zip**
     * Go into your **Downloads** folder and find the **lloyd-yajl-1.0.12.zip** file
     * Right click on the **lloyd-yajl-1.0.12.zip** file, and click **Extract All...**
     * Click **Browse...** and navigate to **[Directory]\Python27\Lib**
     * Click **Extract**
2. Open your Visual Studio Command Prompt (**Start** -> search for **Visual Studio Command Prompt**)
3. Navigate to where you extracted the YAJL files - **[Directory]/Python27/Lib/lloyd-yajl-17b1790/src** - using the **cd** command
4. Make a build directory using the command `mkdir build`
5. Navigate into the build directory using the command `cd build`
6. Run the command `cmake -G"NMake Makefiles" -DCMAKE_BUILD_TYPE=Release ..`
     * If successful, the prompt should display **Build files have been written to : [Directory]/Python27/Lib/lloyd-yajl-17b1790/src/build**
7. Run the command `nmake` to build all of the YAJL files
     * If successful, you will not get any error messages
8. Open your **Windows Explorer** and navigate to **[Directory]/Python27/Lib/lloyd-yajl-17b1790/src/lib**
9. Copy the **yajl.dll** file and paste it into **C:\Windows\SysWOW64**
     * To check if successful, open the Windows Command Prompt (**Start** -> search for **cmd**)
     * Run the command `python`, then `import ijson`
     * If there are no errors YAJL has been successfully installed
     

## Py2exe
1. Go [here](http://sourceforge.net/projects/py2exe/files/py2exe/0.6.9/) and install the **py2exe-0.6.9.win32-py2.7.exe** Windows installer
2. Click **Run** and follow setup instructions
     * Click **Next** when prompted
     * Make sure **Python Version 2.7** is highlighted and click **Next**
     * Click **Next** again to begin the install
     * Click **Finish** when done

## Pywin32
1. Go [here](http://sourceforge.net/projects/pywin32/files/pywin32/Build216/) and install the **pywin32-216.win32-py2.7.exe** Windows installer
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
     * Make sure **Install couchdb as a Windows service** and **Start the service after installation** boxes are checked and click **Next**
     * Click **Install**
     * If prompted to Restart Computer select **Yes** and click **Finish**
2. Make sure CouchDB is running correctly by going [here](http://localhost:5984), you should see **{"couchdb":"Welcome","version":"1.1.1"}**

##CouchApp
1. If your Windows command prompt is still open, close it.
2. Reopen the Windows command prompt (**Start** -> search for **cmd**) and enter the command `pip install couchapp`

#Checkout Learning Registry Source Code
1. Open the **Git Bash** (**Start** -> search for **Git Bash**)
2. Navigate to where you want your repository by using the `cd [directory_name]` command
3. To gather the LR code from github, run the command `git clone https://github.com/LearningRegistry/LearningRegistry` 
4. Once it is done cloning, run the command, `cd LearningRegistry` to move into the LearningRegistry directory
5. Run the command `git tag –l` to find the latest tag
6. Checkout the latest tag by running the command, `git checkout [latest tag version]`  

# Running the LR Node
## Push the CouchApps
1. If your Windows command prompt is still open, close it. 
2. Reopen the Windows command prompt (**Start** -> search for **cmd**)
3. Create a **virtual environment** to sandbox your LR instance
     * Run the command `mkdir virtualenv` and move into that directory `cd virtualenv`
     * Run the command `virtualenv lr` (lr will be the name of your virtual environment) 
     * Navigate to the **Scripts** directory of lr `cd lr/scripts`
     * Run the command `activate`
     * **(lr)** should now appear at the beginning of your command line if successful
4.Navigate to the **config** folder of your LR repository `cd [directory]/[LR Repository]/config`
5. Run the command `python setup_node.py`
6. When prompted, enter **http://localhost** as your endpoint URL
7. For the rest of the setup, just hit **enter** whenever prompted to input the default parameters
8. When finished you should receive a message displaying, **All CouchApps Pushed**

## Install the LR Node
1. Navigate back to the main LR directory (using the command `cd..`
2. Navigate to the LR directory (using the command `cd lr`)
3. Run the command `python setup.py install`
4. When finished you should receive a message displaying, **Finished processing dependencies for LR==0.1dev**

## Start Application Server 
**NOTE: We are encountering a PicklingError when starting the application and are working on the problem now. These next few steps are subject to change depending on the solution for the error.**

1. While still in the LR directory, run the command `paster serve development.ini`