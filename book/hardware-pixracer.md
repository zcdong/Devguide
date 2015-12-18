# Pixracer

The Pixhawk XRacer board family is optimized for small racing quads and planes. In contrast to the [Pixfalcon](hardware-pixfalcon.md) it has in-built Wifi, new sensors, convenient full servo headers, CAN and supports 2M flash.

![](images/hardware/hardware-pixracer.jpg)

## Quick Summary

<aside class="tip">
The main hardware documentation is here: https://pixhawk.org/modules/pixracer
</aside>

  * Standard FPV form factor: 40x40 mm with standard 32.5 mm hole pattern
  * Wifi telemetry and software upgrade
  * Invensense ICM-20608 Accel / Gyro (4 KHz) / MPU9250 Accel / Gyro / Mag (4 KHz)
  * HMC5983 magnetometer with temperature compensation
  * Measurement Specialties MS5611 barometer
  * JST GH connectors
  * microSD (logging)
  * S.BUS / Spektrum / SUMD / PPM input
  * FrSky telemetry port
  * OneShot PWM out (configurable)
  * Optional: Safety switch and buzzer
  * Availability:
    * [AUAV Pixracer](http://www.auav.co/product-p/xr-v1.htm)


## Kit

The Pixracer is designed to use a separate avionics power supply. This is necessary to avoid current surges from motors or ESCs to flow back to the flight controller and disturb its delicate sensors.

  * Power module (with voltage and current sensing)
  * I2C splitter (supporting AUAV, Hobbyking and 3DR peripherals)
  * Cable kit for all common peripherals

## Wifi (no USB required)

One of the main features of the board is its ability to use Wifi for flashing new firmware, system setup and in-flight telemetry. This frees it of the need of any desktop system.

<aside class="todo">
Setup and telemetry are already available, firmware upgrade is already supported by the default bootloader but not yet enabled
</aside>

  * [ESP8266 Documentation and Flash Instructions](https://pixhawk.org/peripherals/8266)
  * [Custom ESP8266 MAVLink firmware](https://github.com/dogmaphobic/mavesp8266)
