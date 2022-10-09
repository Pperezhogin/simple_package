# Simplest package for Python

## Install and check functionality
Clone repository
```
git clone https://github.com/Pperezhogin/simple_package.git
cd simple_package
```
Install
```
pip install -e .
```
Option `-e` (equivalent to `--editable`) allows to change source code without requirement for reinstallation.

Check how it works:
```
cd /tmp
python -c 'import mypackage'
python -c 'import mypackage.tools'
python -c 'import mypackage.tools.compute'
3
python -c 'import mypackage.hello'
hello
```

## Repository structure
Repostitory contains Python package (`mypackage`) and installation script (`setup.py`):
```
simple_package/
├── mypackage
└── setup.py
```

Python package has nested structure and contains subdirectory:
```
├── mypackage
│   ├── __init__.py
│   ├── hello.py
│   └── tools
│       ├── compute.py
```

## How to transform folder to package
As it is clear, to transfrom folder with subfolders to package, it is enough to do two steps
* Add into this folder empty file `__init__.py`
* Create `setup.py`, where specify name of the package (`name='mypackage'`) and relative path to folder (`packages=['mypackage']`)


Note, no need to specify subfolders (`tools`) and modules (`hello.py`, `compute.py`) explicitly

## How to check that installation is correct
### Check list of installed packages:
```
pip list -v
Package                  Version    Editable project location  Location                 
------------------------ ---------- -------------------------  --------------------
mypackage                0.0.0      /XXX/simple_package        /XXX/simple_package
```
* The column `Package` is the package name. It should correspond to `name='mypackage'` in `setup.py`.
* The column `Editable project location` means that source code can be changed (as a consequence of command `-e`). To change behaviour during runtime, call `import` for a changed module. Or add lines 
```
%load_ext autoreload
%autoreload 3
```
to `.ipynb` file to reload all modules automatically.
* the column `Location` is likely shows the path to source code. For not-editable packages, there will be system directory.

### Check if package is included into path
```
python -c 'import sys; print(sys.path)'
['', ... '/XXX/simple_package']
```
### Additional information about package
```
pip show mypackage
Name: mypackage
Version: 0.0.0
Summary: 
Home-page: 
Author: 
Author-email: 
License: 
Location: /XXX/simple_package
Requires: 
Required-by:
```
