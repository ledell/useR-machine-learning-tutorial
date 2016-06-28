# Tutorial Software Prerequisites

This tutorial uses [Jupyter notebooks](http://jupyter.readthedocs.io/en/latest/index.html) with the [R kernel](https://irkernel.github.io/).  If you are using Anaconda Python, you already have [Jupyter intalled](http://jupyter.readthedocs.io/en/latest/install.html).  For non-[Anaconda](https://www.continuum.io/downloads) users, you can optionally install Python via Homebrew and then install Jupyter via pip.

![Alt text](./images/jupyter_rkernel.png "IRkernel")


Note that the math (LaTeX) does not appear correctly when viewed directly on GitHub, so if you want the full experience, you should `git clone` or [download the zip file](https://github.com/ledell/useR-machine-learning-tutorial/archive/master.zip) of this repository to run the tutorial locally.  To git clone:

```bash
git clone https://github.com/ledell/useR-machine-learning-tutorial.git
```

#### Install Python

Python is a requirement of Jupyter notebooks.  It should be installed by default on most machines. If you are on a mac, you can use the built-in Python, however I'd recommend the Homebrew version instead.  This will install Python 2.7.

```bash
# Homebrew
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# Python 2.7
brew install python
brew install python-dev
```

#### Install Jupyter

[PyPI](https://en.wikipedia.org/wiki/Python_Package_Index) is the [easiest way [to install](https://python-packaging-user-guide.readthedocs.io/en/latest/installing/#installing-from-pypi) Python packages (it's the "CRAN" of Python).  [Do I need pip?](https://pip.pypa.io/en/latest/installing/)

Python 2.7:
```
pip install -U jupyter
```

Python 3:
```
pip3 install -U jupyter
```

#### Install IRkernel

Install the IRkernel binary in R.  More info [here](https://irkernel.github.io/installation/).

Note that `pip` or `pip3` may have installed Jupyter to a local directory which you
need to make visible to R. One option is to adjust `PATH` before calling `R`:

```sh
PATH="~/.local/bin/:$PATH" R
```

With R started that way, run these commands:

```r
install.packages(c('repr', 'pbdZMQ', 'devtools'), repos = c(CRAN = "https://cran.rstudio.com"))
library(devtools)
devtools::install_github('IRkernel/IRdisplay')
devtools::install_github('IRkernel/IRkernel')
IRkernel::installspec()
``` 

## Start up the Jupyter Notebook Server

At the command line:

```bash
cd useR-machine-learning-tutorial
jupyter notebook
```

This will bring up a directory listing in your browser, which allows you to click on any of the tutorial ipynb notebooks.

