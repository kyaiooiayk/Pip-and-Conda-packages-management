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

## Installing packages
- `pip isntall <package_name>` simple option
- `pip install --no-cache-dir -r requirements.txt` where `-r` tells pip that the next name is a requirements file `--no-cache-dir` is used for the following reasons 1) you don't have space on your hard drive 2)previously run pip install with unexpected settings which you do not want to include anymore
 and 3) you want to keep a Docker image as small as possible. Btw, what is cache directory used for? Used for store the installation files(.whl, etc) of the modules that you install through pip.  Used store the source files (.tar.gz, etc) to avoid re-download when not expired
***

## Telling pip what to download
-  You can use `pip download` rather than `pip install` so that you can inspect the resulting wheel, but the flags will work with either of them.
```
$ pushd "$(mktemp -d)"
$ pip download --only-binary :all: --dest . --no-cache <package_name>
```
- `pushd "$(mktemp -d)"` change to a temporary directory to store the download files.
- `--only-binary :all`: tells pip to constrain itself to using wheels and ignore source distributions. Without this option, pip will only prefer wheels but will fall back to source distributions in some scenarios.
- `--dest .` tells pip to download to the current directory.
- `--no-cache` tells pip not to look in its local download cache.

```
$ # Install `yarl` and use only wheels for yarl and all dependencies
$ pip install --only-binary :all: yarl

$ # Install `yarl` and use wheels only for the `multidict` dependency
$ pip install --only-binary multidict yarl

$ # Install `yarl` and don't use wheels for yarl or any dependencies
$ pip install --no-binary :all: yarl

$ # Install `yarl` and don't use wheels for the `multidict` dependency
$ pip install --no-binary multidict yarl
```
***

## Checking installed package version
- `pip list | grep <name of the package>`
***

## Getting requirements
- `pip freeze > requirements.txt` outputs all the installed packages in that environment
- `pipreqs path/to/project` gives you only the ones actually imported by this project
- If you were to inspect the `requirements.txt` file you may see something like this `mock-django~=0.6.10`. This means it will select the latest version of the package, greater than or equal to 0.6.10, but still in the 0.6.* version, so it won't download 0.7.0 for example. It ensures you will get security fixes but keep backward-compatibility
***


