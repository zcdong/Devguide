# UAVCAN Firmware Upgrading

## Vectorcontrol ESCs (Pixhawk ESC 1.6 and S2740VC)

Download and build the ESC code:

<div class="host-code"></div>

```sh
git clone https://github.com/thiemar/vectorcontrol
cd vectorcontrol
BOARD=s2740vc_1_0 make && BOARD=px4esc_1_6 make
```

This will build the UAVCAN node firmware for both supported ESCs. The firmware images will be located at `firmware/org.pixhawk.px4esc-v1-1.0.00000000.uavcan.bin` and `firmware/com.thiemar.s2740vc-v1-1.0.00000000.uavcan.bin`.

Before updating firmware via UAVCAN, the Pixhawk ESC 1.6 requires the UAVCAN bootloader be flashed. To build the bootloader, run:

```sh
make clean && BOARD=px4esc_1_6 make -j8 
```

After building, the bootloader image is located at `firmware/bootloader.bin`, and can be flashed via an SWD adapter such as the ST-Link v2 or the BlackMagic Probe.

## Pixhawk ESC 1.4

Download the Pixhawk ESC 1.4 support branch of PX4ESC:

<div class="host-code"><div>

```sh
git clone https://github.com/thiemar/px4esc
cd px4esc
git checkout px4esc_1.4_update
cd firmware
make px4esc.image
```

The firmware image will be located at `firmware/build/org.pixhawk.px4esc-bldc-v1-1.0.00000000.uavcan.bin`.

Before updating firmware via UAVCAN, the Pixhawk ESC 1.4 requires the UAVCAN bootloader be flashed. The bootloader can be built as follows:

```sh
cd bootloader
make clean && make -j8
```

The bootloader image is located at `bootloader/firmware/bootloader.bin`, and can be flashed via an SWD adapter such as the ST-Link v2 or the BlackMagic Probe.

## Firmware installation

The UAVCAN node file names follow a naming convention which allows the Pixhawk to update all UAVCAN devices on the network, regardless of manufacturer. The firmware files generated in the steps above must therefore be copied to the correct locations on an SD card or the PX4 ROMFS in order for the devices to be updated.

The convention for firmware image names is:

  ```<node name>-<hw version major>.<hw version minor>-<git commit hash>.uavcan.bin```

However, due to space/path length/performance constraints, the UAVCAN firmware updater requires those filenames to be split and stored in a directory structure like the following:

  ```/fs/microsd/fw/<node name>/<hw version major>.<hw version minor>/<git commit hash>.bin```

The ROMFS-based updater follows that pattern, so you add the firmware in:

  ```/etc/uavcan/fw/<node name>/<hw version major>.<hw version minor>/<git commit hash>.bin```

The git commit hash is not validated so it can actually be anything.

## Placing the binaries in the PX4 ROMFS

The resulting finale file locations are:

  * S2740VC ESC: ```ROMFS/px4fmu_common/uavcan/fw/com.thiemar.s2740vc-v1/1.0/00000000.uavcan.bin```
  * Pixhawk ESC 1.6: ```ROMFS/px4fmu_common/uavcan/fw/org.pixhawk.px4esc-v1/1.0/00000000.uavcan.bin```
  * Pixhawk ESC 1.4: ```ROMFS/px4fmu_common/uavcan/fw/org.pixhawk.px4esc-bldc-v1/1.0/00000000.uavcan.bin```

Note that the ROMFS/px4fmu_common directory will be mounted to /etc on Pixhawk.
