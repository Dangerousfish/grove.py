![](https://user-images.githubusercontent.com/4081906/55451417-67559d00-5605-11e9-96b3-4c6bdd3e770c.png)

grove.py
========

[![Build Status](https://travis-ci.org/Seeed-Studio/grove.py.svg?branch=master)](https://travis-ci.org/Seeed-Studio/grove.py)
[![](https://img.shields.io/pypi/v/grove.py.svg)](https://pypi.python.org/pypi/grove.py)

Python library for Seeedstudio Grove Devices on embeded Linux platform, especially good on below platforms:
- [Coral Dev Board](https://www.seeedstudio.com/Coral-Dev-Board-p-2900.html)
- [NVIDIA Jetson Nano](https://www.seeedstudio.com/NVIDIA-Jetson-Nano-Development-Kit-p-2916.html)
- [Raspberry Pi](https://www.seeedstudio.com/category/Boards-c-17.html)

<br><br>
# Archtecture
To operate grove sensors, the grove.py depends many hardware interface libraries such as mraa/upm/smbus2. 

<br>

![](images/grove-py-arch.png)

<br><br>
# Installation
For beginner or library user only, please install with online method.<br>
For developer, please install dependencies and then install grove.py with source code.

<br>

### Online install
install/update all dependencies and latest grove.py
```shell
curl -sL https://github.com/Seeed-Studio/grove.py/raw/master/install.sh | sudo bash -s -
```

### Install Dependencies
#### Install MRAA and UPM

- Add repository

```shell
# RPi
echo "deb https://seeed-studio.github.io/pi_repo/ stretch main" | sudo tee /etc/apt/sources.list.d/seeed.list
# Coral Dev Board
echo "deb https://seeed-studio.github.io/pi_repo/ mendel-beaker main" | sudo tee /etc/apt/sources.list.d/seeed.list
```

- Add public GPG key

```shell
curl https://seeed-studio.github.io/pi_repo/public.key | sudo apt-key add -
```

[^_^]:
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BB8F40F3


- Install MRAA & UPM

```shell
sudo apt update
# Python2
sudo apt install python-mraa python-upm
# Python3
sudo apt install python3-mraa python3-upm
```

#### Install library raspberry-gpio-python for RPi
```shell
sudo apt update
sudo apt install python-rpi.gpio python3-rpi.gpio
```

#### Install library rpi_ws281x for RPi
```shell
sudo pip install rpi_ws281x
sudo pip3 install rpi_ws281x
```

<br>

### Install grove.py

[^_^]:
    #### From PyPI
    ```shell
    # python2
    sudo pip install grove.py
    # python3
    sudo pip3 install grove.py
    ```

#### From source code
```shell
git clone https://github.com/Seeed-Studio/grove.py
cd grove.py
# Python2
sudo pip install .
# Python3
sudo pip3 install .
```

<br><br>
## Usage
See [demos and how to run](doc/README.md)

<br><br>
## API Documentation
click [here](https://seeed-studio.github.io/grove.py)

[how to update me](sphinx/README.md)

<br><br>
## Contribution
Check list for adding a new grove device, for simple, take [grove_led](grove/grove_led.py) as a example.
- Add a Class in the python source file, and export with `__all__ =`
- Code sytle pep8 is recommanded
- The python source could run directly with `python <file>` and `python3 <file>`
- Add demo code at the near top of source file
- The demo code could run directly with someone python/python3 IDE.
- Add document to class and it's member and show the result by refering to [API document](#api-documentation)
- Add a command item in setup.py `console_scripts` list
- Add a item to command table in [Usage Doc](doc/README.md)
- If the command need argument but not specified, please list available arguments.
- If specified invalid argument, also output usage document then exit.
