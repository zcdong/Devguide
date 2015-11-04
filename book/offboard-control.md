<aside class="caution">
Offboard control is dangerous. It is the responsibility of the developer to ensure adequate preparation, testing and safety precautions are taken before offboard flights.
</aside>

# Offboard Control

The idea behind off-board control is to be able to control the px4 flight stack using software running outside of the autopilot. This is done through the Mavlink protocol, specifically the [SET_POSITION_TARGET_LOCAL_NED](https://pixhawk.ethz.ch/mavlink/#SET_POSITION_TARGET_LOCAL_NED) and the [SET_ATTITUDE_TARGET](https://pixhawk.ethz.ch/mavlink/#SET_ATTITUDE_TARGET) messages.
