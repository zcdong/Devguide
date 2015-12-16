# Snapdragon Flight Autopilot

The Snapdragon Flight platform is a high-end autopilot / onboard computer which runs the PX4 Flight Stack on the DSP on the QuRT real time operating system using the [DSPAL API](https://github.com/ATLFlight/dspal) for POSIX compatibility. In comparison to [Pixhawk](hardware-pixhawk.md) it adds a camera and WiFi and high-end processing power, and different IO.

More information about the Snapdragon Flight platform is at [Snapdragon-Flight-Details](https://www.intrinsyc.com/qualcomm-snapdragon-flight-details/)

![](images/hardware/hardware-snapdragon.jpg)

## Quick Summary

  * System-on-Chip: [Snapdragon 801](https://www.qualcomm.com/products/snapdragon/processors/801)
    * CPU: Quad-core 2.26 GHz Krait
    * DSP: Hexagon DSP (QDSP6 V5A) – 801 MHz+256KL2 (running the flight code)
    * GPU: Qualcomm® Adreno™ 330 GPU
    * RAM: 2GB LPDDR3 PoP @931 MHz
  * Storage: 32GB eMMC Flash
  * Video: Sony IMX135 on Liteon Module 12P1BAD11
    * 4k@30fps 3840×2160 video capture to SD card with H.264 @ 100Mbits (1080p/60 with parallel FPV), 720p FPV
  * Optic Flow: 640x480 Omnivision OV7251 on Sunny Module MD102A-200
  * Wifi: Qualcomm® VIVE™ 1-stream 802.11n/ac with MU-MIMO † Integrated digital core
  * BT/WiFi: BT 4.0 and 2G/5G WiFi via QCA6234
    * 802.11n, 2×2 MIMO with 2 uCOAX connectors on-board for connection to external antenna
  * GPS: Telit Jupiter SE868 V2 module
    * uCOAX connector on-board for connection to external GPS patch antenna 
    * CSR SiRFstarV @ 5Hz via UART
  * MPU: Invensense MPU-9250 9-Axis Sensor, 3x3mm QFN
  * Baro: Bosch BMP280 barometric pressure sensor
  * Power: 5VDC via external 2S-6S battery regulated down to 5V via APM adapter
  * Availability: [Intrinsyc Store](http://shop.intrinsyc.com/products/snapdragon-flight-dev-kit)

## Connectivity

  * One USB 3.0 OTG port (micro-A/B)
  * Micro SD card slot
  * Gimbal connector (PWB/GND/BLSP)
  * ESC connector (2W UART)
  * I2C
  * 60-pin high speed Samtec QSH-030-01-L-D-A-K expansion connector
  * 2x BLSP ([BAM Low Speed Peripheral](http://www.inforcecomputing.com/public_docs/BLSPs_on_Inforce_6540_6501_Snapdragon_805.pdf))

## Dimensions

![](images/hardware/hardware-snapdragon-dimensions.png)

