# UAVCAN Firmware Upgrading

## Vectorcontrol ESC Codebase (Pixhawk ESC 1.6 and S2740VC)

Download the ESC code:

<div class="host-code"></div>

```sh
git clone https://github.com/thiemar/vectorcontrol
cd vectorcontrol
```

### Flashing the UAVCAN Bootloader

Before updating firmware via UAVCAN, the Pixhawk ESC 1.6 requires the UAVCAN bootloader be flashed. To build the bootloader, run:

<div class="host-code"></div>

```sh
make clean && BOARD=px4esc_1_6 make -j8
```

After building, the bootloader image is located at `firmware/px4esc_1_6-bootloader.bin`, and the OpenOCD configuration is located at `openocd_px4esc_1_6.cfg`. Follow [these instructions](uavcan-bootloader-installation.md) to install the bootloader on the ESC.

### Compiling the Main Binary

<div class="host-code"></div>

```sh
BOARD=s2740vc_1_0 make && BOARD=px4esc_1_6 make
```

This will build the UAVCAN node firmware for both supported ESCs. The firmware images will be located at `firmware/com.thiemar.s2740vc-v1-1.0.00000000.bin` and `firmware/org.pixhawk.px4esc-v1-1.0.00000000.bin`.

## PX4 ESC Codebase (Pixhawk ESC 1.4)

Download the Pixhawk ESC 1.4 support branch of PX4ESC:

<div class="host-code"></div>

```sh
git clone https://github.com/thiemar/px4esc
cd px4esc
git checkout px4esc_1.4_update
```

### Flashing the UAVCAN Bootloader

Before updating firmware via UAVCAN, the Pixhawk ESC 1.4 requires the UAVCAN bootloader be flashed. The bootloader can be built as follows:

<div class="host-code"></div>

```sh
cd bootloader
make clean && make -j8
cd ..
```

The bootloader image is located at `bootloader/firmware/bootloader.bin`, and the OpenOCD configuration is located at `openocd.cfg`. Follow [these instructions](uavcan-bootloader-installation.md) to install the bootloader on the ESC.

### Compiling the Main Binary

<div class="host-code"></div>

```sh
cd firmware
make px4esc.image
```
The firmware image will be located at `firmware/build/org.pixhawk.px4esc-bldc-v1-1.0.<xxxxxxxx>.bin`, where `<xxxxxxxx>` is an arbitrary sequence of numbers and letters.

## Zubax GNSS

Please refer to the [project page](https://github.com/Zubax/zubax_gnss) to learn how to build and flash the firmware.
Zubax GNSS comes with a UAVCAN-capable bootloader, so its firmware can be updated in a uniform fashion via UAVCAN as described below.

## Firmware Installation on the Autopilot

The UAVCAN node file names follow a naming convention which allows the Pixhawk to update all UAVCAN devices on the network, regardless of manufacturer. The firmware files generated in the steps above must therefore be copied to the correct locations on an SD card or the PX4 ROMFS in order for the devices to be updated.

The convention for firmware image names is:

  ```<node name>-<hw version major>.<hw version minor>-<version hash>.bin```

However, due to space/performance constraints, the UAVCAN firmware updater requires those filenames to be split and stored in a directory structure like the following:

  ```/fs/microsd/fw/<node name>/<hw version major>.<hw version minor>/<version hash>.bin```

The ROMFS-based updater follows that pattern, so you add the firmware in:

  ```/etc/uavcan/fw/<node name>/<hw version major>.<hw version minor>/<version hash>.bin```

## Placing the binaries in the PX4 ROMFS

The resulting finale file locations are:

  * S2740VC ESC: `ROMFS/px4fmu_common/uavcan/fw/com.thiemar.s2740vc-v1/1.0/<xxxxxxxx>.bin`
  * Pixhawk ESC 1.6: `ROMFS/px4fmu_common/uavcan/fw/org.pixhawk.px4esc-v1/1.0/<xxxxxxxx>.bin`
  * Pixhawk ESC 1.4: `ROMFS/px4fmu_common/uavcan/fw/org.pixhawk.px4esc-bldc-v1/1.0/<xxxxxxxx>.bin`
  * Zubax GNSS v1: `ROMFS/px4fmu_common/uavcan/fw/com.zubax.gnss/1.0/<xxxxxxxx>.bin`
  * Zubax GNSS v2: `ROMFS/px4fmu_common/uavcan/fw/com.zubax.gnss/2.0/<xxxxxxxx>.bin`

(In all the above, `<xxxxxxxx>` is an arbitrary sequence of numbers and letters.)

Note that the ROMFS/px4fmu_common directory will be mounted to /etc on Pixhawk.

### Starting the Firmware Upgrade process

<aside class="note">
When using the [PX4 Flight Stack](concept-flight-stack.md), set the UAVCAN_ENABLE parameter to '3' in the QGroundControl parameter editor and *power cycle* the board to enable CAN motor outputs. Set it to '2' to enable CAN firmware upgrades, but leave motor outputs on PWM.
</aside>

Alternatively UAVCAN firmware upgrading can be started manually on NSH via:

```sh
uavcan start
uavcan start fw
```
