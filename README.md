# TFASPD01 - sdp3x differental pressure sensor

ThunderFly TFASPD01 is SPI/I2C sensor board equipped with a differential pressure sensor (Senserion [SDP3x]()) and 9-axis motion tracking sensor ([ICM-20948]()). Board is equipted with 7pin JST-GH connector. The sensor board is designed for multiple uses. It can be used as a self-adjusting anemometer (TFASPD01A)[../README.md] or as an airspeed sensor for UAVs with external magnetometer. 

** IMG PCB **

## WINDGUAGE01A

## UAV integration
Our 'Venturi self' (our woriking title :) is airspeed sensor for use on small UAV. Due to 3D printed case it is possible to optimalize part according to the location of sensor on UAV. First use of this sensor was on our autogyro [TF-G2](). 


## Hardware
### Schema
Full schema is avialible in [PDF]()

### Pinout


| Pin | I2C | SPI  |
| --- |:---:|:----:|
| 1   | +5V | +5V  |
| 2   | SCL | SCK  |
| 3   | --  | MISO |
| 4   | SDA | MOSI |
| 5   | --  | CS   |
| 6   | INT | INT  |
| 7   | GND | GND  |

** IMG **

#### PixHawk autopilot cable

| ASPD | PIN | PixHawk |
|   1  | +5V |  1   |
|   2  | SCL |  2   |
|   4  | SDA |  3   |
|   6  | GND |  4   |




## Usage 

### Python
For reading data from the sensor, we have prepared a python script in PyMLAB library that uses the pySMBus to readou data. It can be used direcly from a computer with a corresponding converter (for example [USBI2C01A]()) or with use of one-board computers (Odroid, raspberry and similar) that have own smbus output.


#### Calibration vertification
Calibration can be verified by mounting of an anemometer to car roof and comparing it to speed obtained from GPS (gpsd). This needs to be done in windless weather.


### PX4
We are now working on implementing the driver into PX4 stack. 

Main usage of this sensor is as airspeed sensor. It can be also used as an external magnetometer.


### Ardupilot
We are currently unable to implement the sensor in the Ardupilot flight stack. However, we will be happy to provide assistance with implementation.


#### configuration
*TODO*