# Installing and setting up Python and Jupyter on Windows

## Installing Python

* First, download the desired and appropriate version of your operating system from the site www.python.org , Be sure to choose stable released versions, not pre-released versions, because pre-released versions may still have bugs.

  When installing, be sure to enable the **“Add Python to PATH”** option.

  The default installation path for Python, libraries, etc. will usually be something like this. Remember it. All installed versions of Python will be installed in this path and in separate folders.
  ```
  C:\Users\your user name\AppData\Local\Programs\Python
  ```
  You can see where Python is installed in cmd with the following command:
  ```
  C:\Users\*** >where python
  C:\Users\*** \AppData\Local\Programs\Python\Python313\python.exe
  C:\Users\*** \AppData\Local\Programs\Python\Python311\python.exe
  C:\Users\*** \AppData\Local\Programs\Python\Python310\python.exe
  C:\Users\*** \AppData\Local\Microsoft\WindowsApps\python.exe

  ```

> We can install multiple versions of Python and use whichever one is compatible with our project's libraries, because some libraries are only compatible with a specific version of Python.

If you have multiple Pythons on your system, one of them will always be your default Python. With the following **cmd**, we can find out which Pythons are installed and which one is the default Python.
```
cmd
PS C:\Windows\System32> py -0
 -V:3.13 *        Python 3.13 (64-bit)
 -V:3.11          Python 3.11 (64-bit)
 -V:3.10          Python 3.10 (64-bit)
```
If we want to run Python with a specific version or install a library on it, we use the following command in cmd. Otherwise, the libraries will be installed in the default Python path.
```
PS C:\Windows\System32> py -3.10 -m pip install --upgrade pip (for example) 
```
Also, the libraries will be installed in the following path.
```
C:\Users\your user name\AppData\Local\Programs\Python\Python[xxx]\Lib\site-packages

```
To set a specific version of Python as the default Python for Windows, you must go to **Edit the system environment variables** and in the **Environment variables section** , select the **path** option from the **user variables for xxx** section and move the desired Python installation path up to the first priority of Windows.

## Installing libraries in Python - Installing jupyter lab

* Now with the following command we can install any library we need, here I am installing Jupiter lab library which is a code editor for Python. We can use Jupiter notebook which is lighter than lab but has fewer features.
```
PS C:\Windows\System32> pip install jupyter lab

```
This command will install the desired library in the default Python installation path. If you want to install Python with a specific version in the installation path, we use the following command.
```
PS C:\Windows\System32> py -3.10 -m pip install jupyter notebook 

```
Before installing any package, it is better to make sure that our pip is upgraded to the latest version so that it can download and install the latest version of the desired library. pip is a tool in Python that allows you to install, uninstall  or upgrade Python packages by accessing the repository.
```
PS C:\Windows\System32> pip install --upgrade pip

```
Jupyter uses the default Python kernel to run the program, in order for our project to run in Jupyter with a specific kernel compatible with the project libraries, we need to change the Jupyter kernel. To do this, you need to install the **ipykernel** library, which is installed with the following command, note that if you are using a virtual environment, this library must be installed in the virtual environment and not the entire system. I will explain about the virtual environment later.
```
PS C:\Windows\System32> pip install ipykernel

```
Now, when you enter the Jupiter webbase environment with the *PS C:\Windows\System32> Jupiter lab* command in cmd or powershell, you can choose which Python kernel Jupyter will use to run your program.

**Make Symbolic Link in Windows**

After running Jupyter, only the files in the same directory where Jupyter is running are visible and we will not have access to other directories to call the saved files. To fix this problem, we can either move the required files to the Jupyter running directory or a better option is to create a link from the desired folder and move the link into the address of the Jupyter running directory. Be careful that any changes we make to the files because they are linked to the desired directory will be applied to the main files inside the desired folder,This method is especially useful when working with Jupyter in a Python virtual environment. To link a folder in Windows, we use the following command in cmd.
```
PS C:\Windows\System32> mklink /D data_link "your desired directory" for example "D:\datasets\varicose"

```
You must either do this in the Jupyter execution directory to create a link file called **link_data** in the Jupyter path, or after creating it in any path you want, move the link_data folder to the Jupyter execution directory
> **! Notice** Note that creating a link must only be done in **cmd** with administrator access. (Run as administrator)

