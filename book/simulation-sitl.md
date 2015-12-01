# Software in the Loop (SITL) Simulation

Software in the Loop Simulation runs the complete system on the host machine and simulates the autopilot. It connects via local network to the simulator. The setup looks like this:

```mermaid
graph LR;
  Simulator-->MAVLink;
  MAVLink-->SITL;
```

## Running SITL

After ensuring that the [simulation prerequisites](simulation-prerequisites.md) are installed on the system, just launch: The convenience make target will compile the POSIX host build and run the simulation.

<div class="host-code"></div>

```sh
make posix_sitl_default jmavsim
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

## Taking it to the Sky

And a window with the 3D view of the [jMAVSim](http://github.com/PX4/jMAVSim.git) simulator:

![](images/sim/jmavsim.png)

The system will print the home position once it finished intializing (`telem> home: 55.7533950, 37.6254270, -0.00`). You can bring it into the air by typing:

```sh
pxh> commander takeoff
```

<aside class="tip">
Joystick or thumb-joystick support is available through QGroundControl (QGC). To use manual input, put the system in a manual flight mode (e.g. POSCTL, position control). Enable the thumb joystick from the QGC preferences menu.
</aside>
