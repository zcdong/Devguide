# VTOL Testing

How-to test that the VTOL functions properly, main focus are transitions:

  * On the bench
  * In flight

## General notes on transitions

There are currently 3 ways of commanding the VTOL to transition:

  * RC switch (2 pos, aux1)
  * MAVLink command (MAV_CMD_DO_VTOL_TRANSITION)
  * Transition during mission (MAV_CMD_DO_VTOL_TRANSITION internally)

When a transition is commanded (by either of the methods above), the VTOL enters the transition phase.
If the VTOL receives a new transition command back to the old state during an ongoing transition it will switch back instantly.
This is a safety feature to exit to abort the transition when necessary. After the transition has been completed,
the VTOL will be in the new state and a commanded transition into the reverse direction will take place normally.

<aside class="warn">
Make sure the AUX1 channel is assigned to an RC switch and airspeed is working properly.
</aside>

<aside class="todo">
TODO: support new VTOL MAVLink commands for direct VTOL takeoff/land
</aside>

## On the bench

<aside class="warn">
Remove all props! To test transition functionality properly, the vehicle needs to be armed.
</aside>

By default, starting in multirotor mode:

  * arm the vehicle
  * check that motors are running in multirotor configuration (rudders/elevons should not move on roll/pitch/yaw inputs)
  * toggle transition switch
  * (if applicable) wait on step 1 of the transition phase to complete
  * blow into pito tube to simulate airspeed
  * (if applicable) step 2 of the transition phase will be executed
  * check that motors are running in fixed-wing configuration (roll/pitch/yaw inputs should control rudders/elevons)
  * toggle transition switch
  * observe back transition
  * check that motors are running in multirotor configuration (rudders/elevons should not move on roll/pitch/yaw inputs)

## In flight

<aside class="warn">
Before testing transitions in flight, make sure the VTOL flies stable in multirotor mode.
In general, if something doesn't go as planned, transition to multirotor mode and let it recover (it does a good job when it's properly
tuned).
</aside>

### Manual test

### Automatic test (mission, commanded)

Commanded transitions only work in auto (mission) or offboard flight-mode.
Make sure you are confident to operate the auto/offboard and transition switch in flight.

Switching to manual will reactivate the transition switch. For example: if you switch out of auto/offboard when in automatic
fixed-wing flight and the transition switch is currently in multirotor position it will transition to multirotor right away.

The following procedure can be used to test a mission with transition:

  * upload mission
  * takeoff in multirotor mode and climb to mission height
  * enable mission with switch
  * observe transition to fixed-wing flight
  * enjoy flight
  * observe transition back to multirotor mode
  * disable mission
  * land manually
  
During flight, the manual transition switch stays in multirotor position. If something doesn't go as planned,
switch to manual and it will recover in multirotor mode.

The mission should contain at least:
  * position waypoint near takeoff location
  * position waypoint in the direction of the planned fixed-wing flight route
  * transition waypoint (to plane mode)
  * position waypoint further away (at least as far away as the transition needs)
  * position waypoint to fly back (a bit before takeoff location so back transition takes some distance)
  * transition waypoint (to hover mode)
  * position waypoint near takeoff location

## Relevant parameters

<aside class="todo">
TODO: params for all 3 types
</aside>

