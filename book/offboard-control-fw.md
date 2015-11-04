# Offboard Control Firmware Setup
There are two things you want to setup on the firmware side before starting offboard development.

## 1. Map an RC switch to offboard mode activation
To do this, load up the parameters in qGroundcontrol and look for the RC_MAP_OFFB_SW parameter to which you can assign the RC channel you want to use to activate offboard mode. It can be useful to map things in such a way that when you fall out of offboard mode you go into position control.

Although this step isn't mandatory since you can activate offboard mode using a MAVLink message. We consider this method much safer.

## 2. Enable the companion computer interface
Look for the [SYS_COMPANION](https://pixhawk.org/firmware/parameters#system) parameter and set it to either 921600 (Recommended) or 57600. This parameter will activate a MAVLink stream on the Telem2 port with data streams specific to onboard mode with the appropriate baud rate (921600 8N1 or 57600 8N1). 

For more information on these data streams, look for "MAVLINK_MODE_ONBOARD" in the [source code](https://github.com/PX4/Firmware/blob/master/src/modules/mavlink/mavlink_main.cpp).