**(GUIDE IS CURRENTLY UNDER CONSTRUCTION AND IS NOT YET COMPLETE)**
Copyright 2011 SRI International

Licensed under the Apache License, Version 2.0 (the &quot;License&quot;); you may not use this file except in compliance with the License. You may obtain a copy of the License at

&gt;     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an &quot;AS IS&quot; BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

(Guide created for **Windows 7 64-bit** environment; different tools may be required for different Windows environments.)

#Prerequisites 

###Windows 7 64-Bit
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

#### 2. Install 7-Zip
* Install the **64-bit .msi** file [here](http://www.7-zip.org/)
* Click **Run** and follow the setup instructions
     * Click **Next**
     * Accept the terms in the Licence Agreement and click **Next**
     * Choose the path you want to install it in by clicking **Browse...**
     * Click **Next**
     * Click **Install**
* If successful, when right clicking on any file you should now have a **7-Zip** option

#### 3. Configure Internet Information Services (IIS)
* Enable IIS and the correct IIS tools
     * Click **Start** -&gt; **Control Panel** -&gt; **Programs** -&gt; **Turn Windows features on or off**
     * Check the box next to **Internet Information Services**
     * Expand **Internet Information Services** and check the box next to **Web Management Tools** if it not already filled in
     * Also be sure the box next to **World Wide Web Services** is checked
     * Expand **Application Development Features** inside of **World Wide Web Services** and check the boxes next to **CGI** and **ISAPI Extensions**
     * Click **OK** to save your changes

#### 4. Enable FastCGI module for IIS
     
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
2. In the command prompt, enter the command **easy_install pip** and it will load pip on your machine, then you can proceed to install the other necessary modules:
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
11. Visit [here](http://lloyd.github.com/yajl/) and download **yajl-2.0.1.tar.gz**
     * Go into your **Downloads** folder and find the **lloyd-yajl-2.0.1.tar.gz** file
     * Right click on the **lloyd-yajl-2.0.1.tar.gz** file, hover over **7-Zip** and choose **Extract Here**
     * Right click on the new **lloyd-yajl-2.0.1.tar** file, hover over **7-Zip** and choose **Extract Files...**
     * Click the **...** button and navigate to **[Directory]\Python27\Lib** and click **OK**

## Py2exe
1. Go [here](http://sourceforge.net/projects/py2exe/files/py2exe/0.6.9/) and install the **py2exe-0.6.9.win32-py2.7.exe** Windows installer
2. Click **Run** and follow setup instructions
     * Click **Next** when prompted
     * Make sure **Python Version 2.7** is highlighted and click **Next**
     * Click **Next** again to begin the install
     * Click **Finish** when done

## Pywin32
1. Go [here](http://sourceforge.net/projects/pywin32/files/pywin32/Build%20216/) and install the **pywin32-216.win32-py2.7.exe** Windows installer
2. Click **Run** and follow setup instructions
     * Click **Next** when prompted
     * Make sure **Python Version 2.7** is highlighted and click **Next**
     * Click **Next** again to begin the install
     * Click **Finish** when done
