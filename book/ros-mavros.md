# MAVROS 
## Overview
The [mavros](http://wiki.ros.org/mavros#mavros.2BAC8-Plugins.sys_status) ros package enables MAVLink extendable communication between computers running ROS, MAVLink enabled autopilots, and MAVLink enabled GCS.  While MAVRos can be used to communicate with any MAVLink enabled autopilot this documentation will be in the context of enabling communication between the PX4 flight stack and a ROS enabled companion computer.

## Installation
### Binary installation (debian)

Since v0.5 that programs available in precompiled debian packages for x86 and amd64 (x86\_64).
Also v0.9+ exists in ARMv7 repo for Ubuntu armhf.
Just use `apt-get` for installation:
```sh
$ sudo apt-get install ros-indigo-mavros ros-indigo-mavros-extras
```

### Source installation

Note this installation assumes you have a catkin workspace located at `~/catkin_ws` If you don't create one with 
```sh
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws
$ catkin init
```
Use `wstool` utility for installation and catkin tool for build. If this is your first time using wstool you will need to initialize your source space with:
```sh
$ wstool init ~/catkin_ws/src
```
Now you are ready to do the build
```sh
$ sudo apt-get install python-catkin-tools
$ sudo apt-get install python-rosinstall-generator

    # get source (upstream - released)
$ rosinstall_generator --upstream mavros | tee /tmp/mavros.rosinstall
    # alternative: latest source
$ rosinstall_generator --upstream-development mavros | tee /tmp/mavros.rosinstall

    # workspace & deps
$ wstool merge -t src /tmp/mavros.rosinstall
$ wstool update -t src
$ rosdep install --from-paths src --ignore-src --rosdistro indigo -y

    # finally - build
$ catkin build
```

*Build error*. if you have an error with missing `mavlink_*_t` or `MAVLINK_MSGID_*` then you need fresh mavlink package.
You may update from [ros-shadow-fixed](http://packages.ros.org/ros-shadow-fixed/ubuntu/pool/main/r/ros-indigo-mavlink/) or build it from source (see next section).

*Important*. The current implementation of mavlink does not allow to select dialect in run-time,
so mavros package (and all plugin packages) have compile-time option `MAVLINK_DIALECT`, default is 'aurdupilotmega'.

If you want change dialect change workspace config:
```sh
$ catkin config --cmake-args -DMAVLINK_DIALECT=pixhawk
```

### Installing ros-\*-mavlink from source

In ROS Indigo there new tool named `catkin`. It is more powerful and more comfortable that `catkin_make`.
With that tool you may place mavlink package in your mavros workspace.
```sh
$ cd ~/catkin_ws/src # your mavros workspace
$ rosinstall_generator mavlink | tee /tmp/mavlink.rosinstall
$ wstool merge /tmp/mavlink.rosinstall
$ wstool up -j4
$ catkin clean --all
$ catkin build # also will build mavros
```

### Building ros-\*-mavlink debian package

You could build debian package by pulling right bloom branch from [mavlink-gbp-release](https://github.com/mavlink/mavlink-gbp-release)
(common naming: `debian/<rosdistro>/<osdistro>/<package>`) using `dh binary`.
```sh
$ cd /tmp
$ git clone https://github.com/mavlink/mavlink-gbp-release.git -b debian/indigo/trusty/mavlink
$ cd mavlink-gbp-release
$ fakeroot dh binary
    # deb will be in /tmp
```
