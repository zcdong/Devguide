# FAKE GPS
This page shows you how to use mocap data to fake gps. 
The tutorial setup looks as follows:
There is a "VICON computer" which has the required software installed + [ROS](http://www.ros.org/) + [vicon_bridge](https://github.com/ethz-asl/vicon_bridge) and sends this data over network to "your Computer".
On "your computer" you should have ROS + MAVROS installed. In MAVROS there is a script which simulates gps data out of mocap data.
"Your computer" then sends the data over 3DR radiometry to the pixhawk.
*NOTE*: of course the "VICON computer" and "your computer" can be the same.

## Prerequisites
* MOCAP system (in this example, VICON is used)
* Computer with ROS, MAVROS and Vicon_bridge
* 3DR radiometry set

## Procedure
### Step 1
Make sure "your computer" is in the same network as the "VICON computer" (maybe you need a wireless adapter).
Create two files on the "VICON computer": "launch_fake_gps.sh" and "launch_fake_gps_distorted.sh" 

Add the following two lines to the "launch_fake_gps.sh" file and replace xxx.xxx.x.xxx with the IP adress of "your computer" (you can get the IP adress by typing "ifconfig" in the terminal).
```sh
export ROS_MASTER_URI=http://xxx.xxx.x.xxx:11311
roslaunch vicon_bridge vicon.launch $@
```

Next, add the following two lines to the "launch_fake_gps_distorted.sh" file and replace xxx.xxx.x.xxx with the IP adress of "your computer".
```sh
export ROS_MASTER_URI=http://xxx.xxx.x.xxx:11311
rosrun vicon_bridge tf_distort $@
```

### Step 2
Run
```sh
$ roscore
```
on "your computer".


### Step 3
Run
```sh
$ sh launch_fake_gps.sh
```
and
```sh
$ sh launch_fake_gps_distorted.sh
```
in two different terminals on the "VICON computer" in the directory where you created the two files.


### Step 4
On "your computer" run
```sh
$ rosrun rqt_reconfigure rqt_reconfigure
```
A new window should open where you can select "tf_distort". With this tool you can edit the parameters to distort the MOCAP data.

To simulate GPS we use:
* publish rate = 5.0Hz
* tf_frame_in = vicon/yourModelName/yourModelName (e.g. vicon/DJI_450/DJI_450)
* delay = 200ms
* sigma_xy = 0.05
* sigma_z = 0.05


### Step 5
Connect your pixhawk in QGroundControl. Go to PARAMETERS -> System and change SYS_COMPANION to 257600 (enables magic mode;)).

Next, go to PARAMETERS -> MAVLink and change MAV_USEHILGPS to 1 (enable HIL GPS).

Now, go to PARAMETERS -> Attitude Q estimator and change and change ATT_EXT_HDG_M to 2 (use heading from motion capture).

*NOTE*: if you can't find the above stated parameters, check PARAMETERS -> default Group


### Step 6
Next, open "mocap_fake_gps.cpp". It should be at: yourCatkinWS/src/mavros/mavros_extras/src/plugins/mocap_fake_gps.cpp

Replace the subscription 
```sh
mocap_tf_sub = mp_nh.subscribe("/vicon/DJI_450/DJI_450_drop", 1, &MocapPoseEstimatePlugin::mocap_tf_cb, this);
```
