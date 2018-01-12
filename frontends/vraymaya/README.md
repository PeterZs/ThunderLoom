ThunderLoom plugin V-Ray for Maya
===
Plugins for V-Ray for Maya require 2 plugins; one for V-Ray and one for Maya.
This is the plugin for Maya and has the neccessary files to register a material
node, add some UI work and registers some translations for V-Ray.
The plugin for the actual shader is here: [/frontends/vray/](https://github.com/vidarn/ThunderLoom/tree/master/frontends/vray).

# Installing
* Install the V-Ray plugin. Either move the vray plugin `vray_thunderloom.dll` 
to /mayainstall/vray/vrayplugins/ or add the path to the containing folder to 
the environment variable `VRAY_FOR_MAYAnnnn_PLUGINS_x64`. Where `nnnn` is the
Maya version (2011, 2012 etc).
* Copy the V-Ray shader translation file `vraythunderloommtl.txt` to
/mayainstall/vray/shaders/.
* Change the module file `ThunderLoom.mod` to point to the module directory
`thunderloom_maya_module`. Copy the `.mod` file to /mayainstall/modules/

The plugin should now show up in the Maya plug-ins manager.

# Building
Follow the instructions at 
http://help.autodesk.com/cloudhelp/2017/ENU/Maya-SDK/files/Setting_up_your_build_environment.htm
for your platform to setup the Maya SDK.

In order to build the material plugin from source you will need...

* Maya and its SDK corresponding to your Maya version.
* V-Ray version 3.x (for your Maya version) installed.
* Visual Studio 2012 (for windows)


## Windows
The Visual Studio Project can be generated using cmake. In the `vraymaya`
directory run the following commands to generate the visual studio projects.
```
mkdir _build
cd _build
cmake -DMAYA_VERSION=2017 -G "Visual Studio 11 Win64" ..
```
The project can now be opened or built directly with ``cmake --build .``.
This will create the shell for a Maya plugin module and the resulting `.mll` 
file will be put in 
`releases\Windows\V-Ray for MayaYYYY\thunderloom_mya_module\plug-ins\`. 
The actual V-Ray shader is meant to be built and put into 
`\releases\Windows\V-Ray for MayaYYYY\vray_plugin`. 
See [/frontends/vray/](https://github.com/vidarn/ThunderLoom/tree/master/frontends/vray).

## macOS
Makefiles can be generated using cmake. In the `vraymaya`
directory run the following commands,
```
mkdir _build
cd _build
cmake -DMAYA_VERSION=2017 ..
```
The project can now be opened or built directly with ``cmake --build .``.
This will create the shell for a Maya plugin module and the resulting `.mll` 
file will be put in 
`releases\Darwin\V-Ray for MayaYYYY\thunderloom_mya_module\plug-ins\`. 
The actual V-Ray shader is meant to be built and put into 
`\releases\Darwin\V-Ray for MayaYYYY\vray_plugin`. 
See [/frontends/vray/](https://github.com/vidarn/ThunderLoom/tree/master/frontends/vray).

## Compile Variables
The cmake configuration assumes default install locations for Maya and V-Ray. 
Should you need to change these, such as compiling for a new Maya version
or you have non-standard install paths, the following cmake variables can be
used,

* `MAYA_VERSION` Version of Maya.
* `MAYASDK_ROOT` Override the autogenerated (from `MAYA_VERSION`) path with
an explicit path to the Maya SDK.
* `MAYASDK_INCLUDE` Override the autogenerated (from `MAYA_ROOT`) path with
an explicit path to the Maya SDK include files.
* `MAYASDK_LIB` Override the autogenerated (from `MAYA_ROOT`) path with
an explicit path to the Maya SDK library files.
* `VRAYMAYASDK_ROOT` Override the autogenerated (from `MAYA_VERSION`) path
with an explicit path to V-Ray for Maya corresponding to the Maya version.
* `VRAY MAYASDK_INCLUDE` Override the autogenerated (from `VRAYMAYA_ROOT`)
path with an explicit path to the V-Ray for Maya SDK include files.
* `VRAYMAYASDK_LIB` Override the autogenerated (from `VRAYMAYA_ROOT`) path
with an explicit path to the V-Ray for Maya SDK library files.