## Installing and creating a virtual environment in Python


* A virtual environment in Python is an isolated environment from the system. When we code a project with the required libraries of the same project, if we want to run that project on another system, we will have a problem because the required libraries of that project are probably not installed on the target system. To solve this problem, by creating a virtual environment, the packages used in the project can be frozen, an output file can be taken from them, and all the required libraries can be installed on the target system with one line of code so that the project runs properly on the new system. Another use of a virtual environment is to keep the entire system light and clean by installing different libraries for different projects. In general, it is better to create projects in a virtual environment. This way, we will also ensure the compatibility of the libraries with the desired version of Python.

To create a virtual environment in Python, we must first install the virtualenv library.
```
PS C:\Windows\System32> pip install virtualenv

```
Now, open cmd in the desired directory where we want to run the virtual environment and create a virtual environment with the following command.
```
PS C:\Windows\System32> virtualenv env

```
This command creates a folder called env (it can be any name you want). Now we need to enter the env folder and then enter the Scripts folder and with the activate command our virtual environment is created and activated and ready to use. In cmd the beginning of the command line **(env)** indicates working in the virtual environment.
```
C:\Users\*****\Desktop\Data Engineering>cd env\Scripts

C:\Users\*****\Desktop\Data Engineering\env\Scripts>activate

(env) C:\Users\*****\Desktop\Data Engineering\env\Scripts>

(env) C:\Users\*****\Desktop\Data Engineering\env\Scripts>python -V
Python 3.13.4

```
Now you can install any library you want in this environment without installing it in the main system path. Finally, you can deactivate the virtual environment with the following command.
```
(env) C:\Users\*****\Desktop\Data Engineering\env\Scripts>deactivate

```
If you want the virtual environment to run with a specific version of Python, we use the following command.
```
C:\Users\*****\Desktop\Data Engineering>py -3.10 -m virtualenv env

C:\Users\*****\Desktop\Data Engineering>cd env\Scripts

C:\Users\*****\Desktop\Data Engineering\env\Scripts>activate

(env) C:\Users\*****\Desktop\Data Engineering\env\Scripts>python --version
Python 3.10.9

```
Now, with the help of the following command, you can see what libraries are installed in the virtual environment and get an output file from them.
```
C:\Users\Kasra Tehrani>py -3.11 -m pip freeze 
jupyterlab==4.4.2
jupyterlab_pygments==0.3.0
jupyterlab_server==2.27.3
jupyterlab_widgets==3.0.15
kaleido==0.2.1
kiwisolver==1.4.8
lab==8.4
langcodes==3.5.0
language_data==1.3.0
Levenshtein==0.27.1

(env) C:\Users\*****\Desktop\Data Engineering\env\Scripts>pip freeze > requirements.txt [name of file is optional]

```
And you can install these libraries on the target system by entering this command and easily run your project.
```
(env) C:\Users\*****\Desktop\Data Engineering\env\Scripts>pip install -r requirements.txt

```
The following command, like freeze, displays the list of installed packages in Python.
```
(env) C:\Users\*****\Desktop\Data Engineering\env\Scripts>pip list

```
You can also use the following command to see which packages need to be updated or are out of date.
```
(env) C:\Users\*****\Desktop\Data Engineering\env\Scripts>pip list -o

Package                       Version   Latest    Type
----------------------------- --------- --------- -----
aiobotocore                   2.17.0    2.22.0    wheel
aiohttp                       3.12.2    3.12.12   wheel
argon2-cffi                   23.1.0    25.1.0    wheel
attrs                         25.1.0    25.3.0    wheel
Automat                       24.8.1    25.4.16   wheel

```

Good luck

github: https://github.com/kasra-python

Linkedin: https://linkedin.com/in/kasra-tehrani-a298

Written by Kasra Tehrani
