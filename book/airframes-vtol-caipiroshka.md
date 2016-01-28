# TBS Caipiroshka

The Caipiroshka VTOL is a slightly modified TBS Caipirinha.

{% youtube %}https://www.youtube.com/watch?v=acG0aTuf3f8&vq=hd720{% endyoutube %}

## Parts List

  * TBS Caipirinha Wing ([Eflight store](http://www.eflight.ch/shop/USER_ARTIKEL_HANDLING_AUFRUF.php?von_suchresultat=true&Ziel_ID=19638&Kategorie_ID=110923))
  * Left and right 3D-printed motor mount ([design files](parts/motor_mounts.zip))
  * CW 8045 propeller ([Eflight store](http://www.eflight.ch/shop/USER_ARTIKEL_HANDLING_AUFRUF.php?von_suchresultat=true&Ziel_ID=19532&Kategorie_ID=288))
  * CCW 8045 propeller ([Eflight store](http://www.eflight.ch/shop/USER_ARTIKEL_HANDLING_AUFRUF.php?von_suchresultat=true&Ziel_ID=19533&Kategorie_ID=288))
  * 2x 1800 kV 120-180W motors
    * [Quanum MT2208 1800 kV](http://www.hobbyking.com/hobbyking/store/__67014__Quanum_MT_Series_2208_1800KV_Brushless_Multirotor_Motor_Built_by_DYS.html)
    * [ePower 2208](http://www.eflight.ch/pi/ePower-X-22081.html)
  * 2x 20-30S ESC
    * [Eflight store](http://www.eflight.ch/shop/USER_ARTIKEL_HANDLING_AUFRUF.php?von_suchresultat=true&Ziel_ID=19713&Kategorie_ID=36077)
  * BEC (3A, 5-5.3V)
  * 3S 2200 mA LiPo battery
    * Team Orion 3S 11.1V 50 C ([Brack store](https://www.brack.ch/team-orion-2200mah-11-1v-50c-308340))
  * [Pixracer autopilot board + power module](hardware-pixracer.md)
  * [Digital airspeed sensor](http://www.hobbyking.com/hobbyking/store/__62752__HKPilot_32_Digital_Air_Speed_Sensor_And_Pitot_Tube_Set.html)

<aside type="todo">
Update the mixer for Pixracer
</aside>

## Servo Connections

| Output | Actuator |
| -- | -- | -- |
| MAIN1 | 50 Hz | Left motor controller |
| MAIN2 | 50 Hz | Right motor controller |
| MAIN3 | 50 Hz | Empty |
| MAIN4 | 50 Hz | Empty |
| MAIN5 | 400 Hz | Left aileron servo |
| MAIN6 | 400 Hz | Right aileron servo |
