# Development Environment on Linux

We have standardized on Debian / Ubuntu LTS as the supported Linux distribution, but [boutique distribution instructions](starting-installing-linux-boutique.md) are available for Cent OS and Arch Linux.

## Installation

Update the package list and install the following dependencies for all PX4 build targets. PX4 supports three main families:

  * NuttX based hardware: [Pixhawk](hardware-pixhawk.md), [Pixfalcon](hardware-pixfalcon.md)
  * Snapdragon Flight hardware: [Snapdragon](hardware-snapdragon.md)
  * Host simulation: [jMAVSim SITL](simulation-sitl.md) and [Gazebo SITL](simulation-gazebo.md)

<aside class="note">
Install the [Ninja Build System](starting-installing-linux-boutique.md#ninja-build-system) for faster build times than with Make. It will be automatically selected if installed.
</aside>

<div class="host-code"></div>

```sh
sudo add-apt-repository ppa:george-edison55/cmake-3.x -y
sudo apt-get update
sudo apt-get install python-argparse git-core wget zip \
    python-empy qtcreator cmake build-essential -y
```

### NuttX based hardware

Ubuntu comes with a serial modem manager which interferes heavily with any robotics related use of a serial port (or USB serial). It can deinstalled without side effects:

<div class="host-code"></div>

```sh
sudo apt-get remove modemmanager
```

Update the package list and install the following dependencies. Packages with specified versions should be installed with this particular package version.

<div class="host-code"></div>

```sh
sudo add-apt-repository ppa:terry.guo/gcc-arm-embedded -y
sudo apt-get update
sudo apt-get install python-serial openocd \
    flex bison libncurses5-dev autoconf texinfo build-essential \
    libftdi-dev libtool zlib1g-dev genromfs \
    python-empy
```

This guide generally refers to the specific latest GCC version tested. Use the package version tag for current Ubuntu versions:

```sh
sudo apt-get install gcc-arm-none-eabi=4.8.3-18ubuntu2+12 -y
```

For older releases, e.g. Ubuntu 14.04 (Trusty) and 14.10, leave the version tag out:

```sh
sudo apt-get install gcc-arm-none-eabi -y
```


### Snapdragon Flight

Developers working on Snapdragon Flight should download the Hexagon Linux toolchain and execute the commands below. The installation guide will come up, leave everything at default by just continuing to press enter.

<div class="host-code"></div>

```sh
sudo apt-get install gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf -y
tar xf Hexagon.LNX.7.2\ Installer-07210.1.tar
chmod u+x Hexagon.LLVM_linux_installer_7.2.10.bin
./Hexagon.LLVM_linux_installer_7.2.10.bin
```

After this the tools will have been installed to '~/Qualcomm/HEXAGON_Tools/7.2.10'. Add this to your path variable:

<div class="host-code"></div>

```sh
export PATH="$PATH:$HOME/Qualcomm/HEXAGON_Tools/7.2.10/Tools/bin/"
export HEXAGON_TOOLS_ROOT="$HOME/Qualcomm/HEXAGON_Tools/7.2.10/Tools"
```

Load the new configuration:

<div class="host-code"></div>

```sh
source ~/.bashrc
```

### Simulation

The default toolchain for simulation is CLANG 3.5.

<div class="host-code"></div>

```sh
sudo apt-get install -y clang-3.5 lldb-3.5

```

## Permission Setup

<aside class="note">
Never ever fix permission problems by using 'sudo'. It will create more permission problems in the process and require a system reinstallation to fix them.
</aside>

The user needs to be added to the group "dialout":

<div class="host-code"></div>

```sh
sudo usermod -a -G dialout $USER
```

Now continue to run the [first build](starting-building.md)!
