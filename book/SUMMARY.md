# Summary

This is the summary of the PX4 dev guide.

* Getting Started
  * [Initial Configuration](starting-initial-config.md)
  * [Toolchain Installation](starting-installing.md)
    * [Mac OS](starting-installing-mac.md)
    * [Linux](starting-installing-linux.md)
      * [Advanced Linux](starting-installing-linux-boutique.md)
    * [Windows](starting-installing-windows.md)
  * [Building the Code](starting-building.md)
  * [Contributing & Dev Call](starting-contributing.md)
* Concepts
  * [Flight Modes / Operation](concept-flight-modes.md)
  * [Architectural Overview](concept-architecture.md)
  * [Flight Stack](concept-flight-stack.md)
  * [Middleware](concept-middleware.md)
  * [Mixing and Actuators](concept-mixing.md)
* Ground Control
  * [Introduction](qgroundcontrol-intro.md)
* Simulation
  * [Prerequisites](simulation-prerequisites.md)
  * [Light Simulation](simulation-sitl.md)
    * [Debugging](simulation-debugging.md)
  * [Gazebo Simulation](simulation-gazebo.md)
    * [Octomap](simulation-gazebo-octomap.md)
* Autopilot Hardware
  * [Snapdragon Flight](hardware-snapdragon.md)
  * [Pixhawk](hardware-pixhawk.md)
  * [Pixfalcon](hardware-pixfalcon.md)
  * [Pixracer](hardware-pixracer.md)
* Airframes
  * [Unified Codebase](airframes-architecture.md)
  * [Adding a new Airframe](airframes-adding-a-new-frame.md)
  * [Multicopters](airframes-multicopter.md)
    * [Motor Map](airframes-motor-map.md)
    * [QAV 250 Racer](airframes-multicopter-qav250.md)
    * [Matrice 100](airframes-multicopter-matrice100.md)
  * [Planes](airframes-plane.md)
    * [Wing Wing Z-84](airframes-plane-wing-z-84.md)
  * [VTOL](airframes-vtol.md)
    * [TBS Caipiroshka](airframes-vtol-caipiroshka.md)
  * [Boats, Submarines, Blimps, Rovers](airframes-experimental.md)
* Robotics using ROS
  * [ROS Installation on RPi 2](ros-raspberrypi-installation.md)
  * [MAVROS (MAVLink on ROS)](ros-mavros-installation.md)
  * [Offboard Control from Linux](offboard-control.md)
  * [MAVROS offboard example](ros-mavros-offboard.md)
  * [External Position Estimation](external-position.md)
* Sensor and Actuator Buses
  * [I2C Bus](i2c-intro.md)
  * [UAVCAN Bus](uavcan-intro.md)
    * [UAVCAN Bootloader](uavcan-bootloader-installation.md)
    * [UAVCAN Firmware Upgrades](uavcan-node-firmware.md)
    * [UAVCAN Configuration](uavcan-node-enumeration.md)
  * [PWM / GPIO](pwm-gpio-intro.md)
  * [UART](uart-intro.md)
* Advanced Topics
  * [System Console](advanced-system-console.md)
  * [System Boot](advanced-system-startup.md)
  * [uORB Messaging](advanced-uorb.md)
  * [Licenses](advanced-licenses.md)
