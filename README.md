# PCA9685-Controller
Provides a means of communicating with one or more PCA9685 boards from a Raspberry Pi.

## Requirements
* Raspberry Pi
* PCA9685
* Python 3

## Installation
* I2C communication needs to be activated on the Raspberry Pi. Follow [this](https://www.raspberrypi-spy.co.uk/2014/11/enabling-the-i2c-interface-on-the-raspberry-pi/) guide to do this.

* The following python package also must be installed via this command:
    ``` bash
    sudo pip3 install adafruit-circuitpython-pca9685
    ```

## Example
To start a connection with the (or chained) PCA9685 board create an object with the following command:
``` python
from suitceyes import VibrationMotorDriver

# VibrationMotorDriver accepts a variable length of addresses of the i2c board.
with VibrationMotorDriver(0x41, 0x40) as driver:
    pass 
```
By using the `with` statement all vibrations are stopped once leaving the scope.

To trigger a vibration on a specific pin simply use the `set_vibration(index, intensity)` command. Intensity is a number between 0.0 and 1.0.

``` python
with VibrationMotorDriver(0x41, 0x40) as driver:
    # trigger vibration at pin 16 (on board at address 0x40) at full intensity
    driver.set_vibration(16, 1.0)
    # wait one second 
    time.sleep(1)
    # trigger vibration at pin 16 with half the intensity
    driver.set_vibration(16, 0.5)
    # wait one second 
    time.sleep(1)
    driver.set_vibration(16, 0.5)
```
Note that pins for the board at address `0x41` start at index 0 and go to index 15. Pins at address `0x40` then continue at pin 16 and go up to 31.