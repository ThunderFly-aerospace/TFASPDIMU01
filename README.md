# TFASPDIMU01 - sdp3x differental pressure sensor and IMU 9-axis unit

![.github/workflows/KiCad.yml](https://github.com/ThunderFly-aerospace/TFASPDIMU01/workflows/.github/workflows/KiCad.yml/badge.svg)

ThunderFly TFASPDIMU01 is SPI/I2C sensor board equipped with a differential pressure sensor (Senserion [SDP3x](https://www.sensirion.com/sdp3x/)) and 9-axis motion tracking sensor ([ICM-20948](https://invensense.tdk.com/products/motion-tracking/9-axis/icm-20948/)). Board is equipped with 7pin JST-GH connector. The sensor board is designed for multiple uses. It can be used as a self-adjusting anemometer [WINDGAUGE03](https://github.com/mlab-modules/WINDGAUGE03) or as an airspeed sensor for UAVs with optional function as the external magnetometer.

![TFASPDIMU01 PCB](doc/img/TFASPDIMU01_top_big.png)

TFASPDIMU is commercially available from [ThunderFly s.r.o.](https://www.thunderfly.cz/), write an email to info@thunderfly.cz or shop at [Tindie store](https://www.tindie.com/stores/thunderfly/).

## Specification
 * Type: Differential and 9-axis motion sensor board
 * Mass: 3 g
 * Size: 36 x 14 mm
 * Power: +5 V
 * Connection: 7pin JST-GH connector, custom pinout

**SDP3x**
 * Range: +/- 125/500 Pa (depending on exact sensor type)
 * Excellent accuracy and repeatability, even below one Pascal
 * No zero-point offset, no temperature drift
 * Calibrated and temperature compensated
 * Fast sampling time of 2kHz at 16 bit resolution
 * I2C address: 0x21 (d33)

 **ICM-20948**
 * 3-axis gyroscope, 3-axis accelerometer, 3-axis compass (magnetometer)
 * Onboard Digital Motion Processor (DMP)
 * On-Chip 16-bit ADCs and Programmable Filters
 * 7 MHz SPI or 400 kHz Fast Mode I²C
 * Digital temperature sensor
 * Default I2C address: 0x68 (0d104), can be changed to 0x69 (0d105) by moving the resistor R2->R1. 


## Example of uses

### WINDGUAGE01

Ground control station anemometer [WINDGAUGE03](https://github.com/mlab-modules/WINDGAUGE03)

### TFSLOT01 - UAV airspeed sensor

Our [TFSLOT](https://github.com/ThunderFly-aerospace/TFSLOT01) senzor is an airspeed sensor for use mainly on UAV. Due to 3D printed case it is possible to optimalize part according to the location of sensor on UAV and tune their characteristics. First use of this sensor was on our autogyro [TF-G2](https://github.com/ThunderFly-aerospace/TF-G2/).

![TFSLOT01 sensor](https://github.com/ThunderFly-aerospace/TFSLOT01/blob/TFSLOT01/doc/img/TFSLOT01A.jpg)

More details about this solution is available in the repository [TFSLOT01](https://github.com/ThunderFly-aerospace/TFSLOT01).

### TFPIPE01 - UAV airspeed sensor

Symmetric variant of TFSLOT sensor for different mounting options [TFPIPE01](https://github.com/ThunderFly-aerospace/TFPIPE01).

### TFVENTUFO - omnidirectional anemometer
This anemometer should also based on venturi effect. Thanks to an clever design, it will measure the wind speed from all directions (without knowing the direction).

### Angle of Attack sensor

In case of mounting on slip-ring bearing the sensor could sense air [AoA of the vehicle](https://en.wikipedia.org/wiki/Angle_of_attack).


## Hardware

![TFASPDIMU01 sensor](doc/img/TFASPDIMU01.jpg)

### Eletronic schema

Full schema is avialible in [PDF](/hw/sch_pcb/TFASPDIMU01.pdf)
![schema](/hw/cam/docs/TFASPDIMU01_schematic.svg)

### Hardware layout


** IMG - technical draft **


### Pinout
|Pin #| I2C | SPI  |
| --- |:---:|:----:|
| 1   | +5V | +5V  |
| 2   | SCL | SCK  |
| 3   | --  | MISO |
| 4   | SDA | MOSI |
| 5   | --  | CS   |
| 6   | INT | INT  |
| 7   | GND | GND  |
> Due to the possible wider use of the sensor, a standard pixhawk pinout is not used.


#### PixHawk autopilot cable


To increase the transmission quality, it is recommended to create pairs SDA,GND and SCL,+5V on the cable (as shown in image)

![I2C jstgh](doc/img/jstgh_i2c.jpg)

| TFASPDIMU01 Pin | Sigal | Pixhawk | Color |
| ---------------:|:-----:|:-------:|-------|
|   1             | +5V   |  1      | Red   |
|   2             | SCL   |  2      | Yellow|
|   4             | SDA   |  3      | Green |
|   7             | GND   |  4      | Black |
> Pixhawk pinout is listed according to the [Pixhawk connector standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf).

## Usage

### Python
For reading data from the sensor, we have prepared a python script in PyMLAB library that uses the pySMBus to readout data. It can be used directly from a computer with a corresponding converter (for example MLAB [USBI2C01A](https://wiki.mlab.cz/doku.php?id=cs:usbi2c)) or with one-board computers (Odroid, raspberry and similar) that have own smbus output.

#### Calibration vertification
Calibration can be verified by mounting of an anemometer to car roof and comparing it to speed obtained from GPS (gpsd). This needs to be done in windless weather.

### PX4
> We are now working on implementation of driver into PX4 stack.

Main usage of this sensor is as airspeed sensor. It can be also used as an external magnetometer and thermometer.

### Ardupilot
We are currently unable to implement the sensor in the Ardupilot flight stack. However, we will be happy to provide assistance with implementation. You can [contact us](https://www.thunderfly.cz/contact-us.html)

#### configuration
*TODO*
