# Driver Development

The PX4 codebase uses a lightweight, unified driver abstraction layer: [DriverFramework](https://github.com/px4/DriverFramework). New drivers for POSIX and [QuRT](https://en.wikipedia.org/wiki/Qualcomm_Hexagon) are written against this framework.

<aside class="todo">
Legacy drivers for NuttX are based on the [Device](https://github.com/PX4/Firmware/tree/master/src/drivers/device) framework and will be ported to DriverFramework.
</aside>

## Core Architecture

PX4 is a [reactive system](concept-architecture.md) and uses pub/sub to transport messages. File handles are not required or used for the core operation of the system. Two main APIs are used:

  * The publish / subscribe system which has a file, network or shared memory backend depending on the system PX4 runs on
  * The global device registry, which allows to enumerate devices and get/set their configuration. This can be as simple as a linked list or map to the file system.

## Bringing up a new Platform

### NuttX

  * The start script is located in [ROMFS/px4fmu_common](https://github.com/PX4/Firmware/tree/master/ROMFS/px4fmu_common)
  * The OS configuration is located in [nuttx-configs](https://github.com/PX4/Firmware/tree/master/nuttx-configs). The OS gets loaded as part of the application build.
  * The PX4 middleware configuration is located in [src/drivers/boards](https://github.com/PX4/Firmware/tree/master/src/drivers/boards). It contains bus and GPIO mappings and the board initialization code.
  * Drivers are located in [src/drivers](https://github.com/PX4/Firmware/tree/master/src/drivers)
  * Reference config: Running 'make px4fmu-v4_default' builds the FMUv4 config, which is the current NuttX reference configuration

### QuRT / Hexagon

  * The start script is located in [posix-configs/](https://github.com/PX4/Firmware/tree/master/posix-configs)
  * The OS configuration is part of the default Linux image (TODO: Provide location of LINUX IMAGE and flash instructions)
  * The PX4 middleware configuration is located in [src/drivers/boards](https://github.com/PX4/Firmware/tree/master/src/drivers/boards). TODO: ADD BUS CONFIG
  * Drivers are located in [DriverFramework](https://github.com/px4/DriverFramework)
  * Reference config: Running 'make qurt_eagle_release' builds the Snapdragon Flight reference config
