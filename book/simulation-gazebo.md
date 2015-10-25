# Gazebo Simulation

[Gazebo](http://gazebosim.org) is a 3D simulation environment for autonomous robots. It can be used with [ROS as complete robotics simulation suite](https://pixhawk.org/dev/ros/sitl) or standalone, and this guide covers the simpler to set up standalone operation.

## Installation

The installation requires to install Gazebo and our simulation plugin.

Follow the instruction in the [sitl_gazebo documentation](https://github.com/px4/sitl_gazebo) to build.

## Running the Simulation

Run the PX4 SITL with the Iris configuration in the Firmware directory:

<div class="host-code"></div>

```sh
cd ~/src/Firmware
make posix_sitl_default gazebo
```

This will bring up the PX4 shell:

```sh
[init] shell id: 140735313310464
[init] task name: mainapp

______  __   __    ___ 
| ___ \ \ \ / /   /   |
| |_/ /  \ V /   / /| |
|  __/   /   \  / /_| |
| |     / /^\ \ \___  |
\_|     \/   \/     |_/

Ready to fly.


pxh>
```

<aside class="note">
Right-clicking the quadrotor model allows to enable follow mode from the context menu, which is handy to keep it in view.
</aside>

![](images/sim/gazebo.png)
