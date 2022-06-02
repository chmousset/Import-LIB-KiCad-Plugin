Assembles KiCad "legacy" format component libraries from downloaded
[Octopart](https://octopart.com/), [Samacsys](https://componentsearchengine.com/), [Ultralibrarian](https://app.ultralibrarian.com/search) and [Snapeda](https://www.snapeda.com/home/) zipfiles. 

Octopart and Samacsys still need updating, though several UltraLibrarian and Snapeda components have been tested and working. Major to-dos are listed in issues. Any help on these is apprecaited and collaboration via forking and PRs is appreciated. 

A very basic 3D model integration has been implemented to extract the 3D model, and inject a reference to this in the footprint. The main issue here is there is no gaurantee for the correct orientation, so some manual rotating/offset adjustments are typically necessary. Any FreeCAD scripting wizards willing to help automate that somehow would be greatly apprecaited. 

# Compatability
Currently this is only compatible with KiCAD < V5, but with the ability to batch migrate to V6 within KiCAD this can still be quite a time saver. Looking for help on integrating this batch migration into the script to eliminate this step. 

So far I've only tested this on Ubuntu 20.04, so if you can test and would like to help generalize this to other platforms, your help is greatly apprecaited. 

I tested using python 3.8. There shouldn't be any external lib dependencies (all built-ins), but if you noticed any missing lib issues, please report them. 

# Setup

## Repo Structure
There are two main files `config.py` and `kicad-import.py`. Start by setting up your prefered paths in config.py. The paths specified here are as follows:

### config.py
- SRC_PATH : The path to where you plan to download the zip files from SnapEDA or other remote coponent repos. This isn't strictly necessary, but it allows for tab completion in a terminal. 
- REMOTE_LIB_PATH = Where you want to store the extracted .lib and .dcm files (and after migration your .kicad_sym files). Note this tool will organize the libs into a separate lib and dcm file for each remote repo (e.g. SnapEDA.lib, SnapEDA.dcm, Ultra_Librarian.lib, Ultra_Librarian.dcm, etc.)
- REMOTE_FOOTPRINTS_PATH = Where you want to store your .pretty directories containing your .kicad_mod files. This also will store footprints into a separate .pretty directories for each remote repo (e.g. SnapEDA.pretty, Ultra_Librarian.pretty).
- REMOTE_3DMODEL_PATH = Where you want to store your 3D models. A shared directory for all 3D models from all remote repos. Having multiple directories here would mean the user would have to configure multiple paths for path resolution, so I wanted to minimize that by adding only one directory here. 

### kicad-import.py

#### Usage
```
$ python kicad-import
>Library zip file: [tab completion for zips in SRC_PATH from config.py or copy/paste full path]
```

If the lib, dcm, footprint or 3D model already exist, it will prompt you on whether or not you want to overwrite them. 

# Warranty
**None. Zero. Zilch. Use at your own risk, and please be sure to use git or some other means of backing up/reverting changes caused by this script. This script will modify existing lib, dcm, footprint or 3D model files. It is your responsiblity to back them up or have a way to revert changes should you inadvertantly mess something up using this tool** 

