# Interfacing the Simulation to ROS

The simulated autopilot starts a second MAVLink interface on port 14557. Connecting MAVROS to this port allows to receive all data the vehicle would expose if in real flight.

## Launching MAVROS

If an interface to ROS is wanted, the already running secondary MAVLink instance can be connected to ROS via [mavros](ros-mavros-offboard.md). To connect to a specific IP (`fcu_url` is the IP / port of SITL), use a URL in this form:

<div class="host-code"></div>

```sh
roslaunch mavros px4.launch fcu_url:="udp://:14540@192.168.1.36:14557"
```

To connect to localhost, use this URL:

<div class="host-code"></div>

```sh
roslaunch mavros px4.launch fcu_url:="udp://:14540@127.0.0.1:14557"
```
