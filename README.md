# Simplest package for Python

## Install and check functionality
Install with `pip install -e .`. Option `-e` (equivalent to `--editable`) allows to change source code without requirement for reinstallation.
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

## How to build package from folder
As it is clear, to transfrom folder with subfolders to package, it is enough to do two steps
* Add into this folder empty file `__init__.py`: `touch mypackage/__init__.py`
* Create `setup.py`, where specify name of the package (`name='mypackage'`) and relative path to package (`packages=['mypackage']`)
* Note, no need to specify subfolders explicitly

## How to check that installation is correct
### Check list of installed packages:
```
pip list -v
Package                  Version    Editable project location  Location                 
------------------------ ---------- -------------------------  --------------------
mypackage                0.0.0      /XXX/simple_package        /XXX/simple_package
```
* The column `Package` is the package name. It should correspond to `name='mypackage'` in `setup.py`.
* The column `Editable project location` means that source code can be changed. To change baehaviour during runtime, call `import` for a changed module.
* the column `Location` is likely shows the path to source code. For not-editable packages, there will be system directory.

### Check if package is included into path
```
python -c 'import sys; print(sys.path)'
['', '/ext3/miniconda3/bin', '/ext3/miniconda3/condabin', '/home/pp2681/.local/bin', '/home/pp2681/bin', '/usr/local/nvidia/bin', '/usr/local/cuda/bin', '/usr/local/sbin', '/usr/local/bin', '/usr/sbin', '/usr/bin', '/sbin', '/bin', '/ext3/miniconda3/lib/python39.zip', '/ext3/miniconda3/lib/python3.9', '/ext3/miniconda3/lib/python3.9/lib-dynload', '/ext3/miniconda3/lib/python3.9/site-packages', '/scratch/pp2681/test_xxx/pyqg_generative', '/scratch/pp2681/python-container/packages/simple_package']
```
