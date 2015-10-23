# Development Environment Installation on Linux

We have standardized on Debian / Ubuntu LTS as the supported Linux distribution, but [boutique distribution instructions](starting-installing-linux-boutique.md) are available for Cent OS and Arch Linux.

## Installation

### STM32 based hardware

Update the package list and install the following dependencies:

<div class="host-code"></div>

```sh
sudo apt-get update
sudo apt-get install python-serial python-argparse openocd \
    flex bison libncurses5-dev autoconf texinfo build-essential \
    libftdi-dev libtool zlib1g-dev genromfs git-core wget zip \
    python-empy cmake qtcreator
```

Toolchain installation: Generally installing from this ARM-maintained PPA is fine, however, we recommend for a production system to use the last tested toolchain, which is documented at the bottom of this page.

<div class="host-code"></div>

```sh
sudo add-apt-repository ppa:terry.guo/gcc-arm-embedded
sudo apt-get update
sudo apt-get install gcc-arm-none-eabi
```
<aside class="note">
The current recommended GCC version is 4.8.4 and can be installed manually for the local user by running the script below.
</aside>

```sh
pushd .
cd ~
wget https://launchpadlibrarian.net/186124160/gcc-arm-none-eabi-4_8-2014q3-20140805-linux.tar.bz2
tar -jxf gcc-arm-none-eabi-4_8-2014q3-20140805-linux.tar.bz2
exportline="export PATH=$HOME/gcc-arm-none-eabi-4_8-2014q3/bin:\$PATH"
if grep -Fxq "$exportline" ~/.profile; then echo nothing to do ; else echo $exportline >> ~/.profile; fi
. ~/.profile
popd
```


<aside class="note">
If using Debian Linux, run this command:
</aside>

<div class="host-code"></div>

```sh
sudo dpkg --add-architecture i386
sudo apt-get update
```

Install the 32 bit support libraries (if running already on 32 bit this might fail and can be skipped):

<div class="host-code"></div>

```sh
sudo apt-get install libc6:i386 libgcc1:i386 gcc-4.6-base:i386 libstdc++5:i386 libstdc++6:i386
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

### Snapdragon Flight

Developers working on Snapdragon Flight should download the Hexagon Linux toolchain and execute the commands below. The installation guide will come up, leave everything at default by just continuing to press enter.

<div class="host-code"></div>

```sh
sudo apt-get install gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf
tar xf Hexagon.LNX.7.2\ Installer-07210.1.tar
chmod u+x Hexagon.LLVM_linux_installer_7.2.10.bin
./Hexagon.LLVM_linux_installer_7.2.10.bin
```

After this the tools will have been installed to '~/Qualcomm/HEXAGON_Tools/7.2.10'. Add this to your path variable:

<div class="host-code"></div>

```sh
export PATH="$PATH:$HOME/Qualcomm/HEXAGON_Tools/7.2.10/Tools/bin/"
```

Load the new configuration:

<div class="host-code"></div>

```sh
source ~/.bashrc
```

### Simulation

The default toolchain for simulation is CLANG.

<div class="host-code"></div>

```sh


```

Now continue to run the [first build](starting-building.md)!
