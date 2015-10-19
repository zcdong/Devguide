# Development Environment Installation on Linux

We have standardized on Debian / Ubuntu LTS as the supported Linux distribution, but [boutique distribution instructions](starting-installing-linux-boutique.md) are available for Cent OS and Arch Linux.

## Installation

Update the package list and install the following dependencies:

<div class="host-code"></div>
```sh
sudo apt-get update
sudo apt-get install python-serial python-argparse openocd \
    flex bison libncurses5-dev autoconf texinfo build-essential \
    libftdi-dev libtool zlib1g-dev genromfs git-core wget zip \
    python-empy
```

<aside class="note">
If using Debian, run this command:
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

The user needs to be added to the group "dialout":

<div class="host-code"></div>
```sh
sudo usermod -a -G dialout $USER
```

Now continue to run the [first build](starting-building.md)!
