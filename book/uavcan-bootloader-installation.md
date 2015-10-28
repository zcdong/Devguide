# UAVCAN Bootloader Installation

***UAVCAN devices typically ship with a bootloader pre-installed. Do not follow the instructions in this section unless you are developing UAVCAN devices.***

## Overview

The PX4 project includes a standard UAVCAN bootloader for STM32 devices.

The bootloader occupies the first 8–16 KB of flash, and is the first code executed on power-up. Typically, the bootloader performs low-level device initialization, automatically determines the CAN bus baud rate, acts as a UAVCAN dynamic node ID client to obtain a unique node ID, and waits for confirmation from the flight controller before proceeding with application boot.

This process ensures that a UAVCAN device can recover from invalid or corrupted application firmware without user intervention, and also permits automatic firmware updates.

## Prerequisites

Installing or updating the UAVCAN bootloader requires:

* An SWD or JTAG interface (depending on device), for example the [BlackMagic Probe](http://www.blacksphere.co.nz/main/blackmagic) or the [ST-Link v2](http://www.st.com/internet/evalboard/product/251168.jsp);
* An adapter cable to connect your SWD or JTAG interface to the UAVCAN device's debugging port;
* A [supported ARM toolchain](starting-installing.md).

## Device Preparation

If you are unable to connect to your device using the instructions below, it's possible that firmware already on the device has disabled the MCU's debug pins. To recover from this, you will need to connect your interface's NRST or nSRST pin (pin 15 on the standard ARM 20-pin connector) to your MCU's NRST pin. Obtain your device schematics and PCB layout or contact the manufacturer for details.

## Installation

After compiling or obtaining a bootloader image for your device (refer to device documentation for details), the bootloader must be copied to the beginning of the device's flash memory.

The process for doing this depends on the SWD or JTAG interface used.

## BlackMagic Probe

Ensure your BlackMagic Probe [firmware is up to date](https://github.com/blacksphere/blackmagic/wiki/Hacking).

Connect the probe to your UAVCAN device, and connect the probe to your computer.

Identify the probe's device name. This will typically be `/dev/ttyACM<x>` or `/dev/ttyUSB<x>`.

Power up your UAVCAN device, and run:

<div class="host-code"></div>

```sh
arm-none-eabi-gdb /path/to/your/bootloader/image.elf
```

At the `gdb` prompt, run:

<div class="host-code"></div>

```gdb
target extended /dev/ttyACM0
monitor connect_srst enable
monitor swdp_scan
attach 1
set mem inaccessible-by-default off
load
run
```

If `monitor swdp_scan` returns an error, ensure your wiring is correct, and that you have an up-to-date version of the BlackMagic firmware.

## ST-Link v2

Ensure you have a recent version—at least 0.9.0—of [OpenOCD](http://openocd.org).

Connect the ST-Link to your UAVCAN device, and connect the ST-Link to your computer.

Power up your UAVCAN device, and run:

<div class="host-code"></div>

```sh
openocd -f /path/to/your/openocd.cfg &
arm-none-eabi-gdb /path/to/your/bootloader/image.elf
```

At the `gdb` prompt, run:

<div class="host-code"></div>

```gdb
target extended-remote localhost:3333
monitor reset halt
set mem inaccessible-by-default off
load
run
```
