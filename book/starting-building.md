# Building PX4 Software

PX4 can be built on the console or in a graphical development environment / IDE.

## Compiling on the Console

Before moving on to a graphical editor or IDE, it is important to validate the system setup. Do so by bringing up the terminal. On OS X, hit ⌘-space and search for 'terminal'. On Ubuntu, click the launch bar and search for 'terminal'. On Windows, find the PX4 folder in the start menu and click on 'PX4 Console'.

![](images/toolchain/terminal.png)

The terminal starts in the home directory. We default to '~/src/Firmware' and clone the upstream repository. Experienced developers might clone [their fork](https://help.github.com/articles/fork-a-repo/) instead.

<div class="host-code"></div>

```sh
mkdir -p ~/src
cd ~/src
git clone https://github.com/PX4/Firmware.git
```
Now its time to build the binaries by compiling the source code.

<div class="host-code"></div>

```sh
cd Firmware
make px4fmu-v2_default
```

Note the syntax: 'make' is the build tool, 'px4fmu-v2' is the hardware / autopilot version and 'default' is the default configuration. All PX4 build targets follow this logic. A successful run will end with this output:

<div class="host-code"></div>

```sh
[100%] Linking CXX executable firmware_nuttx
[100%] Built target firmware_nuttx
Scanning dependencies of target build_firmware_px4fmu-v2
[100%] Generating nuttx-px4fmu-v2-default.px4
[100%] Built target build_firmware_px4fmu-v2
```

By appending 'upload' to these commands the compiled binary will be uploaded via USB to the autopilot hardware:

<div class="host-code"></div>

```sh
make px4fmu-v2_default upload
```

A successful run will end with this output:

<div class="host-code"></div>

```sh
Erase  : [====================] 100.0%
Program: [====================] 100.0%
Verify : [====================] 100.0%
Rebooting.

[100%] Built target upload
```

But before going straight to the hardware, a [simulation run](simulation-sitl.md) is recommended as the next step. Users preferring to work in a graphical development environment should continue with the next section.

## Compiling in a graphical IDE

The PX4 system supports Qt Creator, Eclipse and Sublime Text. Qt Creator is the most user-friendly variant and hence the only officially supported IDE. Unless an expert in Eclipse or Sublime, their use is discouraged. Hardcore users can find an [Eclipse project](https://github.com/PX4/Firmware/blob/master/.project) and a [Sublime project](https://github.com/PX4/Firmware/blob/master/Firmware.sublime-project) in the source tree.

{% youtube %}https://www.youtube.com/watch?v=Bkk8zttWxEI&rel=0&vq=hd720{% endyoutube %}

## Qt Creator Functionality

Qt creator offers clickable symbols, auto-completion of the complete codebase and building and flashing firmware.

![](images/toolchain/qtcreator.png)

### Qt Creator on Linux

<aside class="note">
Linux users can just load the CMakeLists.txt in the root firmware folder via File -> Open File or Project -> Select the CMakeLists.txt file.
</aside>

After loading, the 'play' button can be configured to run the project by selecting 'custom executable' in the run target configuration and entering 'make' as executable and 'upload' as argument.

### Qt Creator on Windows

<aside class="todo">
Windows has not been tested with Qt creator yet.
</aside>

### Qt Creator on Mac OS

Before starting Qt Creator, the [project file](https://cmake.org/Wiki/CMake_Generator_Specific_Information#Code::Blocks_Generator) needs to be created:

<div class="host-code"></div>

```sh
cd ~/src/Firmware
mkdir build_creator
cd build_creator
cmake .. -G "CodeBlocks - Unix Makefiles"
```

That's it! Start Qt Creator, then complete the steps in the video below to set up the project to build.

{% youtube %}https://www.youtube.com/watch?v=0pa0gS30zNw&rel=0&vq=hd720{% endyoutube %}
