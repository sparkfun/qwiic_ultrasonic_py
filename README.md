SparkFun![Qwiic Ultrasonic Python Package](docs/images/ultrasonic-gh-banner-py.png "qwiic Ultrasonic Python Package" )

# SparkFun Qwiic Ultrasonic - Python Package

![PyPi Version](https://img.shields.io/pypi/v/sparkfun_qwiic_ultrasonic)
![GitHub issues](https://img.shields.io/github/issues/sparkfun/qwiic_ultrasonic_py)
![License](https://img.shields.io/github/license/sparkfun/qwiic_ultrasonic_py)
![X](https://img.shields.io/twitter/follow/sparkfun)
[![API](https://img.shields.io/badge/API%20Reference-blue)](https://docs.sparkfun.com/qwiic_ultrasonic_py/classqwiic__ultrasonic_1_1_qwiic_ultrasonic.html)

The SparkFun Qwiic HC-SR04 Ultrasonic Distance Sensor provides a simple and cost effective solution for adding distance measurements (from 2cm to 400cm) to your project. Implementing a SparkFun Qwiic I2C interface, these sensors can be rapidly added to any project with boards that are part of the SparkFun Qwiic ecosystem.

This repository implements a Python package for the SparkFun Qwiic Ultrasonic. This package works with Python, MicroPython and CircuitPython.

### Contents

* [About](#about-the-package)
* [Getting Started](#getting-started)
* [Installation](#installation)
* [Supported Platforms](#supported-platforms)
* [Documentation](https://docs.sparkfun.com/qwiic_ultrasonic_py/classqwiic__ultrasonic_1_1_qwiic_ultrasonic.html)
* [Examples](#examples)

## About the Package

This python package enables the user to access the features of the Ultrasonic Distance Sensor HC-SR04 via a single Qwiic cable. This includes reading distance and setting the I2C address of the device. The capabilities of the Ultrasonic Distance Sensor are each demonstrated in the included examples.

New to qwiic? Take a look at the entire [SparkFun qwiic ecosystem](https://www.sparkfun.com/qwiic).

### Supported SparkFun Products

This Python package supports the following SparkFun qwiic products on Python, MicroPython and Circuit python. 

* [SparkFun Qwiic Ultrasonic Distance Sensor - HC-SR04](https://www.sparkfun.com/sparkfun-qwiic-ultrasonic-distance-sensor-hc-sr04.html)

### Supported Platforms

| Python | Platform | Boards |
|--|--|--|
| Python | Linux | [Raspberry Pi](https://www.sparkfun.com/raspberry-pi-5-8gb.html) , [NVIDIA Jetson Orin Nano](https://www.sparkfun.com/nvidia-jetson-orin-nano-developer-kit.html) via the [SparkFun Qwiic SHIM](https://www.sparkfun.com/sparkfun-qwiic-shim-for-raspberry-pi.html) |
| MicroPython | Raspberry Pi - RP2, ESP32 | [SparkFun RP2040 Thing+](https://www.sparkfun.com/sparkfun-thing-plus-rp2040.html), [SparkFun RP2350 Thing+](https://www.sparkfun.com/sparkfun-thing-plus-rp2350.html), [SparkFun ESP32 Thing+](https://www.sparkfun.com/sparkfun-thing-plus-esp32-wroom-usb-c.html)
|CircuitPython | Raspberry Pi - RP2, ESP32 | [SparkFun RP2040 Thing+](https://www.sparkfun.com/sparkfun-thing-plus-rp2040.html), [SparkFun RP2350 Thing+](https://www.sparkfun.com/sparkfun-thing-plus-rp2350.html), [SparkFun ESP32 Thing+](https://www.sparkfun.com/sparkfun-thing-plus-esp32-wroom-usb-c.html)

> [!NOTE]
> The listed supported platforms and boards are the primary platform targets tested. It is fully expected that this package will work across a wide variety of Python enabled systems. 

## Installation 

The first step to using this package is installing it on your system. The install method depends on the python platform. The following sections outline installation on Python, MicroPython and CircuitPython.

### Python 

The package is primarily installed using the `pip` command, downloading the package from the Python Index - "PyPi". Note - the below instructions outline installation an Linux-based (Raspberry Pi) system.

#### PyPi Installation

The SparkFun Qwiic Ultrasonic Python package is part of the overall SparkFun Qwiic Python package which is hosted on PyPi. On systems that support PyPi installation via pip, this library is installed using the following commands

For all users (note: the user must have sudo privileges):
```sh
sudo pip install sparkfun-qwiic
```
For the current user:

```sh
pip install sparkfun-qwiic
```
---
---
> [!CAUTION]
> **TODO** Put together how this works with the new virtual environments used with the latest Python install
---
---
#### Local Installation
To install, make sure the setuptools package is installed on the system.

Direct installation at the command line:
```sh
python setup.py install
```

To build a package for use with pip:
```sh
python setup.py sdist
 ```
A package file is built and placed in a subdirectory called dist. This package file can be installed using pip.
```sh
cd dist
pip install sparkfun_qwiic_ultrasonic-<version>.tar.gz
```

### MicroPython Installation
If not already installed, follow the [instructions here](https://docs.micropython.org/en/latest/reference/mpremote.html) to install mpremote on your computer.

Connect a device with MicroPython installed to your computer and then install the package directly to your device with mpremote mip.
```sh
mpremote mip install github:sparkfun/qwiic_ultrasonic_py
```

### CircuitPython Installation
If not already installed, follow the [instructions here](https://docs.circuitpython.org/projects/circup/en/latest/#installation) to install CircUp on your computer.

Ensure that you have the latest version of the SparkFun Qwiic CircuitPython bundle. 
```sh
circup bundle-add sparkfun/Qwiic_Py
```

Finally, connect a device with CircuitPython installed to your computer and then install the package directly to your device with circup.
```sh
circup install --py qwiic_ultrasonic
```

Example Use
 ---------------
Below is a quickstart program to print distance measurements (in mm) every tenth of a second.

See the examples directory for more detailed use examples and [examples/README.md](https://github.com/sparkfun/qwiic_ultrasonic_py/blob/main/examples/README.md) for a summary of the available examples.

```python
import qwiic_ultrasonic
import sys
import time

# Here we set the device address. Note that an older version of the Qwiic
# Ultrasonic firmware used a default address of 0x00. If yours uses 0x00,
# you'll need to change the address below. It is also recommended to run
# Example 2 to change the address to the new default.
deviceAddress = qwiic_ultrasonic.QwiicUltrasonic.kDefaultAddress
# deviceAddress = 0x00

def runExample():
	print("\nQwiic Ultrasonic Example 1 - Basic Readings\n")

	# Create instance of device
	my_ultrasonic = qwiic_ultrasonic.QwiicUltrasonic(address=deviceAddress)

	# Check if it's connected
	if my_ultrasonic.is_connected() == False:
		print("The device isn't connected to the system. Please check your connection", \
			file=sys.stderr)
		return

	# Initialize the device
	my_ultrasonic.begin()

	# Loop forever
	while True:
		# Get measurement from sensor. Note that the measured distance actually
		# comes from the previous trigger, so measurements will be slightly delayed
		distance = my_ultrasonic.trigger_and_read()

		# Print measurement
		print("Distance (mm):", distance)

		# Wait a bit
		time.sleep(0.1)
```
<p align="center">
<img src="https://cdn.sparkfun.com/assets/custom_pages/3/3/4/dark-logo-red-flame.png" alt="SparkFun - Start Something">
</p>
