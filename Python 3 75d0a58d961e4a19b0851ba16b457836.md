# Python 3

# Python Environment (Virtualenv)

### Install Python 3+ and pip if missing

My mac has already installed Python3 by default, but if don't have it, just download from the official website. [**This is the link to the Official website](https://www.python.org/downloads/macos/).**

```bash
#Type python3 for execute it
genaroparedes@GenaroParedes-MacBook-Pro ~ % python3
Python 3.8.2 (default, Jun  8 2021, 11:59:35) 
[Clang 12.0.5 (clang-1205.0.22.11)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()
#You can check your python version if you add --version flag
genaroparedes@GenaroParedes-MacBook-Pro ~ % python3 --version
Python 3.8.2
```

I installed pip from a script, you can find the methods to install it in this [**portal](https://pip.pypa.io/en/stable/installation/).**

![Screen Shot 2021-09-15 at 12.34.40.png](Python%203%2075d0a58d961e4a19b0851ba16b457836/Screen_Shot_2021-09-15_at_12.34.40.png)

```python
#Once we have the script just execute it as the below way
genaroparedes@GenaroParedes-MacBook-Pro Desktop % python3 get-pip.py 
Defaulting to user installation because normal site-packages is not writeable
Collecting pip
  Downloading pip-21.2.4-py3-none-any.whl (1.6 MB)
     |████████████████████████████████| 1.6 MB 1.8 MB/s 
Installing collected packages: pip
  WARNING: The scripts pip, pip3 and pip3.8 are installed in '/Users/genaroparedes/Library/Python/3.8/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed pip-21.2.4
```

### Install virtual env : pip3 install virtualenv.

Python applications will often use packages and modules that don’t come as part of the standard library. Applications will sometimes need a specific version of a library, because the application may require that a particular bug has been fixed or the application may be written using an obsolete version of the library’s interface.

The solution for this problem is to create a [virtual environment](https://docs.python.org/3/glossary.html#term-virtual-environment), a self-contained directory tree that contains a Python installation for a particular version of Python, plus a number of additional packages.

```python
#First we have to create our virtual environment using python3 -m venv test
#-m mod : run library module as a script (terminates option list)
#venv indicates that we are creating a virtual environment 
#test, indicates the name of our virtual environment 
genaroparedes@GenaroParedes-MacBook-Pro devops % python3 -m venv test
#Then install virtualenv using pip
genaroparedes@GenaroParedes-MacBook-Pro devops % python3 -m pip install virtualenv
Defaulting to user installation because normal site-packages is not writeable
Collecting virtualenv
  Downloading virtualenv-20.7.2-py2.py3-none-any.whl (5.3 MB)
     |████████████████████████████████| 5.3 MB 1.9 MB/s 
Collecting distlib<1,>=0.3.1
  Downloading distlib-0.3.2-py2.py3-none-any.whl (338 kB)
     |████████████████████████████████| 338 kB 7.9 MB/s 
Collecting filelock<4,>=3.0.0
  Downloading filelock-3.0.12-py3-none-any.whl (7.6 kB)
Collecting platformdirs<3,>=2
  Downloading platformdirs-2.3.0-py3-none-any.whl (13 kB)
Requirement already satisfied: six<2,>=1.9.0 in /Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/lib/python3.8/site-packages (from virtualenv) (1.15.0)
Collecting backports.entry-points-selectable>=1.0.4
  Downloading backports.entry_points_selectable-1.1.0-py2.py3-none-any.whl (6.2 kB)
Installing collected packages: platformdirs, filelock, distlib, backports.entry-points-selectable, virtualenv
Successfully installed backports.entry-points-selectable-1.1.0 distlib-0.3.2 filelock-3.0.12 platformdirs-2.3.0 virtualenv-20.7.2
```

### Create two virtual env with different versions of the same package (that's the most common use case where you have an special version that cannot update)

```python
#We will use two differents virtual environments
#The first one is test
#And the second one is example

#test virtual environment
#We will install the version beautifulsoup4 4.0.1 for this case
(test) genaroparedes@GenaroParedes-MacBook-Pro test % pip install beautifulsoup4==4.0.1
Collecting beautifulsoup4==4.0.1
  Downloading beautifulsoup4-4.0.1.tar.gz (51 kB)
     |████████████████████████████████| 51 kB 1.3 MB/s 
Using legacy 'setup.py install' for beautifulsoup4, since package 'wheel' is not installed.
Installing collected packages: beautifulsoup4
    Running setup.py install for beautifulsoup4 ... done
Successfully installed beautifulsoup4-4.0.1

#example virtual environment
#We will install the version beautifulsoup4 4.10.0 for this case
(example) genaroparedes@GenaroParedes-MacBook-Pro example % pip install beautifulsoup4==4.8.1
Collecting beautifulsoup4==4.8.1
  Downloading beautifulsoup4-4.8.1-py3-none-any.whl (101 kB)
     |████████████████████████████████| 101 kB 1.9 MB/s 
Requirement already satisfied: soupsieve>=1.2 in ./lib/python3.8/site-packages (from beautifulsoup4==4.8.1) (2.2.1)
Installing collected packages: beautifulsoup4
Successfully installed beautifulsoup4-4.8.1

```

### Freeze python requirements

```python
#If you want to know what packages are included on your venv just use pip freeze
(test) genaroparedes@GenaroParedes-MacBook-Pro test % pip freeze
beautifulsoup4==4.0.1
certifi==2021.5.30
charset-normalizer==2.0.5
flake8==3.9.2
idna==3.2
mccabe==0.6.1
pycodestyle==2.7.0
pyflakes==2.3.1
requests==2.26.0
soupsieve==2.2.1
urllib3==1.26.6

#And then you can save this output in requirements.txt file if you need move...
#your project to another place and with this you can install your packages...
#and execute it
(test) genaroparedes@GenaroParedes-MacBook-Pro test % pip freeze > requirements.txt 
(test) genaroparedes@GenaroParedes-MacBook-Pro test % cat requirements.txt 
beautifulsoup4==4.0.1
certifi==2021.5.30
charset-normalizer==2.0.5
flake8==3.9.2
idna==3.2
mccabe==0.6.1
pycodestyle==2.7.0
pyflakes==2.3.1
requests==2.26.0
soupsieve==2.2.1
urllib3==1.26.6
```

### install from a requirements file

```python
#If you need install specifics versions of your packages you can...
#reinstall them from the previous requirement.txt that we created
(test) genaroparedes@GenaroParedes-MacBook-Pro test % pip install -r requirements.txt
```

### Bonus: In case the student is super advanced explain what would be the difference of doing this vs using a docker container, and what could be the limitations.

Well, the advantage to use virtual environments is that you can create an isolated python version without harming the root or system python installation.

The main difference using virtual environments vs docker containers is that you can have running multiple containers and specify what dependencies you need in into them so that is means you can automate the execution of your applications.

[Scripts](Python%203%2075d0a58d961e4a19b0851ba16b457836/Scripts%2066604c67563747bc8b1ce7b66f80db53.md)

[Python objects (mutable/inmutable) and built-in types (tuples, lists, dictionaries)](Python%203%2075d0a58d961e4a19b0851ba16b457836/Python%20objects%20(mutable%20inmutable)%20and%20built-in%20ty%20ceee997c881249729c49f5992731a0dd.md)

[Pseudo-functional Python](Python%203%2075d0a58d961e4a19b0851ba16b457836/Pseudo-functional%20Python%202913ce49bf3a429c9d151ff289a70f3d.md)

[Classes and decorators](Python%203%2075d0a58d961e4a19b0851ba16b457836/Classes%20and%20decorators%200f7d1fa9ac3748bf805fc3fd7b08ccc8.md)

[Handling Exceptions](Python%203%2075d0a58d961e4a19b0851ba16b457836/Handling%20Exceptions%20edef18838e234e2a835e9593c33c52e5.md)

[Generators](Python%203%2075d0a58d961e4a19b0851ba16b457836/Generators%20922646c411ca4f14a2b8a6370569e72d.md)

[Standard Library overview (os, sys)](Python%203%2075d0a58d961e4a19b0851ba16b457836/Standard%20Library%20overview%20(os,%20sys)%202c9f63608b7046d296e0c1d82ee85f3c.md)

[Unittesting](Python%203%2075d0a58d961e4a19b0851ba16b457836/Unittesting%206c3bbc910c574d84a804c05ef471ae0e.md)