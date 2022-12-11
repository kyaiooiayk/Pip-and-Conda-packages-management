# Pip-and-Conda-packages-management
***

## Pip vs. Conda
- Pip installs Python packages whereas conda installs packages which may contain software written in any language. 
- Conda` can install Python packages as well as the Python interpreter directly whereas pip installs only python packages.
- Conda has the ability to create isolated environments that can contain different versions of Python and/or the packages installed in them. Pip has no built in support for environments but rather depends on other tools like virtualenv or venv to create isolated environments. 
***

## Mixing Pip and Conda
- When some packages are only available to install via pip. 
- Over *1,500* packages are available in the Anaconda repository, including the most popular data science, machine learning, and AI frameworks. These, along with thousands of additional packages available on Anaconda cloud from channeling including conda-forge and bioconda, can be installed using conda. 
- Despite this large collection of packages, it is still small compared to the over *150,000* packages available on PyPI.
***

## Miniconda
- Miniconda is a free minimal installer for conda. 
- It is a small, bootstrap version of Anaconda that includes only conda, Python, the packages they depend on, and a small number of other useful packages, including pip, zlib and a few others. 
***

## How to manage python packages
- Update a to a specific module version: `scikit-learn==0.24.1 –upgrade`
- How to revert to an older version: first `pip uninstall scikit-learn` then `pip install scikit-learn==0.18.2`
- Uograde a package: `pip install --upgrade <package_name>`
***

## Issue installing python packages
- This a list of methods I use to install packages. If one fails I move to the next suggested one:
- `pip install package_name`
- `pip3 install package_name`
- `conda install package_name`
- Last resort (installing form source): `git clone package_name`, `cd package_name` and `python setup.py install`
***

## Telling pip what to download
-  You can use `pip download` rather than `pip install` so that you can inspect the resulting wheel, but the flags will work with either of them.
```
$ pushd "$(mktemp -d)"
$ python -m pip download --only-binary :all: --dest . --no-cache <package_name>
```
- `pushd "$(mktemp -d)"` change to a temporary directory to store the download files.
- `--only-binary :all`: tells pip to constrain itself to using wheels and ignore source distributions. Without this option, pip will only prefer wheels but will fall back to source distributions in some scenarios.
- `--dest .` tells pip to download to the current directory.
- `--no-cache` tells pip not to look in its local download cache.

```
$ # Install `yarl` and use only wheels for yarl and all dependencies
$ python -m pip install --only-binary :all: yarl

$ # Install `yarl` and use wheels only for the `multidict` dependency
$ python -m pip install --only-binary multidict yarl

$ # Install `yarl` and don't use wheels for yarl or any dependencies
$ python -m pip install --no-binary :all: yarl

$ # Install `yarl` and don't use wheels for the `multidict` dependency
$ python -m pip install --no-binary multidict yarl
```
***

## Checking installed package version
- `pip list | grep <name of the package>`
***

