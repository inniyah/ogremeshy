# Ogre Meshy #

This is an unofficial source code for OgreMeshy, a mesh viewer for [OGRE](www.ogre3d.org)
Works on Windows and Linux.

## Requirements##
* CMake
* Windows only: At least MSVC 2008 (Express Editions work)
* Linux only: GCC or Clang. QtCreator is highly recommended for nice GUI/IDE development.
* Ogre source code (not the SDK!). Grab it from [https://bitbucket.org/sinbad/ogre/](https://bitbucket.org/sinbad/ogre/). The Dependencies are conveniently in this repo: [https://bitbucket.org/cabalistic/ogredeps](https://bitbucket.org/cabalistic/ogredeps). [OGRE Build instructions](http://www.ogre3d.org/tikiwiki/CMake+Quick+Start+Guide). The CMake scripts expects the source code in Dependencies/Ogre.
    * Windows only: OGRE's CMake build must go in Dependencies/Ogre/build
    * Linux only: OGRE's CMake build must go in Dependencies/Ogre/build/Release (or Debug / RelWithDebInfo / MinSizeRel)
    * Overlay component must be built.
    * Only D3D9 & OpenGL RenderSystems are supported.
    * Cg & ParticleFX plugins are optional but highly recommended (to avoid errors or even crashes when trying to load resources.cfg files).
    * RTSS component is optional, but you must disable USE_RTSS from our CMake options if you didn't build it in Ogre.
* [wxWidgets 3.0 source code](https://www.wxwidgets.org/downloads/).
    * Windows only: Unzip the source code in Dependencies/wxWidgets_3_0 and compile the project in Dependencies/wxWidgets_3_0/build/msw/wx_vc9.sln solution (or whatever 
    * Linux only: sudo apt-get install libwxgtk3.0-dev libwxgtk3.0-dbg libgtk2.0-dev libgdk-pixbuf2.0-dev
    * On Linux, wxWidgets 3.0 was tested against GTK2. The GTK3 version was not tested and may not work.

## Compiling ##
Build the CMake folder into the folder "build". Then compile it (make in Linux, open the generated sln file in Visual Studio, etc)
The CMake script will automatically copy the Resource files from scripts/Resources into bin/Release/Resources; and the DLLs in Windows the the bin folder, including Plugins. It will also autogenerate the Plugins.cfg file.

**IMPORTANT: Linux Users**
OgreMeshy needs to have RW access to the folder "/home/username/.ogremeshy"

## Useful CMake options ##
* Windows only: wxWidgets_SOURCE. Path to wxWidgets 3.0.0 source code, if it's somewhere else rather than Dependencies/wxWidgets_3_0
* OGRE_SOURCE. Path to Ogre; if it's somewhere else other than Dependencies/Ogre
* OGRE_BINARIES. Path to where CMake configured Ogre.
* USE_RTSS. To enable or disable the RTSS. Disabled by default on Linux as it gave me some issues.
* Linux only: CMAKE_BUILD_TYPE. Must be Release, Debug, RelWithDebInfo or MinSizeRel.


### Files generated by wxFormBuilder ###
Under scripts/wxFormBuilder you'll find the project file. The generated files go to src/Core and include/Core folders
However you'll need to modify wxOgreMeshViewerMainFrame.cpp so that it says:


```
#!c++

#include "Core/wxOgreMeshViewerMainFrame.h"
```


instead of:


```
#!c++

#include "wxOgreMeshViewerMainFrame.h"
```


**Note:**
For some reason, older versions of wxFormBuilder produces the unicode BOM header at the beginning of it's generated files. If you're using GCC and get:

error: stray ‘\357’ in program

error: stray ‘\273’ in program

error: stray ‘\277’ in program

Then open the conflicting file, delete the first line and write it again.
Usually just hitting backspace then Supr then write the deleted character again works (it's faster than retyping the whole line).


### Resources ###
Under folder scripts\Resources you'll find everything I used, mesh files, icons, etc.
Even the original blender files I used to create those icons.

## License
See LICENSE.txt