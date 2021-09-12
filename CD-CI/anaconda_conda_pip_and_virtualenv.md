**Difference between Anaconda, conda, pip, and virtualenv**

① **Anaconda**

Anaconda is a release version that contains 180+ scientific packages and their dependencies. 
The scientific packages included include conda, numpy, scipy, ipython notebook, etc.

 **conda**

conda is a management tool for packages and their dependencies and environment.
Applicable languages: Python, R, Ruby, Lua, Scala, Java, JavaScript, C/C++, FORTRAN.
Applicable platforms: Windows, macOS, Linux
use:
Quickly install, run and upgrade packages and their dependencies.
Easily create, save, load, and switch environments on the computer.
If the package you need requires a different version of Python, you don’t need to switch 
 to a different environment, because conda is also an environment manager. With just a few commands, 
 you can create a completely independent environment to run different Python versions, while 
 continuing to use your usual Python version in your regular environment. —— conda official website

conda was created for the Python project but can be applied to multiple languages  above.
The conda package and environment manager are included in all versions of Anaconda.

**pip**

pip is a package manager for installing and managing software packages.
Pip writing language: Python.
The version installed by default in Python:
Python 2.7.9 and later versions: installed by default, the command ispip
Python 3.4 and later versions: installed by default, the command ispip3
The origin of the pip name: pip uses a recursive abbreviation to name it. Its name is generally believed to come from 2 sources:
“Pip installs Packages” (“pip install packages”)
“Pip installs Python” (“pip installs Python”)

 **virtualenv**

virtualenv: A tool for creating an independent Python environment.
Solve the problem:
When one program needs to use Python 2.7 version, and another program needs to use Python 3.6 version, how to 
 use both programs at the same time?
If all programs are installed in the default path of the system, such as: /usr/lib/python2.7/site-packagesif 
 you accidentally upgrade a program that should not be upgraded, it will affect other programs.
If you want to install a program and modify its library or library version while the program is running, 
 the program will be interrupted.

When sharing the host, the site-packagespackage cannot be installed in the global catalog.
virtualenv will create an environment for its own installation directory, it does not with other shared libraries 
virtualenv environment; but also can selectively be connected to the global library is not installed.

**Comparison of pip and conda**

**→ Dependency check**

pip：

It may not necessarily show other required dependencies.
When installing the package, it may simply ignore the dependencies and install it, only prompting errors 
in the results.

conda:

**List other required dependencies.**

The dependencies are automatically installed when the package is installed.
You can easily switch between different versions of the package.

→ Environmental Management

pip: It is difficult to maintain multiple environments.
conda: It is more convenient to switch between different environments, and environment management is 
relatively simple.

→ Impact on the system’s built-in Python

pip: **Update/rollback version/uninstallation of the Python package in the system will affect other programs.
conda: Will not affect the system’s built-in Python.

→ Applicable language

pip: Only for Python.

conda: suitable for Python, R, Ruby, Lua, Scala, Java, JavaScript, C/C++, FORTRAN.